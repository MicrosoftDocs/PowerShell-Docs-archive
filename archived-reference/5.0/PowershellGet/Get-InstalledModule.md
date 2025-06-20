---
external help file: PSModule-help.xml
Locale: en-US
Module Name: PowershellGet
ms.date: 05/23/2019
online version: https://learn.microsoft.com/previous-versions/powershell/module/powershellget/get-installedmodule?view=powershell-5.0&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Get-InstalledModule
---
# Get-InstalledModule

## SYNOPSIS
Gets installed modules on a computer.

## SYNTAX

```
Get-InstalledModule [[-Name] <String[]>] [-MinimumVersion <Version>] [-RequiredVersion <Version>]
 [-MaximumVersion <Version>] [<CommonParameters>]
```

## DESCRIPTION
The `Get-InstalledModule` cmdlet gets PowerShell modules that are installed on a computer using
PowerShellGet. To see all modules installed on the system, use the `Get-Module -ListAvailable`
command.

## EXAMPLES

### Example 1: Get all installed modules

```powershell
Get-InstalledModule
```

```Output
Version    Name                                Type       Repository     Description
-------    ----                                ----       ----------     -----------
2.0.0      PSGTEST-UploadMultipleVersionOfP... Module     GalleryINT     Module for DAC functionality
1.3.5      AzureAutomationDebug                Module     PSGallery      Module for debugging Azure Automation runbooks, emulating AA native cmdlets
1.0.1      AzureRM.Automation                  Module     PSGallery      Microsoft Azure PowerShell - Automation service cmdlets for Azure Resource Manager
```

This command gets all installed modules.

### Example 2: Get specific versions of a module

```powershell
Get-InstalledModule -Name "AzureRM.Automation" -MinimumVersion 1.0 -MaximumVersion 2.0
```

```Output
Version    Name                                Type       Repository     Description
-------    ----                                ----       ----------     -----------
1.0.1      AzureRM.Automation                  Module     PSGallery      Microsoft Azure PowerShell - Automation service cmdlets for Azure Resource Manager
```

This command gets versions of the AzureRM.Automation module from version 1.0 through version 2.0.

## PARAMETERS

### -MaximumVersion

Specifies the maximum, or newest, version of a module to get.
The **MaximumVersion** and **RequiredVersion** parameters are mutually exclusive; you cannot use both
parameters in the same command.

```yaml
Type: Version
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -MinimumVersion

Specifies the minimum version of a single module to get.
The **MinimumVersion** and **RequiredVersion** parameters are mutually exclusive; you cannot use both
parameters in the same command.

```yaml
Type: Version
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Name

Specifies an array of names of modules to get.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases:

Required: False
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -RequiredVersion

Specifies the exact version of a module to get.

```yaml
Type: Version
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable,
-InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose,
-WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](../Microsoft.PowerShell.Core/About/about_CommonParameters.md).

## INPUTS

## OUTPUTS

### Microsoft.PowerShell.Commands.PSRepositoryItemInfo

## NOTES

## RELATED LINKS
