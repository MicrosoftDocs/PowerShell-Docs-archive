---
keywords: powershell,cmdlet
ms.date: 01/03/2018
online version: https://learn.microsoft.com/previous-versions/powershell/module/microsoft.powershell.core/about/about_providers?view=powershell-3.0&WT.mc_id=ps-gethelp
schema: 2.0.0
title: about_Providers
---

# About Providers

## Short description

Describes how PowerShell providers provide access to data and
components that would not otherwise be easily accessible at the command line.
The data is presented in a consistent format that resembles a file system
drive.

## Long description

PowerShell providers are Microsoft .NET Framework-based programs that
make the data in a specialized data store available in PowerShell so
that you can view and manage it.

The data that a provider exposes appears in a drive, and you access the data
in a path like you would on a hard disk drive. You can use any of the built-in
cmdlets that the provider supports to manage the data in the provider drive.
And, you can use custom cmdlets that are designed especially for the data.

The providers can also add dynamic parameters to the built-in cmdlets. These
are parameters that are available only when you use the cmdlet with the
provider data.

## Built-in providers

PowerShell includes a set of built-in providers that you can use to
access the different types of data stores.

|Provider    |Drive        |Data store                                 |
|------------|-------------|-------------------------------------------|
|Alias       |Alias:       |PowerShell aliases                 |
|Certificate |Cert:        |x509 certificates for digital signatures   |
|Environment |Env:         |Windows environment variables              |
|FileSystem  |(*)          |File system drives, directories, and files |
|Function    |Function:    |PowerShell functions               |
|Registry    |HKLM:, HKCU: |Windows registry                           |
|Variable    |Variable:    |PowerShell variables               |
|WSMan       |WSMan:       |WS-Management configuration information    |

(*) The FileSystem drives vary on each system.

You can also create your own PowerShell providers, and you can install
providers that others develop. To list the providers that are available in
your session, type:

```powershell
Get-PSProvider
```

## Installing and removing providers

PowerShell providers are delivered to you in PowerShell
snap-ins, which are .NET Framework-based programs that are compiled into .dll
files. The snap-ins can include providers and cmdlets.

Before you use the provider features, you have to install the snap-in and
then add it to your PowerShell session. For more information, see
[about_PSSnapins](about_PSSnapins.md).

You cannot uninstall a provider, although you can remove the PowerShell snap-in
for the provider from the current session. If you do, you will remove all the
contents of the snap-in, including its cmdlets.

To remove a provider from the current session, use the `Remove-PSSnapin`
cmdlet. This cmdlet does not uninstall the provider, but it makes
the provider unavailable in the session.

You can also use the `Remove-PSDrive` cmdlet to remove any drive from the
current session. This data on the drive is not affected, but the drive is no
longer available in that session.

## Viewing providers

To view the PowerShell providers on your computer, type:

```powershell
Get-PSProvider
```

The output lists the built-in providers and the providers that you added to
the session.

## The provider cmdlets

The following cmdlets are designed to work with the data exposed by any
provider. You can use the same cmdlets in the same way to manage the different
types of data that providers expose. After you learn to manage the data of one
provider, you can use the same procedures with the data from any provider.

For example, the `New-Item` cmdlet creates a new item. In the `C:` drive that is
supported by the **FileSystem** provider, you can use `New-Item` to create a new
file or folder. In the drives that are supported by the **Registry** provider,
you can use `New-Item` to create a new registry key. In the `Alias:` drive,
you can use `New-Item` to create a new alias.

For detailed information about any of the following cmdlets, type:

```
Get-Help <cmdlet-name> -Detailed
```

### ChildItem cmdlets

- [Get-ChildItem](xref:Microsoft.PowerShell.Management.Get-ChildItem)

### Content Cmdlets

- [Add-Content](xref:Microsoft.PowerShell.Management.Add-Content)
- [Clear-Content](xref:Microsoft.PowerShell.Management.Clear-Content)
- [Get-Content](xref:Microsoft.PowerShell.Management.Get-Content)
- [Set-Content](xref:Microsoft.PowerShell.Management.Set-Content)

### Item Cmdlets

- [Clear-Item](xref:Microsoft.PowerShell.Management.Clear-Item)
- [Copy-Item](xref:Microsoft.PowerShell.Management.Copy-Item)
- [Get-Item](xref:Microsoft.PowerShell.Management.Get-Item)
- [Invoke-Item](xref:Microsoft.PowerShell.Management.Invoke-Item)
- [Move-Item](xref:Microsoft.PowerShell.Management.Move-Item)
- [New-Item](xref:Microsoft.PowerShell.Management.New-Item)
- [Remove-Item](xref:Microsoft.PowerShell.Management.Remove-Item)
- [Rename-Item](xref:Microsoft.PowerShell.Management.Rename-Item)
- [Set-Item](xref:Microsoft.PowerShell.Management.Set-Item)

### ItemProperty cmdlets

- [Clear-ItemProperty](xref:Microsoft.PowerShell.Management.Clear-ItemProperty)
- [Copy-ItemProperty](xref:Microsoft.PowerShell.Management.Copy-ItemProperty)
- [Get-ItemProperty](xref:Microsoft.PowerShell.Management.Get-ItemProperty)
- [Move-ItemProperty](xref:Microsoft.PowerShell.Management.Move-ItemProperty)
- [New-ItemProperty](xref:Microsoft.PowerShell.Management.New-ItemProperty)
- [Remove-ItemProperty](xref:Microsoft.PowerShell.Management.Remove-ItemProperty)
- [Rename-ItemProperty](xref:Microsoft.PowerShell.Management.Rename-ItemProperty)
- [Set-ItemProperty](xref:Microsoft.PowerShell.Management.Set-ItemProperty)

