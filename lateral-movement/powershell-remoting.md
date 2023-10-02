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
