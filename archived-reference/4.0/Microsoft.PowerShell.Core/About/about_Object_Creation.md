---
keywords: powershell,cmdlet
ms.date: 06/03/2019
online version: https://learn.microsoft.com/previous-versions/powershell/module/microsoft.powershell.core/about/about_object_creation?view=powershell-4.0&WT.mc_id=ps-gethelp
schema: 2.0.0
title: about_Object_Creation
---
# About Object Creation

## SHORT DESCRIPTION

Explains how to create objects in PowerShell.

## LONG DESCRIPTION

You can create objects in PowerShell and use the objects that you create in
commands and scripts.

There are many ways to create objects, this list is not definitive:

- [New-Object](xref:Microsoft.PowerShell.Utility.New-Object): Creates an
  instance of a .NET Framework object or COM object.
- [Import-Csv](xref:Microsoft.PowerShell.Utility.Import-Csv)/
  [ConvertFrom-CSV](xref:Microsoft.PowerShell.Utility.ConvertFrom-Csv):
  Creates custom objects (**PSCustomObject**) from the items defined as comma
  separated values.
- [ConvertFrom-Json](xref:Microsoft.PowerShell.Utility.ConvertFrom-Json):
  Creates custom objects defined in JavaScript Object Notation (JSON).
- [ConvertFrom-StringData](xref:Microsoft.PowerShell.Utility.ConvertFrom-StringData):
  Creates custom objects defined as key value pairs.
- [Add-Type](xref:Microsoft.PowerShell.Utility.Add-Type): Allows you to
  define a class in your PowerShell session that you can instantiate with
  `New-Object`.
- [New-Module](xref:Microsoft.PowerShell.Core.New-Module): The **AsCustomObject** parameter creates a
  custom object you define using script block.
- [Add-Member](xref:Microsoft.PowerShell.Utility.Add-Member): Adds
  properties to existing objects. You can use `Add-Member` to create a custom
  object out of a simple type, like `[System.Int32]`.
- [Select-Object](xref:Microsoft.PowerShell.Utility.Select-Object): Selects
  properties on an object. You can use `Select-Object` to create custom and
  calculated properties on an already instantiated object.

The following additional methods are covered in this article:

- [System.Activator](/dotnet/api/system.activator) class: Creates objects
  given the assembly name and type name.
- Hash tables: Beginning in PowerShell 3.0, you can create objects
  from hash tables of property names and property values.

### Determining constructors for a type

You can determine the available constructors for a given type using the
following sample script.

```powershell
function Get-Constructors ([type]$type)
{
    foreach ($constr in $type.GetConstructors())
    {
        $params = ''
        foreach ($parameter in $constr.GetParameters())
        {
            if ($params -eq '') {
                $params =  "{0} {1}" -f $parameter.parametertype.fullname,
                    $parameter.name
            } else {
              $params +=  ", {0} {1}" -f $parameter.parametertype.fullname,
                  $parameter.name
            }
        }
        Write-Host $($constr.DeclaringType.Name) "($params)"
    }
}
Get-Constructors "System.String"
```

```Output
String (System.Char[] value)
String (System.Char[] value, System.Int32 startIndex, System.Int32 length)
String (System.Char* value)
String (System.Char* value, System.Int32 startIndex, System.Int32 length)
String (System.SByte* value)
String (System.SByte* value, System.Int32 startIndex, System.Int32 length)
String (System.SByte* value, System.Int32 startIndex, System.Int32 length, System.Text.Encoding enc)
String (System.Char c, System.Int32 count)
String (System.ReadOnlySpan`1[[System.Char, System.Private.CoreLib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=7cec85d7bea7798e]] value)
```

### System.Activator class

The **System.Activator** class allows you to create a type by specifying the
assembly and type name.

You can view the static methods of the **System.Activator** class using
`Get-Member` with the **Static** parameter.

```powershell
[System.Activator] | Get-Member -Static
```

The following example creates a **System.Diagnostics.Stopwatch** using the
**CreateInstance** static method which takes a type and array of arguments.
The **System.Diagnostics.Stopwatch** constructor takes no arguments, so we
pass an empty array.

```powershell
[System.Activator]::CreateInstance([System.Diagnostics.Stopwatch], @())
```

```Output
IsRunning Elapsed  ElapsedMilliseconds ElapsedTicks
--------- -------  ------------------- ------------
    False 00:00:00                   0            0
