---
external help file: PSModule-help.xml
Locale: en-US
Module Name: PowershellGet
ms.date: 07/16/2019
online version: https://learn.microsoft.com/previous-versions/powershell/module/powershellget/update-module?view=powershell-5.0&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Update-Module
---

# Update-Module

## SYNOPSIS
Downloads and installs the newest version of specified modules from an online gallery to the local
computer.

## SYNTAX

### All

```
Update-Module [[-Name] <String[]>] [-RequiredVersion <Version>] [-MaximumVersion <Version>] [-Force]
 [-WhatIf] [-Confirm] [<CommonParameters>]
```

## DESCRIPTION

The `Update-Module` cmdlet installs a module's newest version from an online gallery. You're
prompted to confirm the update before it's installed. Updates are installed only for modules that
were installed on the local computer with `Install-Module`. `Update-Module` searches
`$env:PSModulePath` for installed modules.

`Update-Module` with no parameters specified updates all installed modules. To specify a module to
update, use the **Name** parameter. You can update to a module's specific version by using the
**RequiredVersion** parameter.

If an installed module is already the newest version, the module isn't updated. If the module isn't
found in `$env:PSModulePath`, an error is displayed.

To display the installed modules, use `Get-InstalledModule`.

## EXAMPLES

### Example 1: Update all modules

This example updates all installed modules to the newest version in an online gallery.

```powershell
Update-Module
```

### Example 2: Update a module by name

This example updates a specific module to the newest version in an online gallery.

```powershell
Update-Module -Name SpeculationControl
```

`Update-Module` uses the **Name** parameter to update a specific module, **SpeculationControl**.

### Example 3: View what-if Update-Module runs

This example does a what-if scenario to show what happens if `Update-Module` is run. The command
isn't run.

```powershell
Update-Module -WhatIf
```

```Output
What if: Performing the operation "Update-Module" on target "Version '2.8.0' of module
  'Carbon', updating to version '2.8.1'".
What if: Performing the operation "Update-Module" on target "Version '1.0.10' of module
  'SpeculationControl', updating to version '1.0.14'".
```

`Update-Module` uses the **WhatIf** parameter display what would happen if `Update-Module` were run.

### Example 4: Update a module to a specified version

In this example, a module is updated to a specific version. The version must exist in the online
gallery or an error is displayed.

```powershell
Update-Module -Name SpeculationControl -RequiredVersion 1.0.14
```

`Update-Module` uses the **Name** parameter to specify the module, **SpeculationControl**. The
**RequiredVersion** parameter specifies the version, **1.0.14**.

### Example 5: Update a module without confirmation

This example doesn't request confirmation to update the module to the newest version from an online
gallery. If the module is already installed, the **Force** parameter reinstalls the module.

```powershell
Update-Module -Name SpeculationControl -Force
```

`Update-Module` uses the **Name** parameter to specify the module, **SpeculationControl**. The
**Force** parameter updates the module without requesting user confirmation.

## PARAMETERS

### -Confirm

Prompts you for confirmation before running `Update-Module`.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: cf

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Force

Forces an update of each specified module without a prompt to request confirmation. If the module is
already installed, **Force** reinstalls the module.

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

### -MaximumVersion

Specifies the maximum version of a single module to update. You can't add this parameter if you're
attempting to update multiple modules. The **MaximumVersion** and the **RequiredVersion** parameters
can't be used in the same command.

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

Specifies the names of one or more modules to update. `Update-Module` searches `$env:PSModulePath`
for the modules to update. If no matches are found in `$env:PSModulePath` for the specified module
name, an error occurs.

Wildcards are accepted in module names. If you add wildcard characters to the specified name and no
matches are found, no error occurs.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases:

Required: False
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: True
```

### -RequiredVersion

Specifies the exact version to which the existing installed module will be updated. The version
specified by **RequiredVersion** must exist in the online gallery or an error is displayed. If more
than one module is updated in a single command, you can't use **RequiredVersion**.

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

### -WhatIf

Shows what would happen if `Update-Module` runs. The cmdlet isn't run.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: wi

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable,
-InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose,
-WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

For PowerShell 5.1 or below, the default scope in an elevated session is **AllUsers**, and in a
non-elevated session, **CurrentUser**. Module updates for **AllUsers**,
`$env:ProgramFiles\PowerShell\Modules`, need elevated permissions. Module updates for
**CurrentUser**, `$home\Documents\PowerShell\Modules`, don't need elevated permissions.

`Update-Module` runs on PowerShell 3.0 or later releases of PowerShell, on Windows 7 or Windows 2008
R2 and later releases of Windows.

If the module that you specify with the **Name** parameter wasn't installed by using
`Install-Module`, an error occurs.

You can only run `Update-Module` on modules that you installed from the online gallery by running
`Install-Module`.

If `Update-Module` attempts to update binaries that are in use, `Update-Module` returns an error
that identifies the problem processes. The user is informed to retry `Update-Module` after the
processes are stopped.

## RELATED LINKS

[Find-Module](Find-Module.md)

[Get-InstalledModule](Get-InstalledModule.md)

[Install-Module](Install-Module.md)

[Publish-Module](Publish-Module.md)

[Uninstall-Module](Uninstall-Module.md)
