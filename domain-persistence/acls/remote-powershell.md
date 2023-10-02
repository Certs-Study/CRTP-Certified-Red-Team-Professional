# 4⃣ Remote Powershell

```
. ./Set-RemotePSRemoting.ps1
```



**On a local machine**

```
Set-RemotePSRemoting -Username <username> -Verbose
```



**On a remote machine without credentials**

```
Set-RemotePSRemoting -Username <username> -Computername <computername> -Verbose
```



**On a remote machine remove permissions**

```
Set-RemotePSRemoting -Username <username> -Computername <computername> -Remove
```