```

### CREATE OBJECTS FROM HASH TABLES

Beginning in PowerShell 3.0, you can create an object from a hash table of
properties and property values.

The syntax is as follows:

```
[<class-name>]@{
  <property-name>=<property-value>
  <property-name>=<property-value>
}
```

This method works only for classes that have a null constructor, that is, a
constructor that has no parameters. The object properties must be public and
settable.

### CREATE CUSTOM OBJECTS FROM HASH TABLES

Custom objects are very useful and are easy to create using the hash table
method. The PSCustomObject class is designed specifically for this purpose.

Custom objects are an excellent way to return customized output from a function
or script. This is more useful than returning formatted output that cannot be
reformatted or piped to other commands.

The commands in the `Test-Object function` set some variable values and then
use those values to create a custom object. You can see this object in use in
the example section of the `Update-Help` cmdlet help topic.

```powershell
function Test-Object {
  $ModuleName = "PSScheduledJob"
  $HelpCulture = "en-us"
  $HelpVersion = "3.1.0.0"
  [PSCustomObject]@{
    "ModuleName"=$ModuleName
    "UICulture"=$HelpCulture
    "Version"=$HelpVersion
  }
  $ModuleName = "PSWorkflow"
  $HelpCulture = "en-us"
  $HelpVersion = "3.0.0.0"
  [PSCustomObject]@{
    "ModuleName"=$ModuleName
    "UICulture"=$HelpCulture
    "Version"=$HelpVersion
  }
}
Test-Object
```

The output of this function is a collection of custom objects formatted as a
table by default.

```Output
ModuleName        UICulture      Version
---------         ---------      -------
PSScheduledJob    en-us          3.1.0.0
PSWorkflow        en-us          3.0.0.0
```

Users can manage the properties of the custom objects just as they do with
standard objects.

```powershell
(Test-Object).ModuleName
```

```Output
 PSScheduledJob
 PSWorkflow
```

#### CREATE NON-CUSTOM OBJECTS FROM HASH TABLES

You can also use hash tables to create objects for non-custom classes. When
you create an object for a non-custom class, the full namespace name is
required unless class is in the **System** namespace. Use only the properties of
the class.

For example, the following command creates a session option object.

```powershell
[System.Management.Automation.Remoting.PSSessionOption]@{
  IdleTimeout=43200000
  SkipCnCheck=$True
}
```

The requirements of the hash table feature, especially the null constructor
requirement, eliminate many existing classes. However, most PowerShell option
classes are designed to work with this feature, as well as other very useful
classes, such as the **ScheduledJobTrigger** class.

```powershell
[Microsoft.PowerShell.ScheduledJob.ScheduledJobTrigger]@{
  Frequency="Daily"
  At="15:00"
}
```

```Output
Id   Frequency   Time                   DaysOfWeek  Enabled
--   ---------   ----                   ----------  -------
0    Daily       6/6/2012 3:00:00 PM                True
```

You can also use the hash table feature when setting parameter values. For
example, the value of the **SessionOption** parameter of the `New-PSSession`
cmdlet and the value of the **JobTrigger** parameter of `Register-ScheduledJob`
can be a hash table.

```powershell
New-PSSession -ComputerName Server01 -SessionOption @{
  IdleTimeout=43200000
  SkipCnCheck=$True
}
Register-ScheduledJob Name Test -FilePath .\Get-Inventory.ps1 -Trigger @{
  Frequency="Daily"
  At="15:00"
}
```

### Generic Objects

You can also create generic objects in PowerShell. Generics are classes,
structures, interfaces, and methods that have placeholders (type parameters)
for one or more of the types that they store or use.

The following example creates a **Dictionary** object.

```powershell
$dict = New-Object 'System.Collections.Generic.Dictionary[String,Int]'
$dict.Add("One", 1)
$dict
```

```Output
Key Value
--- -----
One     1
```

For more information on Generics, see [Generics in .NET](/dotnet/standard/generics).

## SEE ALSO

[about_Objects](about_Objects.md)

[about_Methods](about_Methods.md)

[about_Properties](about_Properties.md)

[about_Pipelines](about_Pipelines.md)
