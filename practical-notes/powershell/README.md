# PowerShell

{% tabs %}
{% tab title="Examination" %}


#### Get-Process

| Command                                       | Description                                                 |
| --------------------------------------------- | ----------------------------------------------------------- |
| `Get-Process`                                 | Get brief information about running processes               |
| `Get-Process 'powersh*'`                      | Get brief information about a named process with a wildcard |
| `Get-Process 'powershell' \| Select-Object *` | Detailed information about a running process                |
| `Get-Process -ComputerName MartianPC`         | Information about processes on a remote system              |
|                                               |                                                             |

#### Get-CimInstance

| Command                                                                                     | Description                                                                      |
| ------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| `Get-CimInstance -Class Win32_Process \| Select-Object ProcessId, ProcessName, CommandLine` | Returns an object with Windows process information                               |
| `Get-CimInstance -Class Win32_Process \| Where-Object -Property ParentProcessId -EQ 1337`   | Returns an object with Windows process information where ParentProcessId is 1337 |
|                                                                                             |                                                                                  |

#### Get-NetTCPConnection

| Command                                                                                                | Description                                     |
| ------------------------------------------------------------------------------------------------------ | ----------------------------------------------- |
| `Get-NetTCPConnection`                                                                                 | Displays several network connection information |
| `Get-NetTCPConnection -State Listen`                                                                   | Display listening connections                   |
| `Get-NetTCPConnection -State Listen \| Select-Object -Property LocalAddress, LocalPort, OwningProcess` | Display listening connections by property       |
|                                                                                                        |                                                 |

#### Get-Service

| Command                                          | Description                           |
| ------------------------------------------------ | ------------------------------------- |
| `Get-Service nginx`                              | Get information about running servies |
| `Get-Service nginx \| Select-Object -Property *` | Display the properties of a service   |
|                                                  |                                       |

#### Get-LocalUser and Get-LocalGroup

| Command                                                      | Description                                   |
| ------------------------------------------------------------ | --------------------------------------------- |
| `Get-LocalUser`                                              | List all local users                          |
| `Get-LocalUser Martian`                                      | List user information by username             |
| `Get-LocalUser \| Where-Object -Property Enabled -EQ $true`  | List local users with enabled accounts        |
| `Get-LocalUser \| Where-Object -Property Enabled -EQ $false` | List local users with disabled accounts       |
| `Get-LocalGroup`                                             | List all local groups                         |
| `Get-LocalGroup Administrators`                              | Lists the Administrators group                |
| `Get-LocalGroupMember Administrators`                        | Lists the members of the Administrators Group |

#### Applications/Services

list the running services using `net start` to check if there are any interesting running services

```
net start
```

Look for a service with the name `Martian Demo`

```
wmic service where "name like 'Martian Demo'" get Name,PathName
```

If a process exists, get information about the process

```
Get-Process -Name martian-demo
```

Search if process 3212 is listening for a network service

```
netstat -noa |findstr "LISTENING" |findstr "3212"
```
{% endtab %}

{% tab title="Enumeration" %}


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
{% endtab %}

{% tab title="Logging/Monitoring" %}


Get a list of available event logs on the local machine using the `Get-EventLog` cmdlet

```
Get-EventLog -List
```

Look for a process or service that has been named "Sysmon" within the current process/service

```
Get-Process | Where-Object { $_.ProcessName -eq "Sysmon" }
```

Look for a service that has been named "Sysmon" within the current service

```
Get-CimInstance win32_service -Filter "Description = 'System Monitor service'"
```

Check registry for Sysmon tool