### Location cmdlets

- [Get-Location](xref:Microsoft.PowerShell.Management.Get-Location)
- [Pop-Location](xref:Microsoft.PowerShell.Management.Pop-Location)
- [Push-Location](xref:Microsoft.PowerShell.Management.Push-Location)
- [Set-Location](xref:Microsoft.PowerShell.Management.Set-Location)

### Path cmdlets

- [Join-Path](xref:Microsoft.PowerShell.Management.Join-Path)
- [Convert-Path](xref:Microsoft.PowerShell.Management.Convert-Path)
- [Split-Path](xref:Microsoft.PowerShell.Management.Split-Path)
- [Resolve-Path](xref:Microsoft.PowerShell.Management.Resolve-Path)
- [Test-Path](xref:Microsoft.PowerShell.Management.Test-Path)

### PSDrive cmdlets

- [Get-PSDrive](xref:Microsoft.PowerShell.Management.Get-PSDrive)
- [New-PSDrive](xref:Microsoft.PowerShell.Management.New-PSDrive)
- [Remove-PSDrive](xref:Microsoft.PowerShell.Management.Remove-PSDrive)

### PSProvider Cmdlets

- [Get-PSProvider](xref:Microsoft.PowerShell.Management.Get-PSProvider)

## Viewing provider data

The primary benefit of a provider is that it exposes its data in a familiar
and consistent way. The model for data presentation is a file system
drive.

To use data that the provider exposes, you view it, move through it,
and change it as though it were data on a hard drive. Therefore, the most
important information about a provider is the name of the drive
that it supports.

The drive is listed in the default display of the `Get-PSProvider` cmdlet,
but you can get information about the provider drive by using the
`Get-PSDrive` cmdlet. For example, to get all the properties of the
Function: drive, type:

```powershell
Get-PSDrive Function | Format-List *
```

You can view and move through the data in a provider drive just as
you would on a file system drive.

To view the contents of a provider drive, use the Get-Item or Get-ChildItem
cmdlets. Type the drive name followed by a colon (:). For example, to
view the contents of the Alias: drive, type:

```powershell
Get-Item alias:
```

You can view and manage the data in any drive from another drive by
including the drive name in the path. For example, to view the
HKLM\Software registry key in the HKLM: drive from another drive, type:

```powershell
Get-ChildItem HKLM:\SOFTWARE\
```

To open the drive, use the Set-Location cmdlet. Remember the colon
when you specify the drive path. For example, to change your location
to the root directory of the Cert: drive, type:

```powershell
Set-Location cert:
```

Then, to view the contents of the Cert: drive, type:

```powershell
Get-ChildItem
```

## Moving through hierarchical data

You can move through a provider drive just as you would a hard disk drive.
If the data is arranged in a hierarchy of items within items, use a
backslash (`\`) to indicate a child item. Use the following format:

```
drive:\location\child-location\...
```

For example, to change your location to the HKLM\Software registry key,
type a Set-Location command, such as:

```powershell
Set-Location HKLM:\SOFTWARE\
```

You can also use relative references to locations. A dot (.) represents the
current location. For example, if you are in the HKLM:\Software\Microsoft
registry key, and you want to list the registry subkeys in the
HKLM:\Software\Microsoft\PowerShell key, type the following command:

```powershell
Get-ChildItem .\PowerShell
```

## Provider Home

Providers also have a **Home** location.  This location is shared by all
`PSDrives` backed by the provider. It can be retrieved by viewing the **Home**
property of the provider.

```powershell
Get-PSProvider | Format-Table Name, Home
```

```output
Name        Home
----        ----
Registry
Alias
Environment
FileSystem  C:\Users\robreed
Function
Variable
Certificate
```

The **FileSystem** provider is the only provider that has a default value for
**Home**. It is the same value as `$Home` see [about_Automatic_Variables](about_Automatic_Variables.md).

You can set the **Home** directory for a provider, for the current session,
using its property.

```powershell
(Get-PSProvider FileSystem).Home = "C:\"
```

The `~` character can be used to represent the provider's home directory.
If the provider does not have a **Home** location set, you will see an error.

```powershell
Cert:\> Set-Location ~
```

```output
Set-Location : Home location for this provider is not set. To set the home
location, call "(get-psprovider 'Certificate').Home = 'path'".
At line:1 char:1
+ Set-Location ~
+ ~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Set-Location],
                              PSInvalidOperationException
...
```

## Finding dynamic parameters

Dynamic parameters are cmdlet parameters that are added to a cmdlet by a
provider. These parameters are available only when the cmdlet is used with the
provider that added them.

For example, the `Cert:` drive adds the **CodeSigningCert** parameter to the
`Get-Item` and `Get-ChildItem` cmdlets. You can use this parameter only when you
use `Get-Item` or `Get-ChildItem` in the `Cert:` drive.

For a list of the dynamic parameters that a provider supports, see the Help
file for the provider. Type:

```
Get-Help <provider-name>
```

For example:

```powershell
Get-Help certificate
```

## Learning about providers

Although all provider data appears in drives, and you use the same methods to
move through them, the similarity stops there. The data stores that the
provider exposes can be as varied as Active Directory locations and Microsoft
Exchange Server mailboxes.

For information about individual PowerShell providers, type:

```
Get-Help <ProviderName>
```

For example:

```powershell
Get-Help registry
```

For a list of Help topics about the providers, type:

```powershell
Get-Help * -Category Provider
```

## See also

[about_Locations](about_Locations.md)

[about_Path_Syntax](about_Path_Syntax.md)
