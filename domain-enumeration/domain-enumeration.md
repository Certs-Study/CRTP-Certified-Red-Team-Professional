---
description: >-
  Domain enumeration is the process of gathering information about a target
  domain, such as user accounts, group memberships, and computer systems, to
  identify potential security vulnerabilities.
cover: ../.gitbook/assets/RFS (2).png
coverY: 0
---

# 2⃣ Domain Enumeration

### Using PowerView

PowerView is a PowerShell-based tool that provides a range of functions for performing domain enumeration tasks.&#x20;

One of its key features is its ability to query the Active Directory (AD) domain for information about user accounts, groups, and computers.

We can download PowerView here: [https://github.com/PowerShellMafia/PowerSploit/tree/master/Recon](https://github.com/PowerShellMafia/PowerSploit/tree/master/Recon)

```powershell
. ./PowerView.ps1
```

### **Get current domain**

The Get-NetDomain function specifically retrieves information about the domain that the current user is logged into or that is specified as a parameter.

{% tabs %}
{% tab title="PowerView" %}
```powershell
Get-NetDomain
```
{% endtab %}

{% tab title="AD Module" %}
Get ADDomain
{% endtab %}

{% tab title="SharpView" %}

{% endtab %}
{% endtabs %}

Here's an overview of some of the information that the Get-NetDomain function can retrieve:

1. **Domain Name:** The name of the domain.
2. **Domain SID:** The security identifier of the domain.
3. **Domain Forest:** The name of the forest that the domain is a part of.
4. **Domain Controllers:** A list of the domain controllers in the domain, including their names, IP addresses, and operating systems.
5. **Domain Policies:** A list of the domain policies that are applied to the domain, including the password policy, account lockout policy, and audit policy.
6. **Domain Trusts:** A list of the trusts that the domain has with other domains, including the trust type, direction, and status.

### **Get the object of another domain**

The "Get-NetDomain" function with the "-Domain" parameter is used to retrieve information about a specific domain in a Windows environment.

{% tabs %}
{% tab title="PowerView" %}
```powershell
Get-NetDomain -Domain example.com
```
{% endtab %}

{% tab title="AD Module" %}

{% endtab %}
{% endtabs %}

This command will retrieve information about the "example.com" domain, including its name, SID, domain controllers, domain policies, and domain trusts.

### **Get Domain SID for the current domain**

The "Get-DomainSID" function is a part of the PowerView tool, which is a PowerShell-based tool that provides a range of functions for performing domain enumeration tasks in Windows environments.

{% tabs %}
{% tab title="PowerView" %}
```powershell
Get-DomainSID
```
{% endtab %}

{% tab title="AD Module" %}

{% endtab %}
{% endtabs %}

The SID is a unique identifier that is assigned to each object in the Windows security database, including domains.&#x20;

It is often used in access control decisions, so having the SID of a domain can be useful for security assessments and penetration testing engagements.

### **Get the domain password policy**

The "Get-DomainPolicy" function specifically retrieves information about the domain policies that are applied to the current domain or the domain specified as a parameter.

{% tabs %}
{% tab title="PowerView" %}
```powershell
Get-DomainPolicy (Get-DomainPolicy)."System Access" net accounts
```
{% endtab %}

{% tab title="AD Module" %}
```
// Some code
```


{% endtab %}
{% endtabs %}

### Get domain SID for the current domain

{% tabs %}
{% tab title="PowerView" %}
Get DomainSID
{% endtab %}

{% tab title="AD Module" %}
( Get ADDomain DomainSID
{% endtab %}
{% endtabs %}