```
reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\WINEVT\Channels\Microsoft-Windows-Sysmon/Operational# Live Examination

Get-Process

| Command                                       | Description                                                 |
| --------------------------------------------- | ----------------------------------------------------------- |
| `Get-Process`                                 | Get brief information about running processes               |
| `Get-Process 'powersh*'`                      | Get brief information about a named process with a wildcard |
| `Get-Process 'powershell' \| Select-Object *` | Detailed information about a running process                |
| `Get-Process -ComputerName MartianPC`         | Information about processes on a remote system              |
|                                               |                                                             |

Get-CimInstance

| Command                                                                                     | Description                                                                      |
| ------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| `Get-CimInstance -Class Win32_Process \| Select-Object ProcessId, ProcessName, CommandLine` | Returns an object with Windows process information                               |
| `Get-CimInstance -Class Win32_Process \| Where-Object  -Property ParentProcessId -EQ 1337`  | Returns an object with Windows process information where ParentProcessId is 1337 |
|                                                                                             |                                                                                  |

Get-NetTCPConnection

| Command                                                                                                | Description                                     |
| ------------------------------------------------------------------------------------------------------ | ----------------------------------------------- |
| `Get-NetTCPConnection`                                                                                 | Displays several network connection information |
| `Get-NetTCPConnection -State Listen`                                                                   | Display listening connections                   |
| `Get-NetTCPConnection -State Listen \| Select-Object -Property LocalAddress, LocalPort, OwningProcess` | Display listening connections by property       |
|                                                                                                        |                                                 |

Get-Service

| Command                                          | Description                           |
| ------------------------------------------------ | ------------------------------------- |
| `Get-Service nginx`                              | Get information about running servies |
| `Get-Service nginx \| Select-Object -Property *` | Display the properties of a service   |
|                                                  |                                       |

Get-LocalUser and Get-LocalGroup

| Command                                                      | Description                                   |
| ------------------------------------------------------------ | --------------------------------------------- |
| `Get-LocalUser`                                              | List all local users                          |
| `Get-LocalUser Martian`                                      | List user information by username             |
| `Get-LocalUser \| Where-Object -Property Enabled -EQ $true`  | List local users with enabled accounts        |
| `Get-LocalUser \| Where-Object -Property Enabled -EQ $false` | List local users with disabled accounts       |
| `Get-LocalGroup`                                             | List all local groups                         |
| `Get-LocalGroup Administrators`                              | Lists the Administrators group                |
| `Get-LocalGroupMember Administrators`                        | Lists the members of the Administrators Group |# Live Examination

Get-Process

| Command                                       | Description                                                 |
| --------------------------------------------- | ----------------------------------------------------------- |
| `Get-Process`                                 | Get brief information about running processes               |
| `Get-Process 'powersh*'`                      | Get brief information about a named process with a wildcard |
| `Get-Process 'powershell' \| Select-Object *` | Detailed information about a running process                |
| `Get-Process -ComputerName MartianPC`         | Information about processes on a remote system              |
|                                               |                                                             |

Get-CimInstance

| Command                                                                                     | Description                                                                      |
| ------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| `Get-CimInstance -Class Win32_Process \| Select-Object ProcessId, ProcessName, CommandLine` | Returns an object with Windows process information                               |
| `Get-CimInstance -Class Win32_Process \| Where-Object  -Property ParentProcessId -EQ 1337`  | Returns an object with Windows process information where ParentProcessId is 1337 |
|                                                                                             |                                                                                  |

Get-NetTCPConnection

| Command                                                                                                | Description                                     |
| ------------------------------------------------------------------------------------------------------ | ----------------------------------------------- |
| `Get-NetTCPConnection`                                                                                 | Displays several network connection information |
| `Get-NetTCPConnection -State Listen`                                                                   | Display listening connections                   |
| `Get-NetTCPConnection -State Listen \| Select-Object -Property LocalAddress, LocalPort, OwningProcess` | Display listening connections by property       |
|                                                                                                        |                                                 |

Get-Service

| Command                                          | Description                           |
| ------------------------------------------------ | ------------------------------------- |
| `Get-Service nginx`                              | Get information about running servies |
| `Get-Service nginx \| Select-Object -Property *` | Display the properties of a service   |
|                                                  |                                       |

Get-LocalUser and Get-LocalGroup

| Command                                                      | Description                                   |
| ------------------------------------------------------------ | --------------------------------------------- |
| `Get-LocalUser`                                              | List all local users                          |
| `Get-LocalUser Martian`                                      | List user information by username             |
| `Get-LocalUser \| Where-Object -Property Enabled -EQ $true`  | List local users with enabled accounts        |
| `Get-LocalUser \| Where-Object -Property Enabled -EQ $false` | List local users with disabled accounts       |
| `Get-LocalGroup`                                             | List all local groups                         |
| `Get-LocalGroup Administrators`                              | Lists the Administrators group                |
| `Get-LocalGroupMember Administrators`                        | Lists the members of the Administrators Group |# Live Examination

Get-Process

| Command                                       | Description                                                 |
| --------------------------------------------- | ----------------------------------------------------------- |
| `Get-Process`                                 | Get brief information about running processes               |
| `Get-Process 'powersh*'`                      | Get brief information about a named process with a wildcard |
| `Get-Process 'powershell' \| Select-Object *` | Detailed information about a running process                |
| `Get-Process -ComputerName MartianPC`         | Information about processes on a remote system              |
|                                               |                                                             |

Get-CimInstance

| Command                                                                                     | Description                                                                      |
| ------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| `Get-CimInstance -Class Win32_Process \| Select-Object ProcessId, ProcessName, CommandLine` | Returns an object with Windows process information                               |
| `Get-CimInstance -Class Win32_Process \| Where-Object  -Property ParentProcessId -EQ 1337`  | Returns an object with Windows process information where ParentProcessId is 1337 |
|                                                                                             |                                                                                  |

Get-NetTCPConnection

| Command                                                                                                | Description                                     |
| ------------------------------------------------------------------------------------------------------ | ----------------------------------------------- |
| `Get-NetTCPConnection`                                                                                 | Displays several network connection information |
| `Get-NetTCPConnection -State Listen`                                                                   | Display listening connections                   |
| `Get-NetTCPConnection -State Listen \| Select-Object -Property LocalAddress, LocalPort, OwningProcess` | Display listening connections by property       |
|                                                                                                        |                                                 |

Get-Service

| Command                                          | Description                           |
| ------------------------------------------------ | ------------------------------------- |
| `Get-Service nginx`                              | Get information about running servies |
| `Get-Service nginx \| Select-Object -Property *` | Display the properties of a service   |
|                                                  |                                       |

Get-LocalUser and Get-LocalGroup

| Command                                                      | Description                                   |
| ------------------------------------------------------------ | --------------------------------------------- |
| `Get-LocalUser`                                              | List all local users                          |
| `Get-LocalUser Martian`                                      | List user information by username             |
| `Get-LocalUser \| Where-Object -Property Enabled -EQ $true`  | List local users with enabled accounts        |
| `Get-LocalUser \| Where-Object -Property Enabled -EQ $false` | List local users with disabled accounts       |
| `Get-LocalGroup`                                             | List all local groups                         |
| `Get-LocalGroup Administrators`                              | Lists the Administrators group                |
| `Get-LocalGroupMember Administrators`                        | Lists the members of the Administrators Group |
```
{% endtab %}
{% endtabs %}
