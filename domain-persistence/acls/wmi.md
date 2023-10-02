# 3⃣ WMI

### **Import** Set-RemoteWMI

```
. ./Set-RemoteWMI.ps1
```

### **On a local machine**

```
Set-RemoteWMI -Username <username> -Verbose
```

### **On a remote machine without explicit credentials**

```
Set-RemoteWMI -Username <username> -Computername <computername> -namespace ‘root\cimv2’ -Verbose
```

### **On a remote machine with explicit credentials**

Only root/cimv and nested namespaces

```
Set-RemoteWMI -Username <username> -Computername <computername> -Credential Administrator -namespace ‘root\cimv2’ -Verbose
```

### **On remote machine remove permissions**

```
Set-RemoteWMI -Username <username> -Computername <computername> -namespace ‘root\cimv2’ -Remove -Verbose
```

### **Check WMI permissions**

```
Get-wmiobject -Class win32_operatingsystem -ComputerName <computername>
```
