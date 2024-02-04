---
description: >-
  You can run commands on one or hundreds of computers with a single PowerShell
  command. Windows PowerShell supports remote computing by using various
  technologies, including WMI, RPC, and WS-Management
---

# PowerShell Remoting

{% embed url="https://learn.microsoft.com/en-us/powershell/scripting/learn/remoting/running-remote-commands?view=powershell-7.3" %}

{% embed url="https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/?view=powershell-7.3" %}

### Verify if we can execute remote commands:

> The `Invoke-Command` cmdlet runs commands on a local or remote computer and returns all output from the commands, including errors. Using a single `Invoke-Command` command, you can run commands on multiple computers.

```powershell
Invoke-Command -ScriptBlock {whoami;hostname} -ComputerName dcorp-mgmt
```

```powershell
$sess = New-PSSession -ComputerName dcorp-mgmt.dollarcorp.moneycorp.local
```

{% code overflow="wrap" %}
```powershell
Invoke-command -ScriptBlock{Set-MpPreference -DisableIOAVProtection $true} -Session $sess
```
{% endcode %}

```powershell
Invoke-command -ScriptBlock ${function:Invoke-Mimi} -Session $sess
```

#### Run a script on a server: <a href="#example-1-run-a-script-on-a-server" id="example-1-run-a-script-on-a-server"></a>

```powershell
Invoke-Command -FilePath c:\scripts\rfs.ps1 -ComputerName Server01
```

#### Run a single command on several computers <a href="#example-6-run-a-single-command-on-several-computers" id="example-6-run-a-single-command-on-several-computers"></a>

```powershell
$parameters = @{
  ComputerName      = 'Server01', 'Server02', 'TST-0143', 'localhost'
  ConfigurationName = 'MySession.PowerShell'
  ScriptBlock       = { Get-WinEvent -LogName PowerShellCore/Operational }
}
Invoke-Command @parameters
```

#### Explanation of PowerShell Commands

**Executing Remote Commands with `Invoke-Command`**

The `Invoke-Command` cmdlet in PowerShell is a versatile command used to execute scripts and commands on both local and remote systems. Here is how it works:

1.  To run commands on a single remote computer, you use `Invoke-Command` with the `-ComputerName` parameter:

    ```powershell
    Invoke-Command -ScriptBlock {whoami; hostname} -ComputerName dcorp-mgmt
    ```

    This will execute the `whoami` and `hostname` commands on the remote computer named `dcorp-mgmt`.
2.  For establishing a persistent connection to a remote computer, you can create a PowerShell session (PSSession):

    ```powershell
    $sess = New-PSSession -ComputerName dcorp-mgmt.dollarcorp.moneycorp.local
    ```

    The variable `$sess` stores the PSSession for the target computer `dcorp-mgmt.dollarcorp.moneycorp.local`.
3.  You can then run commands in that session using `Invoke-Command`:

    ```powershell
    Invoke-command -ScriptBlock {Set-MpPreference -DisableIOAVProtection $true} -Session $sess
    ```

    This command modifies the antivirus preferences on the remote computer, utilizing the previously established session `$sess`.
4.  To invoke custom functions or scripts that are defined locally on your computer on a remote session, you wrap the function name within `${function:FunctionName}`:

    ```powershell
    Invoke-command -ScriptBlock ${function:Invoke-Mimi} -Session $sess
    ```

    Here, `Invoke-Mimi` is presumably a custom or imported function that is being called remotely via `$sess`.

**Running a Script on a Remote Server**

*   To execute a local script on a remote machine using `Invoke-Command`, the `-FilePath` parameter can be used along with the `-ComputerName`:

    ```powershell
    Invoke-Command -FilePath c:\scripts\rfs.ps1 -ComputerName Server01
    ```

    This runs the script `rfs.ps1` that is located at `c:\scripts` on `Server01`.

**Running Commands on Multiple**
