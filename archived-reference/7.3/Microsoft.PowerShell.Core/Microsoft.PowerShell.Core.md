---
Download Help Link: https://aka.ms/powershell73-help
Help Version: 7.3.0.0
Locale: en-US
Module Guid: 00000000-0000-0000-0000-000000000000
Module Name: Microsoft.PowerShell.Core
ms.date: 12/04/2023
schema: 2.0.0
title: Microsoft.PowerShell.Core
---
# Microsoft.PowerShell.Core Module

## Description

The **Microsoft.PowerShell.Core** snap-in contains cmdlets and providers that manage the basic
features of PowerShell. PowerShell loads **Microsoft.PowerShell.Core** snap-in automatically at
startup. This is not a module. You can't import it using `Import-Module` or remove it using
`Remove-Module`.

## Microsoft.PowerShell.Core Cmdlets

### [Add-History](Add-History.md)
Appends entries to the session history.

### [Clear-History](Clear-History.md)
Deletes entries from the PowerShell session command history.

### [Clear-Host](Clear-Host.md)
Clears the display in the host program.

### [Connect-PSSession](Connect-PSSession.md)
Reconnects to disconnected sessions.

### [Debug-Job](Debug-Job.md)
Debugs a running background or remote job.

### [Disable-ExperimentalFeature](Disable-ExperimentalFeature.md)
Disable an experimental feature on startup of new instance of PowerShell.

### [Disable-PSRemoting](Disable-PSRemoting.md)
Prevents PowerShell endpoints from receiving remote connections.

### [Disable-PSSessionConfiguration](Disable-PSSessionConfiguration.md)
Disables session configurations on the local computer.

### [Disconnect-PSSession](Disconnect-PSSession.md)
Disconnects from a session.

### [Enable-ExperimentalFeature](Enable-ExperimentalFeature.md)
Enable an experimental feature on startup of new instance of PowerShell.

### [Enable-PSRemoting](Enable-PSRemoting.md)
Configures the computer to receive remote commands.

### [Enable-PSSessionConfiguration](Enable-PSSessionConfiguration.md)
Enables the session configurations on the local computer.

### [Enter-PSHostProcess](Enter-PSHostProcess.md)
Connects to and enters into an interactive session with a local process.

### [Enter-PSSession](Enter-PSSession.md)
Starts an interactive session with a remote computer.

### [Exit-PSHostProcess](Exit-PSHostProcess.md)
Closes an interactive session with a local process.

### [Exit-PSSession](Exit-PSSession.md)
Ends an interactive session with a remote computer.

### [Export-ModuleMember](Export-ModuleMember.md)
Specifies the module members that are exported.

### [ForEach-Object](ForEach-Object.md)
Performs an operation against each item in a collection of input objects.

### [Get-Command](Get-Command.md)
Gets all commands.

### [Get-ExperimentalFeature](Get-ExperimentalFeature.md)
Gets experimental features.

### [Get-Help](Get-Help.md)
Displays information about PowerShell commands and concepts.

### [Get-History](Get-History.md)
Gets a list of the commands entered during the current session.

### [Get-Job](Get-Job.md)
Gets PowerShell background jobs that are running in the current session.

### [Get-Module](Get-Module.md)
List the modules imported in the current session or that can be imported from the PSModulePath.

### [Get-PSHostProcessInfo](Get-PSHostProcessInfo.md)
Gets process information about the PowerShell host.

### [Get-PSSession](Get-PSSession.md)
Gets the PowerShell sessions on local and remote computers.

### [Get-PSSessionCapability](Get-PSSessionCapability.md)
Gets the capabilities of a specific user on a constrained session configuration.

### [Get-PSSessionConfiguration](Get-PSSessionConfiguration.md)
Gets the registered session configurations on the computer.

### [Get-PSSubsystem](Get-PSSubsystem.md)
Retrieves information about the subsystems registered in PowerShell.

### [Import-Module](Import-Module.md)
Adds modules to the current session.

### [Invoke-Command](Invoke-Command.md)
Runs commands on local and remote computers.

### [Invoke-History](Invoke-History.md)
Runs commands from the session history.

### [New-Module](New-Module.md)
Creates a new dynamic module that exists only in memory.

### [New-ModuleManifest](New-ModuleManifest.md)
Creates a new module manifest.

### [New-PSRoleCapabilityFile](New-PSRoleCapabilityFile.md)
Creates a file that defines a set of capabilities to be exposed through a session configuration.

### [New-PSSession](New-PSSession.md)
Creates a persistent connection to a local or remote computer.

### [New-PSSessionConfigurationFile](New-PSSessionConfigurationFile.md)
Creates a file that defines a session configuration.

### [New-PSSessionOption](New-PSSessionOption.md)
Creates an object that contains advanced options for a PSSession.

### [New-PSTransportOption](New-PSTransportOption.md)
Creates an object that contains advanced options for a session configuration.

### [Out-Default](Out-Default.md)
Sends the output to the default formatter and to the default output cmdlet.

### [Out-Host](Out-Host.md)
Sends output to the command line.

### [Out-Null](Out-Null.md)
Hides the output instead of sending it down the pipeline or displaying it.

### [Receive-Job](Receive-Job.md)
Gets the results of the PowerShell background jobs in the current session.

### [Receive-PSSession](Receive-PSSession.md)
Gets results of commands in disconnected sessions

### [Register-ArgumentCompleter](Register-ArgumentCompleter.md)
Registers a custom argument completer.

### [Register-PSSessionConfiguration](Register-PSSessionConfiguration.md)
Creates and registers a new session configuration.

### [Remove-Job](Remove-Job.md)
Deletes a PowerShell background job.

### [Remove-Module](Remove-Module.md)
Removes modules from the current session.

### [Remove-PSSession](Remove-PSSession.md)
Closes one or more PowerShell sessions (PSSessions).

### [Save-Help](Save-Help.md)
Downloads and saves the newest help files to a file system directory.

### [Set-PSDebug](Set-PSDebug.md)
Turns script debugging features on and off, sets the trace level, and toggles strict mode.

### [Set-PSSessionConfiguration](Set-PSSessionConfiguration.md)
Changes the properties of a registered session configuration.

### [Set-StrictMode](Set-StrictMode.md)
Establishes and enforces coding rules in expressions, scripts, and script blocks.

### [Start-Job](Start-Job.md)
Starts a PowerShell background job.

### [Stop-Job](Stop-Job.md)
Stops a PowerShell background job.

### [Switch-Process](Switch-Process.md)
On Linux and macOS, the cmdlet calls the `execv()` function to provide similar behavior as POSIX shells.

### [Test-ModuleManifest](Test-ModuleManifest.md)
Verifies that a module manifest file accurately describes the contents of a module.

### [Test-PSSessionConfigurationFile](Test-PSSessionConfigurationFile.md)
Verifies the keys and values in a session configuration file.

### [Unregister-PSSessionConfiguration](Unregister-PSSessionConfiguration.md)
Deletes registered session configurations from the computer.

### [Update-Help](Update-Help.md)
Downloads and installs the newest help files on your computer.

### [Wait-Job](Wait-Job.md)
Waits until one or all of the PowerShell jobs running in the session are in a terminating state.

### [Where-Object](Where-Object.md)
Selects objects from a collection based on their property values.
