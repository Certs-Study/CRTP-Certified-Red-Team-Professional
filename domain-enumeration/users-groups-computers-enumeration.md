---
cover: ../.gitbook/assets/RFS (2).png
coverY: 0
---

# 3⃣ Users, Groups, Computers  Enumeration

### **Get Information of domain controller**

```
Get-NetDomainController
Get-NetDomainController | select-object Name
```

### **Get information on users in the domain**

```
Get-NetUser
Get-NetUser -Username <username>
```

### **Get the list of all users**

```
Get-NetUser | select samaccountname
```

### **Get the list of usernames, last logon, and password last set**

```
Get-NetUser | select samaccountname, lastlogon, pwdlastset
Get-NetUser | select samaccountname, lastlogon, pwdlastset | Sort-Object -Property lastlogon
```

### **Get the list of usernames and their groups**

```
Get-NetUser | select samaccountname, memberof
```

### **Get the list of all properties for users in the current domain**

```
get-userproperty -Properties pwdlastset
```

### **Get description field from the user**

```
Find-UserField -SearchField Description -SearchTerm "built"
Get-netuser | Select-Object samaccountname,description
```

### **Get computer information**

```
Get-NetComputer
Get-NetComputer -FullData
Get-NetComputer -Computername <computername> -FullData
```

### **Get computers with operating system ""**

```
Get-NetComputer -OperatingSystem "*Server 2016*"
```

### **Get the list of all computer names and operating systems**

{% code overflow="wrap" %}
```
Get-NetComputer -fulldata | select samaccountname, operatingsystem, operatingsystemversion
```
{% endcode %}

### **List all groups of the domain**

```
Get-NetGroup
Get-NetGroup -GroupName *admin*
Get-NetGroup -Domain <domain>
```

### **Get all the members of the group**

```
Get-NetGroupMember -Groupname "Domain Admins" -Recurse
Get-NetGroupMember -Groupname "Domain Admins" -Recurse | select MemberName
```

### **Get the group membership of a user**

```
Get-NetGroup -Username <username>
```

### **List all the local groups on a machine (needs admin privs on non dc machines)**

```
Get-NetlocalGroup -Computername <computername> -ListGroups
```

### **Get a Member of all the local groups on a machine (needs admin privs on non dc machines)**

```
Get-NetlocalGroup -Computername <computername> -Recurse
```

### **Get actively logged users on a computer (needs local admin privs)**

```
Get-NetLoggedon -Computername <computername>
```

### **Get locally logged users on a computer (needs remote registry rights on the target)**

```
Get-LoggedonLocal -Computername <computername>
```

### **Get the last logged users on a computer (needs admin rights and remote registry on the target)**

```
Get-LastLoggedOn -ComputerName <computername>
```
