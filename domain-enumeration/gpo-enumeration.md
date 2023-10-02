---
cover: ../.gitbook/assets/RFS (1).png
coverY: 0
---

# 5⃣ GPO  Enumeration

### **Get list of GPO's in the current domain**

```
Get-NetGPO
Get-NetGPO -Computername <computername>
```

### **Get GPO's which uses restricteds groups or groups.xml for interesting users**

```
Get-NetGPOGroup
```

### **Get users which are in a local group of a machine using GPO**

```
Find-GPOComputerAdmin -Computername <computername>
```

### **Get machines where the given user is member of a specific group**

```
Find-GPOLocation -Username student244 -Verbose
```

### **Get OU's in a domain**

```
Get-NetOU -Fulldata
```

### **Get machines that are part of an OU**

```
Get-NetOU StudentMachines | %{Get-NetComputer -ADSPath $_}
```

### **Get GPO applied on an OU**

gplink from Get-NetOU -Fulldata

```
Get-NetGPO -GPOname "{<gplink>}"
```
