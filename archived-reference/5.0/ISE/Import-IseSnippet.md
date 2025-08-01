---
external help file: ISE-help.xml
Locale: en-US
Module Name: ISE
ms.date: 06/09/2017
online version: https://learn.microsoft.com/previous-versions/powershell/module/ise/import-isesnippet?view=powershell-5.0&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Import-IseSnippet
---
# Import-IseSnippet

## SYNOPSIS
Imports ISE snippets into the current session

## SYNTAX

### FromFolder (Default)

```
Import-IseSnippet [-Path] <String> [-Recurse] [<CommonParameters>]
```

### FromModule

```
Import-IseSnippet [-Recurse] -Module <String> [-ListAvailable] [<CommonParameters>]
```

## DESCRIPTION

The **Import-IseSnippet** cmdlet imports reusable text "snippets" from a module or a directory into the current session.
The snippets are immediately available for use in Windows PowerShell ISE.
This cmdlet works only in Windows PowerShell Integrated Scripting Environment (ISE).

To view and use the imported snippets, from the Windows PowerShell ISEEdit menu, click Start Snippets or press Ctrl + J.

Imported snippets are available only in the current session.
To import the snippets into all Windows PowerShell ISE sessions, add an **Import-IseSnippet** command to your Windows PowerShell profile or copy the snippet files to your local snippets directory ($home\Documents\WindowsPowershell\Snippets).

To import snippets, they must be properly formatted in the snippet XML for Windows PowerShell ISE snippets and saved in Snippet.ps1xml files.
To create eligible snippets, use the New-IseSnippet cmdlet.
New-IseSnippet creates a \<SnippetTitle\>.Snippets.ps1xml file in the $home\Documents\WindowsPowerShell\Snippets directory.
You can move or copy the snippets to the Snippets directory of a Windows PowerShell module, or to any other directory.

The Get-IseSnippet cmdlet, which gets user-created snippets in the local snippets directory, does not get imported snippets.

This cmdlet was introduced in Windows PowerShell 3.0.

## EXAMPLES

### Example 1: Import snippets from a directory

```powershell
Import-IseSnippet -Path \\Server01\Public\Snippets -Recurse
```

This command imports the snippets from the \\\\Server01\Public\Snippets directory into the current session.
It uses the Recurse parameter to get snippets from all subdirectories of the Snippets directory.

### Example 2: Import snippets from a module

```powershell
Import-IseSnippet -Module SnippetModule -ListAvailable
```

This command imports the snippets from the SnippetModule module.
The command uses the **ListAvailable** parameter to import the snippets even if the SnippetModule module is not imported into the user's session when the command runs.

### Example 3: Find snippets in modules

```powershell
($env:PSModulePath).split(";") | ForEach-Object {dir $_\*\Snippets\*.Snippets.ps1xml -ErrorAction SilentlyContinue} | ForEach-Object {$_.fullname}
```

This command gets snippets in all installed modules in the PSModulePath environment variable.

### Example 4: Import all module snippets

```powershell
($env:PSModulePath).split(";") | ForEach-Object {dir $_\*\Snippets\*.Snippets.ps1xml -ErrorAction SilentlyContinue} | ForEach-Object {$psise.CurrentPowerShellTab.Snippets.Load($_)}
```

This command imports all snippets from all installed modules into the current session.
Typically, you don't need to run a command like this because modules that have snippets will use the **Import-IseSnippet** cmdlet to import them for you when the module is imported.

### Example 5: Copy all module snippets

```powershell
($env:PSModulePath).split(";") | ForEach-Object {dir $_\*\Snippets\*.Snippets.ps1xml -ErrorAction SilentlyContinue} | Copy-Item -Destination $home\Documents\WindowsPowerShell\Snippets
```

This command copies the snippet files from all installed modules into the Snippets directory of the current user.
Unlike imported snippets, which affect only the current session, copied snippets are available in every Windows PowerShell ISE session.

## PARAMETERS

### -Path
Specifies the path to the snippets directory in which this cmdlet imports snippets.

```yaml
Type: String
Parameter Sets: FromFolder
Aliases:

Required: True
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Recurse
Indicate that this cmdlet imports snippets from all subdirectories of the value of the **Path** parameter.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Module

Imports snippets from the specified module into the current session.
Wildcard characters are not supported.

This parameter imports snippets from Snippet.ps1xml files in the Snippets subdirectory in the module path, such as $home\Documents\WindowsPowerShell\Modules\\\<ModuleName\>\Snippets.

This parameter is designed to be used by module authors in a startup script, such as a script specified in the **ScriptsToProcess** key of a module manifest.
Snippets in a module are not automatically imported with the module, but you can use an **Import-IseSnippet** command to import them.

```yaml
Type: String
Parameter Sets: FromModule
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ListAvailable
Indicates that this cmdlet gets snippets from modules that are installed on the computer, even if the modules are not imported into the current session.
If this parameter is omitted, and the module that is specified by the **Module** parameter is not imported into the current session, the attempt to get the snippets from the module will fail.

This parameter is valid only when the **Module** parameter is used in the command.

```yaml
Type: SwitchParameter
Parameter Sets: FromModule
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### None

This cmdlet does not take input from the pipeline.

## OUTPUTS

### None

This cmdlet does not generate output.

## NOTES

- You cannot use the Get-IseSnippet cmdlet to get imported snippets. **Get-IseSnippet** gets only snippets in the $home\Documents\WindowsPowerShell\Snippets directory.
- **Import-IseSnippet** uses the **Load** static method of Microsoft.PowerShell.Host.ISE.ISESnippetCollection objects. You can also use the Load method of snippets in the Windows PowerShell ISE object model: $psISE.CurrentPowerShellTab.Snippets.Load()
- The New-IseSnippet cmdlet stores new user-created snippets in unsigned .ps1xml files. As such, Windows PowerShell cannot load them into a session in which the execution policy is **AllSigned** or **Restricted**. In a **Restricted** or **AllSigned** session, you can create, get, and import unsigned user-created snippets, but you cannot use them in the session.

  To use unsigned user-created snippets that the **Import-IseSnippet** cmdlet returns, change the execution policy, and then restart Windows PowerShell ISE.

  For more information about Windows PowerShell execution policies, see about_Execution_Policies.

## RELATED LINKS

[Get-IseSnippet](Get-IseSnippet.md)

[New-IseSnippet](New-IseSnippet.md)

[about_Execution_Policies](../Microsoft.PowerShell.Core/About/about_Execution_Policies.md)


