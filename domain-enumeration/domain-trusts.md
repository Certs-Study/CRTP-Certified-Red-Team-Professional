---
description: >-
  Explore our comprehensive article on Domain Trusts, an essential aspect in
  network security.
---

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

#### Check domain trust for a specific domain

```
Get-NetDomainTrust -Domain <specific domain name>
```

#### Get the forest trust status

```
Get-NetForestTrustStatus
Get-NetForestTrustStatus -Forest <domain name>
```

#### Retrieve Domain Controllers for a specific domain

```
Get-NetDomainController
Get-NetDomainController -DomainName <specific domain name>
```

#### Enumerate Organization Units (OUs) in a domain

```
Get-NetOU -Domain <domain name>
Get-NetOU -Domain <domain name> -FullData
```
