---
external help file: System.Management.Automation.dll-Help.xml
Locale: en-US
Module Name: Microsoft.PowerShell.Core
ms.date: 06/09/2017
online version: https://learn.microsoft.com/previous-versions/powershell/module/microsoft.powershell.core/save-help?view=powershell-3.0&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Save-Help
---
# Save-Help

## SYNOPSIS
Downloads and saves the newest help files to a file system directory.

## SYNTAX

### Path (Default)

```
Save-Help [-DestinationPath] <String[]> [[-Module] <PSModuleInfo[]>] [[-UICulture] <CultureInfo[]>]
 [-Credential <PSCredential>] [-UseDefaultCredentials] [-Force] [<CommonParameters>]
```

### LiteralPath
```
Save-Help -LiteralPath <String[]> [[-Module] <PSModuleInfo[]>] [[-UICulture] <CultureInfo[]>]
 [-Credential <PSCredential>] [-UseDefaultCredentials] [-Force] [<CommonParameters>]
```

## DESCRIPTION

The **Save-Help** cmdlet downloads the newest help files for PowerShell modules and saves them to a directory that you specify.
This feature lets you update the help files on computers that do not have access to the Internet, and makes it easier to update the help files on multiple computers.

In Windows PowerShell 3.0, **Save-Help** worked only for modules that are installed on the local computer.
Although it was possible to import a module from a remote computer, or obtain a reference to a **PSModuleInfo** object from a remote computer by using PowerShell remoting, the **HelpInfoUri** property was not preserved, and **Save-Help** would not work for remote module Help.

To install saved help files, run the Update-Help cmdlet.
Add its *SourcePath* parameter to specify the folder in which you saved the Help files.

Without parameters, a **Save-Help** command downloads the newest help for all modules in the session and for modules that are installed on the computer in a location listed in the **PSModulePath** environment variable.
This action skips modules that do not support Updatable Help without warning.

The **Save-Help** cmdlet checks the version of any help files in the destination folder.
If newer help files are available, this cmdlet downloads the newest help files from the Internet, and then saves them in the folder.
The **Save-Help** cmdlet works just like the Update-Help cmdlet, except that it saves the downloaded cabinet (.cab) files, instead of extracting the help files from the cabinet files and installing them on the computer.

The saved help for each module consists of one help information (HelpInfo XML) file and one cabinet (.cab) file for the help files each UI culture.
You do not have to extract the help files from the cabinet file.
The **Update-Help** cmdlet extracts the help files, validates the XML for safety, and then installs the help files and the help information file in a language-specific subfolder of the module folder.

To save the help files for modules in the PowerShell installation folder ($pshome\Modules), start PowerShell by using the Run as administrator option.
You must be a member of the Administrators group on the computer to download the help files for these modules.

This cmdlet was introduced in Windows PowerShell 3.0.

## EXAMPLES

### Example 1: Save help for all modules

```
PS> Save-Help -DestinationPath \\Server01\FileShare01
```

This command downloads the newest help files for all modules in the UI culture set for Windows on the local computer.
It saves the help files in the \\\\Server01\Fileshare01 directory.

### Example 2: Save help for a module on the computer

```
PS> Save-Help -Module ServerManager -DestinationPath \\Server01\FileShare01 -Credential Domain01/Admin01
```

This command downloads the newest help files for the ServerManager module and saves them in the \\\\Server01\Fileshare01 directory.

When a module is installed on the computer, you can type the module name as the value of the **Module** parameter, even if the module is not imported into the current session.

The command uses the **Credential** parameter to supply the credentials of a user who has permission to write to the file share.

### Example 3: Save help for a module on a different computer

```
PS> Invoke-Command -ComputerName Server02 {Get-Module -Name CustomSQL -ListAvailable} | Save-Help -DestinationPath \\Server01\FileShare01 -Credential Domain01\Admin01
```

These commands download the newest help files for the CustomSQL module and save them in the \\\\Server01\Fileshare01 directory.

Because the CustomSQL module is not installed on the computer, the sequence includes an **Invoke-Command** command that gets the module object for the CustomSQL module from the Server02 computer and then pipes the module object to the **Save-Help** cmdlet.

When a module is not installed on the computer, **Save-Help** needs the module object, which includes information about the location of the newest help files.

### Example 4: Save help for a module in multiple languages

```
PS> Save-Help -Module Microsoft.PowerShell* -UICulture de-DE, en-US, fr-FR, ja-JP -DestinationPath D:\Help
```

This command saves help for the Windows PowerShell Core modules in four different UI cultures.
The language packs for these locales do not need to be installed on the computer.

**Save-Help** can download help files for modules in different UI cultures only when the module owner makes the translated files available on the Internet.

### Example 5: Save help more than once each day

```
PS> Save-Help -Force -DestinationPath \\Server3\AdminShare\Help
```

This command saves help for all modules that are installed on the computer.
The command uses It uses the **Force** parameter to override the rule that prevents the **Save-Help** cmdlet from downloading help more than once in each 24-hour period.

The **Force** parameter also overrides the 1 GB restriction and circumvents version checking, so you can download files even if the version is not greater than the version in the destination directory.

The command uses the **Save-Help** cmdlet to download and save the help files to the specified directory.
The **Force** parameter is required when you need to run a **Save-Help** command more than once each day.

## PARAMETERS

### -Credential

Specifies a user credential.
This cmdlet runs the command by using credentials of a user who has permission to access the file system location specified by the *DestinationPath* parameter.
This parameter is valid only when the *DestinationPath* or *LiteralPath* parameter is used in the command.

