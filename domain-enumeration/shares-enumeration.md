---
cover: ../.gitbook/assets/RFS (1).png
coverY: 0
---

# 4⃣ Shares  Enumeration

### **Find shared on hosts in the current domain**

```
Invoke-ShareFinder -Verbose
Invoke-ShareFinder -ExcludeStandard -ExcludePrint -ExcludeIPC
```



### **Find sensitive files on computers in the domain**

```
Invoke-FileFinder -Verbose
```



### **Get all fileservers of the domain**

```
Get-NetFileServer
```
