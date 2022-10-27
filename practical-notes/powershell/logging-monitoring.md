# Logging/Monitoring

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
reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\WINEVT\Channels\Microsoft-Windows-Sysmon/Operational
```
