# PowerShell Enumeration

The output of the `systeminfo` provides information about the machine, including the operating system name and version, hostname, and other hardware information as well as the AD domain

```
systeminfo | findstr Domain
```



Enumerate for any/all (\*) users on the martianredteam.com domain

```
Get-ADUser -Filter * -SearchBase "CN=User1,CN=Users,DC=Martianredteam,DC=com"
```



Check if Windows Defender Service is installed

```
Get-Service WinDefend
```



Check if Windows Defender is running RTP

```
Get-MpComputerStatus | select RealTimeProtectionEnabled
```



Check for Host-Based firewall and output result to table

```
Get-NetFirewallProfile | Format-Table Name, Enabled
```



Disable host based Firewall (Admin Privilege)

```shell-session
Set-NetFirewallProfile -Profile Domain, Public, Private -Enabled False
```



Review Host Based Firewall rules

```
Get-NetFirewallRule | select DisplayName, Enabled, Description
```



Test inbound connection on port 80 and whether it is allowed by the firewall

```
 Test-NetConnection -ComputerName 127.0.0.1 -Port 80
```