This parameter enables you to run **Save-Help** commands that use the *DestinationPath* parameter on remote computers.
By providing explicit credentials, you can run the command on a remote computer and access a file share on a third computer without encountering an access denied error or using CredSSP authentication to delegate credentials.

```yaml
Type: PSCredential
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -DestinationPath

Specifies the path of the folder in which the help files are saved.
Do not specify a file name or file name extension.

```yaml
Type: String[]
Parameter Sets: Path
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Force

Indicates that this cmdlet does not follow the once-per-day limitation, skips version checking, and downloads files that exceed the 1 GB limit.

Without this parameter, only one **Save-Help** command for each module is permitted in each 24-hour period, downloads are limited to 1 GB of uncompressed content per module, and help files for a module are installed only when they are newer than the files on the computer.

The once-per-day limit protects the servers that host the help files, and makes it practical for you to add a **Save-Help** command to your PowerShell profile.

To save help for a module in multiple UI cultures without the *Force* parameter, include all UI cultures in the same command, such as: `Save-Help -Module PSScheduledJobs -UICulture en-US, fr-FR, pt-BR`

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -LiteralPath

Specifies a path of the destination folder.
Unlike the value of the *DestinationPath* parameter, the value of the *LiteralPath* parameter is used exactly as it is typed.
No characters are interpreted as wildcard characters.
If the path includes escape characters, enclose it in single quotation marks.
Single quotation marks tell PowerShell not to interpret any characters as escape sequences.

```yaml
Type: String[]
Parameter Sets: LiteralPath
Aliases: PSPath

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Module

Specifies modules for which this cmdlet downloads help.
Enter one or more module names or name patters in a comma-separated list or in a file that has one module name on each line.
Wildcard characters are permitted.
You can also pipe module objects from the Get-Module cmdlet to **Save-Help**.

By default, **Save-Help** downloads help for all modules that support Updatable Help and are installed on the local computer in a location listed in the **PSModulePath** environment variable.

To save help for modules that are not installed on the computer, run a **Get-Module** command on a remote computer.
Then pipe the resulting module objects to the **Save-Help** cmdlet or submit the module objects as the value of the *Module* or *InputObject* parameters.

If the module that you specify is installed on the computer, you can enter the module name or a module object.
If the module is not installed on the computer, you must enter a module object, such as one returned by the **Get-Module** cmdlet.

The *Module* parameter of the **Save-Help** cmdlet does not accept the full path of a module file or module manifest file.
To save help for a module that is not in a **PSModulePath** location, import the module into the current session before you run the **Save-Help** command.

A value of "*" (all) attempts to update help for all modules that are installed on the computer.
This includes modules that do not support Updatable Help.
This value might generate errors when the command encounters modules that do not support Updatable Help.

```yaml
Type: PSModuleInfo[]
Parameter Sets: (All)
Aliases: Name

Required: False
Position: 1
Default value: None
Accept pipeline input: True (ByPropertyName, ByValue)
Accept wildcard characters: True
```

### -UICulture

Specifies UI culture values for which this cmdlet gets updated help files.
Enter one or more language codes, such as es-ES, a variable that contains culture objects, or a command that gets culture objects, such as a Get-Culture or Get-UICulture command.

Wildcard characters are not permitted.
Do not specify a partial language code, such as "de".

By default, **Save-Help** gets help files in the UI culture set for Windows or its fallback culture.
If you specify the *UICulture* parameter, **Save-Help** looks for help only for the specified UI culture, not in any fallback culture.

```yaml
Type: CultureInfo[]
Parameter Sets: (All)
Aliases:

Required: False
Position: 2
Default value: Current UI culture
Accept pipeline input: False
Accept wildcard characters: False
```

### -UseDefaultCredentials

Indicates that this cmdlet runs the command, including the web download, with the credentials of the current user.
By default, the command runs without explicit credentials.

This parameter is effective only when the web download uses NTLM, negotiate, or Kerberos-based authentication.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### System.Management.Automation.PSModuleInfo

You can pipe a module object from the **Get-Module** cmdlet to the *Module* parameter of **Save-Help**.

## OUTPUTS

### None

This cmdlet does not generate any output.

## NOTES

* To save help for modules in the $pshome\Modules folder, start PowerShell by using the Run as administrator option. Only members of the Administrators group on the computer can download help for modules in the $pshome\Modules folder.
* The saved help for each module consists of one help information (HelpInfo XML) file and one cabinet (.cab) file for the help files each UI culture. You do not have to extract the help files from the cabinet file. The Update-Help cmdlet extracts the help files, validates the XML, and then installs the help files and the help information file in a language-specific subfolder of the module folder.
* The **Save-Help** cmdlet can save help for modules that are not installed on the computer. However, because help files are installed in the module folder, the **Update-Help** cmdlet can install updated help file only for modules that are installed on the computer.
* If **Save-Help** cannot find updated help files for a module, or cannot find updated help files in the specified language, it continues silently without displaying an error message. To see which files were saved by the command, specify the *Verbose* parameter.
* Modules are the smallest unit of updatable help. You cannot save help for a particular cmdlet, only for all cmdlets in module. To find the module that contains a particular cmdlet, use the **ModuleName** property together with the Get-Command cmdlet, for example, `(Get-Command \<cmdlet-name\>).ModuleName`
* **Save-Help** supports all modules and the PowerShell Core snap-ins. It does not support any other snap-ins.
* The **Update-Help** and **Save-Help** cmdlets use the following ports to download help files: Port 80 for HTTP and port 443 for HTTPS.
* The **Update-Help** and **Save-Help** cmdlets are not supported on Windows Preinstallation Environment (Windows PE).

## RELATED LINKS

[Get-Help](Get-Help.md)

[Get-Module](Get-Module.md)

[Update-Help](Update-Help.md)
