# Application Testing

## CLI tools

{% tabs %}
{% tab title="cURL" %}
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
|                                                                                                                    |                                                      |
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
| `ffuf -w ./folders.txt:FOLDERS,./wordlist.txt:WORDLIST,./extensions.txt:EXTENSIONS -u http://www.target.domain/FOLDERS/WORDLISTEXTENSIONS`                      | Mutated bruteforcing against the target web server.                           |
{% endtab %}

{% tab title="Nmap" %}
## Nmap

Scan a port with Nmap via proxy with the `-Pn` flag to skip host discovery and scripts

```shell-session
nmap --proxies http://127.0.0.1:8080 SERVER_IP -pPORT -Pn -sC
```
{% endtab %}

{% tab title="Git" %}
## Git

**How to commit changes from local machine**

| Command                                                                                                                    | Description                                                                                                                       |
| -------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| `git clone`                                                                                                                | Authenticate and Clone repository that needs to managed                                                                           |
| `git add *`                                                                                                                | Find any files that have changed                                                                                                  |
| `git commit –m "message to the team/users"`                                                                                | Commit changes with a message for what changes were made                                                                          |
| `git push origin master`                                                                                                   | Push changes to master branch                                                                                                     |
| `git pull`                                                                                                                 | Pull changes for merging/updates                                                                                                  |
| `git checkout -b testfile.version-number`                                                                                  | <p>Make changes isolated from the master production branch.<br><br>The -b signifies creating a new branch that doesn't exist.</p> |
| `git push origin --delete testfile.version-number`                                                                         | Delete the testing file/branch after changes                                                                                      |
| <p><code>ls; git log</code><br><code>git checkout [commitid]</code><br><code>git revert</code><br><code>git log</code></p> | Revert changes made by checking out the commit via commit id with log command                                                     |
| `git reset --hard origin/master`                                                                                           | Hard Reset after making local changes but the git commit is unwanted or has errors on the local machine                           |
| <p><code>git clean -nxd</code><br><br><code>git clean -fxd</code></p>                                                      | Clean directories that were made during changes                                                                                   |
{% endtab %}
{% endtabs %}

## API Security/Testing

{% tabs %}
{% tab title="Training" %}
#### **crAPI Lab Setup**

* [ ] `mkdir /apilab`
* [ ] `cd /apilab`
* [ ] `sudo curl -o docker-compose.yml https://raw.githubusercontent.com/OWASP/crAPI/main/deploy/docker/docker-compose.yml`
* [ ] `sudo docker-compose pull`
* [ ] `sudo docker-compose -f docker-compose.yml --compatibility up -d`

crAPI Landing page will be located at http://127.0.0.1:8888 with the crAPI Mailhog Server at http://127.0.0.1:8025

****

#### **vAPI lab setup**

* [ ] `mkdir /apilab`
* [ ] `cd /apilab`
* [ ] `sudo git clone https://github.com/roottusk/vapi.git`
* [ ] `cd /vapi`
* [ ] `sudo docker-compose up -d`
{% endtab %}

{% tab title="Checklist" %}
## API Testing Checklist

**Passive Reconnaissance**

* [ ] Google Dorking to reveal specific information about the API
* [ ] Git Dorking: `authorization: Bearer` , `filename: swagger.json`
* [ ] Shodan Search: `"content-type: application/json"`, `"wp-json"`
* [ ] Wayback Machine snapshots

**Active Reconnaissance**

* [ ] Amass: `amass enum -active -d dns.com | grep api`
  * [ ] `amass enum -active -brute -w /usr/share/wordlists/API_superlist -d example.com -dir [directory name]`
* [ ] Testing Directories: `gobuster dir -u http://10.x.x.x -w /location/to/wordlist.txt`
* [ ] `Check for API calls in Devtools > network Tab or Web App Proxy`
* [ ] Import curl request to Postman

**Endpoint Analysis**

* [ ] Proxy all traffic to Postman/Burp and capture requests for history
* [ ] Perform the actions that can be performed within application; this can be filtered in Postman

OR

* [ ] Import api doc files as new collections

API Documentation Conventions

| Convention | Example                                                                                                                      | Meaning                                                                                                                                                                                                                  |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| : or {}    | <p>/user/:id</p><p>/user/{id}</p><p>/user/1337</p><p>/account/:username</p><p>/account/{username}</p><p>/account/mart1an</p> | The colon or curly brackets are used by some APIs to indicate a path variable. In other words, “:id” represents the variable for an ID number and “{username}” represents the account username you are trying to access. |
| \[]        | /api/v1/user?find=\[name]                                                                                                    | Square brackets indicate that the input is optional.                                                                                                                                                                     |
| \|\|       | “blue” \|\| “green” \|\| “red”                                                                                               | Double bars represent different possible values that can be used.                                                                                                                                                        |

* [ ] Set parameters to variable in Postman

**Testing**

* [ ] To change versions: `api/v3/login` → `api/v1/login`
* [ ] Check other AuthN endpoints: `/api/mobile/login` → `/api/v3/login` `/api/magic_link`
* [ ] Verb Tampering: `GET /api/trips/1` → `POST /api/trips/1` `POST /api/trips` `DELETE /api/trips/1`
* [ ] Try Object IDs in HTTP headers and bodies, URLs tend to be less vulnerable.
* [ ] Try Numeric IDs when facing a GUID/UUID: `GET /api/users/6b95d962-df38` → `GET /api/users/1`
* [ ] Wrap ID with an array: `{"id":111}` → `{"id":[111]}`
* [ ] Wrap ID with a JSON object: `{"id":111}` → `{"id":{"id":111}}`
* [ ] HTTP Parameter Pollution: `/api/profile?user_id=legit&user_id=victim` `/api/profile?user_id=victim&user_id=legit`
* [ ] JSON Parameter Pollution: `{"user_id":legit,"user_id":victim}` `{"user_id":victim,"user_id":legit}`
* [ ] Wildcard instead of ID: `/api/users/1` → `/api/users/*` `/api/users/%` `/api/users/_` `/api/users/.`
* [ ] Ruby application HTTP parameter containing a URL → Pipe as the first character and then a shell command.
* [ ] Developer APIs differs with mobile and web APIs. Test them separately.
* [ ] Change Content-Type to `application/xml` and see if the API parse it.
* [ ] Non-Production environments tend to be less secure (staging/qa/etc.) Leverage this fact to bypass AuthZ, AuthN, rate limiting & input validation.
* [ ] Export Injection if you see `Convert to PDF` feature.
* [ ] Expand your attack surface and test old versions of [APKs](https://apkpure.com/) IPAs.

Additional checks:

**Check different `Content-Types`**

```
x-www-form-urlencoded --> user=test
application/json --> {"user": "test"}
application/xml --> <user>test</user>**
```

If it's regular POST data try sending arrays, dictionaries

```
username[]=John
username[$neq]=lalala**
```

If JSON is supported try to send unexpected data types

```
{"username": "John"}
{"username": true}
{"username": null}
{"username": 1}
{"username": [true]}
{"username": ["John", true]}
{"username": {"$neq": "lalala"}}**
```

If XML is supported, check for XXE
{% endtab %}
{% endtabs %}

