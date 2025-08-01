---
external help file: Microsoft.PowerShell.Commands.Utility.dll-Help.xml
Locale: en-US
Module Name: Microsoft.PowerShell.Utility
ms.date: 06/09/2017
online version: https://learn.microsoft.com/previous-versions/powershell/module/Microsoft.PowerShell.Utility/invoke-expression?view=powershell-5.0&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Invoke-Expression
---
# Invoke-Expression

## SYNOPSIS
Runs commands or expressions on the local computer.

## SYNTAX

```
Invoke-Expression [-Command] <String> [<CommonParameters>]
```

## DESCRIPTION

The **Invoke-Expression** cmdlet evaluates or runs a specified string as a command and returns the results of the expression or command.
Without **Invoke-Expression**, a string submitted at the command line would be returned (echoed) unchanged.

## EXAMPLES

### Example 1: Evaluate an expression

```
PS C:\> $Command = "Get-Process"
PS C:\> $Command
Get-Process
PS C:\> Invoke-Expression $Command
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id   ProcessName
-------  ------    -----      ----- -----   ------     --   -----------
296       4       1572       1956    20       0.53     1348   AdtAgent
270       6       1328       800     34       0.06     2396   alg
67        2       620        484     20       0.22     716    ati2evxx
1060      15      12904      11840   74       11.48    892    CcmExec
1400      33      25280      37544   223      38.44    2564   communicator
...
```

This example demonstrates the use of **Invoke-Expression** to evaluate an expression.
Without **Invoke-Expression**, the expression is printed, but not evaluated.

The first command assigns a value of Get-Process (a string) to the $Command variable.

The second command shows the effect of typing the variable name at the command line.
Windows PowerShell echoes the string.

The third command uses **Invoke-Expression** to evaluate the string.

### Example 2: Run a script on the local computer

```
PS C:\> Invoke-Expression -Command "C:\ps-test\testscript.ps1"
PS C:\> "C:\ps-test\testscript.ps1" | Invoke-Expression
```

These commands use **Invoke-Expression** to run a script, TestScript.ps1, on the local computer.
The two commands are equivalent.
The first uses the *Command* parameter to specify the command to run.
The second uses a pipeline operator (|) to send the command string to **Invoke-Expression**.

### Example 3: Run a command in a variable

```
PS C:\> $Command = 'Get-Process | where {$_.cpu -gt 1000}'
PS C:\> Invoke-Expression $Command
```

This example runs a command string that is saved in the $Command variable.

The command string is enclosed in single quotation marks because it includes a variable, `$_`, which represents the current object.
If it were enclosed in double quotation marks, the `$_` variable would be replaced by its value before it was saved in the $Command variable.

### Example 4: Get and run a cmdlet Help example

```
PS C:\> $Cmdlet_name = "Get-EventLog"
PS C:\> $Example_number = 1
PS C:\> $Example_code = (Get-Help $Cmdlet_name).examples.example[($Example_number-1)].code
PS C:\> Invoke-Expression $Example_code
```

This command retrieves and runs the first example in the Get-EventLog cmdlet Help topic.

To run an example of a different cmdlet, change the value of the $Cmdlet_name variable to the name of the cmdlet.
And, change the $Example_number variable to the example number you want to run.
The command will fail if the example number is not valid.

## PARAMETERS

### -Command

Specifies the command or expression to run.
Type the command or expression or enter a variable that contains the command or expression.
The *Command* parameter is required.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### System.String or PSObject

You can pipe an object that represents the command to **Invoke-Expression**.
Use the $Input automatic variable to represent the input objects in the command.

## OUTPUTS

### PSObject

Returns the output that is generated by the invoked command (the value of the *Command* parameter).

## NOTES

* An expression is a statement that can be evaluated and produces a result, such as a Windows PowerShell command.
* Take reasonable precautions when using the **Invoke-Expression** cmdlet in scripts. When using **Invoke-Expression** to run a command that the user enters, verify that the command is safe to run before running it. In general, it is best to design your script with predefined input options, rather than allowing freeform input.

*

## RELATED LINKS

[Invoke-Command](../Microsoft.PowerShell.Core/Invoke-Command.md)

[Where-Object](../Microsoft.PowerShell.Core/Where-Object.md)


