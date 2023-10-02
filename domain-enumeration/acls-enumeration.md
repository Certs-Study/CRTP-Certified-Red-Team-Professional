---
cover: ../.gitbook/assets/RFS (2).png
coverY: 0
---

# 6⃣ ACLs  Enumeration

### **Get the ACL's associated with the specified object**

```
Get-ObjectACL -SamAccountName <accountname> -ResolveGUIDS
```

### **Get the ACL's associated with the specified prefix to be used for search**

```
Get-ObjectACL -ADSprefix ‘CN=Administrator,CN=Users’ -Verbose
```

### **Get the ACL's associated with the specified path**

```
Get-PathAcl -Path \\<Domain controller>\sysvol
```

### **Search for interesting ACL's**

{% code overflow="wrap" %}
```
Invoke-ACLScanner -ResolveGUIDs
Invoke-ACLScanner -ResolveGUIDs | select IdentityReference, ObjectDN, ActiveDirectoryRights | fl
```
{% endcode %}

### **Search of interesting ACL's for the current user**

{% code overflow="wrap" %}
```
Invoke-ACLScanner | Where-Object {$_.IdentityReference –eq [System.Security.Principal.WindowsIdentity]::GetCurrent().Name}
```
{% endcode %}
