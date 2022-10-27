# PowerShell

The output of the `systeminfo` provides information about the machine, including the operating system name and version, hostname, and other hardware information as well as the AD domain

```
systeminfo | findstr Domain
```

Enumerate for any/all (\*) users on the martianredteam.com domain

```
Get-ADUser -Filter * -SearchBase "CN=User1,CN=Users,DC=Martianredteam,DC=com"
```
