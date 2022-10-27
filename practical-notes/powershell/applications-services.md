# Applications/Services

list the running services using  `net start` to check if there are any interesting running services

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
