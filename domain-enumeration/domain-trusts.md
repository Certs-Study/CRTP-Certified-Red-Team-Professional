# 7⃣ Domain Trusts

### **Get a list of all the domain trusts for the current domain**

```
Get-NetDomainTrust
```

### **Get details about the forest**

```
Get-NetForest
```

### **Get all domains in the forest**

```
Get-NetForestDomain
Get-NetforestDomain -Forest <domain name>
```

### **Get global catalogs for the current forest**

```
Get-NetForestCatalog
Get-NetForestCatalog -Forest <domain name>
```

### **Map trusts of a forest**

```
Get-NetForestTrust
Get-NetForestTrust -Forest <domain name>
Get-NetForestDomain -Verbose | Get-NetDomainTrust
```
