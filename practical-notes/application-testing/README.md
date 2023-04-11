# Application Security Testing

##

## Assessments

{% tabs %}
{% tab title="Web" %}
## WEB APPLICATION PENTESTING CHECKLIST

**Inspired by OWASP Based Checklist from** [Hariprasaanth](https://github.com/Hari-prasaanth/Web-App-Pentest-Checklist) whom also has one on [Notion](https://hariprasaanth.notion.site/WEB-APPLICATION-PENTESTING-CHECKLIST-0f02d8074b9d4af7b12b8da2d46ac998)



This list was developed to include additional useful details and techniques for modern application assessments (Always in-progress)\
&#x20;

Scope configuration:

Nongreedy match `.*?website.com$`



#### **INFORMATION GATHERING**

**Open Source Reconnaissance -** [**WSTG-INFO-01**](https://owasp.org/www-project-web-security-testing-guide/stable/4-Web\_Application\_Security\_Testing/01-Information\_Gathering/01-Conduct\_Search\_Engine\_Discovery\_Reconnaissance\_for\_Information\_Leakage)

* [ ] Perform Google Dorks search
  * [ ] Effective dorks in the [GHDB](https://www.exploit-db.com/google-hacking-database)
* [ ] Perform OSINT for as  much public information as possible from online resources
  * [ ] [Investigator](https://abhijithb200.github.io/investigator/)

**Fingerprinting Web Server -**  [**WSTG-INFO-02**](https://owasp.org/www-project-web-security-testing-guide/stable/4-Web\_Application\_Security\_Testing/01-Information\_Gathering/02-Fingerprint\_Web\_Server)

* [ ] Find the type of Web Server
* [ ] Find the version details of the Web Server
  * [ ] View Wappylyzer, Whatruns, Server Reponses

**Looking For Metafiles -** [**WSTG-INFO-03**](https://owasp.org/www-project-web-security-testing-guide/stable/4-Web\_Application\_Security\_Testing/01-Information\_Gathering/03-Review\_Webserver\_Metafiles\_for\_Information\_Leakage)

* [ ] View the Robots.txt file
* [ ] View the Sitemap.xml file
* [ ] View the Humans.txt file
* [ ] View the Security.txt file

**Enumerating Web Server’s Applications -** [**WSTG-INFO-04**](https://owasp.org/www-project-web-security-testing-guide/stable/4-Web\_Application\_Security\_Testing/01-Information\_Gathering/04-Enumerate\_Applications\_on\_Webserver)

*
* [ ] Enumerating with Nmap
* [ ] Enumerating with Netcat
* [ ] Perform a DNS lookup
* [ ] Perform a Reverse DNS lookup

**Review The Web Contents -** [**WSTG-INFO-05**](https://owasp.org/www-project-web-security-testing-guide/stable/4-Web\_Application\_Security\_Testing/01-Information\_Gathering/05-Review\_Webpage\_Content\_for\_Information\_Leakage)

* [ ] Inspect the page source for sensitive info
* [ ] Try to find Sensitive Javascript codes
* [ ] Try to find any keys
* [ ] Make sure the autocomplete is disabled

**Identifying Application’s Entry Points -** [**WSTG-INFO-06**](https://owasp.org/www-project-web-security-testing-guide/stable/4-Web\_Application\_Security\_Testing/01-Information\_Gathering/06-Identify\_Application\_Entry\_Points)

* [ ] Identify what the methods used are?
* [ ] Identify where the methods used are?
* [ ] Identify the Injection point

**Mapping Execution Paths -** [**WSTG-INFO-07**](https://owasp.org/www-project-web-security-testing-guide/stable/4-Web\_Application\_Security\_Testing/01-Information\_Gathering/07-Map\_Execution\_Paths\_Through\_Application)

* [ ] Use Burp Suite
* [ ] Use Dirsearch
* [ ] Use Gobuster
* [ ] Use Feroxbuster
  * [ ] `feroxbuster -H "User-Agent: PENTEST" -w fzf-wordlists -u http://site/`
  * [ ] `feroxbuster -H "User-Agent: PENTEST" -w $WORDLIST -u SITE -t $THREADS`

**Fingerprint Web Application Framework -** [**WSTG-INFO-08**](https://owasp.org/www-project-web-security-testing-guide/stable/4-Web\_Application\_Security\_Testing/01-Information\_Gathering/08-Fingerprint\_Web\_Application\_Framework)**,**[ **WSTG-INFO-09** ](https://owasp.org/www-project-web-security-testing-guide/stable/4-Web\_Application\_Security\_Testing/01-Information\_Gathering/09-Fingerprint\_Web\_Application)**(Merged)**

* [ ] Use the Wappalyzer browser extension
* [ ] Use Whatweb
* [ ] View URL extensions
* [ ] View HTML source code
* [ ] View the cookie parameter
* [ ] View the HTTP headers

**Map Application Architecture -** [**WSTG-INFO-10**](https://owasp.org/www-project-web-security-testing-guide/stable/4-Web\_Application\_Security\_Testing/01-Information\_Gathering/10-Map\_Application\_Architecture)

* [ ] Map the overall site structure

**CONFIGURATION & DEPLOYMENT MANAGEMENT TESTING**

**Test Network Configuration**

* [ ] Check the network configuration
* [ ] Check for default settings
* [ ] Check for default credentials

**Test Application Configuration**

* [ ] Ensure only required modules are used
* [ ] Ensure unwanted modules are disabled
* [ ] Ensure the server can handle DOS
* [ ] Check how the application is handling 4xx & 5xx errors
* [ ] Check for the privilege required to run
* [ ] Check logs for sensitive info

**Test File Extension Handling**

* [ ] Ensure the server won’t return sensitive extensions
* [ ] Ensure the server won’t accept malicious extensions
* [ ] Test for file upload vulnerabilities

**Review Backup & Unreferenced Files**

* [ ] Ensure unreferenced files don’t contain any sensitive info
* [ ] Ensure the namings of old and new backup files
* [ ] Check the functionality of unreferenced pages

**Enumerate Infrastructure & Admin Interfaces**

* [ ] Try to find the Infrastructure Interface
* [ ] Try to find the Admin Interface
* [ ] Identify the hidden admin functionalities

**Testing HTTP Methods**

* [ ] Discover the supported methods
* [ ] Ensure the PUT method is disabled
* [ ] Ensure the OPTIONS method is disabled
* [ ] Test access control bypass
* [ ] Test for XST attacks
* [ ] Test for HTTP method overriding

**Test HSTS**

* [ ] Ensure HSTS is enabled

**Test RIA Cross Domain Policy**

* [ ] Check for Adobe’s Cross Domain Policy
* [ ] Ensure it has the least privilege

**Test File Permission**

* [ ] Ensure the permissions for sensitive files
* [ ] Test for directory enumeration

**Test For Subdomain Takeover**

* [ ] Test DNS, A, and CNAME records for subdomain takeover
* [ ] Test NS records for subdomain takeover
* [ ] Test 404 response for subdomain takeover

**Test Cloud Storage**

* [ ] Check the sensitive paths of AWS
* [ ] Check the sensitive paths of Google Cloud
* [ ] Check the sensitive paths of Azure

#### **IDENTITY MANAGEMENT TESTING**

**Test Role Definitions**

* [ ] Test for forced browsing
* [ ] Test for IDOR (Insecure Direct Object Reference)
* [ ] Test for parameter tampering
* [ ] Ensure low privilege users can’t able to access high privilege resources

**Test User Registration Process**

* [ ] Ensure the same user or identity can’t register again and again
* [ ] Ensure the registrations are verified
* [ ] Ensure disposable email addresses are rejected
* [ ] Check what proof is required for successful registration

**Test Account Provisioning Process**

* [ ] Check the verification for the provisioning process
* [ ] Check the verification for the de-provisioning process
* [ ] Check the provisioning rights for an admin user to other users
* [ ] Check whether a user is able to de-provision themself or not?
* [ ] Check for the resources of a de-provisioned user

**Testing For Account Enumeration**

* [ ] Check the response when a valid username and password entered
* [ ] Check the response when a valid username and an invalid password entered
* [ ] Check the response when an invalid username and password entered
* [ ] Ensure the rate-limiting functionality is enabled in username and password fields

**Test For Weak Username Policy**

* [ ] Check the response for both valid and invalid usernames
* [ ] Check for username enumeration

#### **AUTHENTICATION TESTING**

**Test For Un-Encrypted Channel**

* [ ] Check for the HTTP login page
* [ ] Check for the HTTP register or sign-in page
* [ ] Check for HTTP forgot password page
* [ ] Check for HTTP change password
* [ ] Check for resources on HTTP after logout
* [ ] Test for forced browsing to HTTP pages

**Test For Default Credentials**

* [ ] Test with default credentials
* [ ] Test organization name as credentials
* [ ] Test for response manipulation
* [ ] Test for the default username and a blank password
* [ ] Review the page source for credentials

**Test For Weak Lockout Mechanism**

* [ ] Ensure the account has been locked after 3-5 incorrect attempts
* [ ] Ensure the system accepts only the valid CAPTCHA
* [ ] Ensure the system rejects the invalid CAPTCHA
* [ ] Ensure CAPTCHA code regenerated after reloaded
* [ ] Ensure CAPTCHA reloads after entering the wrong code
* [ ] Ensure the user has a recovery option for a lockout account

**Test For Bypassing Authentication Schema**

* [ ] Test forced browsing directly to the internal dashboard without login
* [ ] Test for session ID prediction
* [ ] Test for authentication parameter tampering
* [ ] Test for SQL injection on the login page
* [ ] Test to gain access with the help of session ID
* [ ] Test multiple logins allowed or not?

**Test For Vulnerable Remember Password**

* [ ] Ensure that the stored password is encrypted
* [ ] Ensure that the stored password is on the server-side

**Test For Browser Cache Weakness**

* [ ] Ensure proper cache-control is set on sensitive pages
* [ ] Ensure no sensitive data is stored in the browser cache storage

**Test For Weak Password Policy**

* [ ] Ensure the password policy is set to strong
* [ ] Check for password reusability
* [ ] Check the user is prevented to use his username as a password
* [ ] Check for the usage of common weak passwords
* [ ] Check the minimum password length to be set
* [ ] Check the maximum password length to be set

**Testing For Weak Security Questions**

* [ ] Check for the complexity of the questions
* [ ] Check for brute-forcing

**Test For Weak Password Reset Function**

* [ ] Check what information is required to reset the password
* [ ] Check for password reset function with HTTP
* [ ] Test the randomness of the password reset tokens
* [ ] Test the uniqueness of the password reset tokens
* [ ] Test for rate limiting on password reset tokens
* [ ] Ensure the token must expire after being used
* [ ] Ensure the token must expire after not being used for a long time

**Test For Weak Password Change Function**

* [ ] Check if the old password asked to make a change
* [ ] Check for the uniqueness of the forgotten password
* [ ] Check for blank password change
* [ ] Check for password change function with HTTP
* [ ] Ensure the old password is not displayed after changed
* [ ] Ensure the other sessions got destroyed after the password change

**Test For Weak Authentication In Alternative Channel**

* [ ] Test authentication on the desktop browsers
* [ ] Test authentication on the mobile browsers
* [ ] Test authentication in a different country
* [ ] Test authentication in a different language
* [ ] Test authentication on desktop applications
* [ ] Test authentication on mobile applications

#### **AUTHORIZATION TESTING**

**Testing Directory Traversal File Include**

* [ ] Identify the injection point on the URL
* [ ] Test for Local File Inclusion
* [ ] Test for Remote File Inclusion
* [ ] Test Traversal on the URL parameter
* [ ] Test Traversal on the cookie parameter

**Testing Traversal With Encoding**

* [ ] Test Traversal with Base64 encoding
* [ ] Test Traversal with URL encoding
* [ ] Test Traversal with ASCII encoding
* [ ] Test Traversal with HTML encoding
* [ ] Test Traversal with Hex encoding
* [ ] Test Traversal with Binary encoding
* [ ] Test Traversal with Octal encoding
* [ ] Test Traversal with Gzip encoding

**Testing Travesal With Different OS Schemes**

* [ ] Test Traversal with Unix schemes
* [ ] Test Traversal with Windows schemes
* [ ] Test Traversal with Mac schemes

**Test Other Encoding Techniques**

* [ ] Test Traversal with Double encoding
* [ ] Test Traversal with all characters encode
* [ ] Test Traversal with only special characters encode

**Test Authorization Schema Bypass**

* [ ] Test for Horizontal authorization schema bypass
* [ ] Test for Vertical authorization schema bypass
* [ ] Test override the target with custom headers

**Test For Privilege Escalation**



* [ ] Identify the injection point
* [ ] Test for bypassing the security measures
* [ ] Test for forced browsing
*   [ ] Test for IDOR

    IDOR testing Automation Steps for Burp Pro Users

    * [ ] Download Standalone Jython Jar file from [https://www.jython.org/](https://www.jython.org/) and store
    * [ ] Start Burp Pro
    * [ ] Install Autorize from the Burp App (BApp) Store
    * [ ] Capture login request and copy cookie
    * [ ] Paste cookie into Autorize Configuration
      * [ ] Note: Instead of pasting you can also select "Copy cookie from last request"
    * [ ] Turn Autorize on and refresh page or walk the application for auth testing
    * [ ] Monitor and verify findings (subject to false positives)
* [ ] Test for parameter tampering to high privileged user

**Test For Insecure Direct Object Reference**

* [ ] Test to change the ID parameter
* [ ] Test to add parameters at the endpoints
* [ ] Test for HTTP parameter pollution
* [ ] Test by adding an extension at the end
* [ ] Test with outdated API versions
* [ ] Test by wrapping the ID with an array
* [ ] Test by wrapping the ID with a JSON object
* [ ] Test for JSON parameter pollution
* [ ] Test by changing the case
* [ ] Test for path traversal
* [ ] Test by changing words
* [ ] Test by changing methods

#### **SESSION MANAGEMENT TESTING**

**Test For Session Management Schema**

* [ ] Ensure all Set-Cookie directives are secure
* [ ] Ensure no cookie operation takes place over an unencrypted channel
* [ ] Ensure the cookie can’t be forced over an unencrypted channel
* [ ] Ensure the HTTPOnly flag is enabled
* [ ] Check if any cookies are persistent
* [ ] Check for session cookies and cookie expiration date/time
* [ ] Check for session fixation
* [ ] Check for concurrent login
* [ ] Check for session after logout
* [ ] Check for session after closing the browser
* [ ] Try decoding cookies (Base64, Hex, URL, etc)

**Test For Cookie Attributes**

* [ ] Ensure the cookie must be set with the secure attribute
* [ ] Ensure the cookie must be set with the path attribute
* [ ] Ensure the cookie must have the HTTPOnly flag

**Test For Session Fixation**

* [ ] Ensure new cookies have been issued upon a successful authentication
* [ ] Test manipulating the cookies

**Test For Exposed Session Variables**

* [ ] Test for encryption
* [ ] Test for GET and POST vulnerabilities
* [ ] Test if GET request incorporating the session ID used
* [ ] Test by interchanging POST with GET method

**Test For Back Refresh Attack**

* [ ] Test after password change
* [ ] Test after logout

**Test For Cross Site Request Forgery**

* [ ] Check if the token is validated on the server-side or not
* [ ] Check if the token is validated for full or partial length
* [ ] Check by comparing the CSRF tokens for multiple dummy accounts
* [ ] Check CSRF by interchanging POST with GET method
* [ ] Check CSRF by removing the CSRF token parameter
* [ ] Check CSRF by removing the CSRF token and using a blank parameter
* [ ] Check CSRF by using unused tokens
* [ ] Check CSRF by replacing the CSRF token with its own values
* [ ] Check CSRF by changing the content type to form-multipart
* [ ] Check CSRF by changing or deleting some characters of the CSRF token
* [ ] Check CSRF by changing the referrer to Referrer
* [ ] Check CSRF by changing the host values
* [ ] Check CSRF alongside clickjacking

**Test For Logout Functionality**

* [ ] Check the log out function on different pages
* [ ] Check for the visibility of the logout button
* [ ] Ensure after logout the session was ended
* [ ] Ensure after logout we can’t able to access the dashboard by pressing the back button
* [ ] Ensure proper session timeout has been set

**Test For Session Timeout**

* [ ] Ensure there is a session timeout exists
* [ ] Ensure after the timeout, all of the tokens are destroyed

**Test For Session Puzzling**

* [ ] Identify all the session variables
* [ ] Try to break the logical flow of the session generation

**Test For Session Hijacking**

* [ ] Test session hijacking on target that doesn’t has HSTS enabled
* [ ] Test by login with the help of captured cookies

#### **INPUT VALIDATION TESTING**

**Test For Reflected Cross Site Scripting**

* [ ] Ensure these characters are filtered <>’’&””
* [ ] Test with a character escape sequence
* [ ] Test by replacing < and > with HTML entities < and >
* [ ] Test payload with both lower and upper case
* [ ] Test to break firewall regex by new line /r/n
* [ ] Test with double encoding
* [ ] Test with recursive filters
* [ ] Test injecting anchor tags without whitespace
* [ ] Test by replacing whitespace with bullets
* [ ] Test by changing HTTP methods

**Test For Stored Cross Site Scripting**

* [ ] Identify stored input parameters that will reflect on the client-side
* [ ] Look for input parameters on the profile page
* [ ] Look for input parameters on the shopping cart page
* [ ] Look for input parameters on the file upload page
* [ ] Look for input parameters on the settings page
* [ ] Look for input parameters on the forum, comment page
* [ ] Test uploading a file with XSS payload as its file name
* [ ] Test with HTML tags

**Test For HTTP Parameter Pollution**

* [ ] Identify the backend server and parsing method used
* [ ] Try to access the injection point
* [ ] Try to bypass the input filters using HTTP Parameter Pollution

**Test For SQL Injection**

* [ ] Test SQL Injection on authentication forms
* [ ] Test SQL Injection on the search bar
* [ ] Test SQL Injection on editable characteristics
* [ ] Try to find SQL keywords or entry point detections
* [ ] Try to inject SQL queries
* [ ] Use tools like SQLmap or Hackbar
* [ ] Use Google dorks to find the SQL keywords
* [ ] Try GET based SQL Injection
* [ ] Try POST based SQL Injection
* [ ] Try COOKIE based SQL Injection
* [ ] Try HEADER based SQL Injection
* [ ] Try SQL Injection with null bytes before the SQL query
* [ ] Try SQL Injection with URL encoding
* [ ] Try SQL Injection with both lower and upper cases
* [ ] Try SQL Injection with SQL Tamper scripts
* [ ] Try SQL Injection with SQL Time delay payloads
* [ ] Try SQL Injection with SQL Conditional delays
* [ ] Try SQL Injection with Boolean based SQL
* [ ] Try SQL Injection with Time based SQL

**Test For LDAP Injection**

* [ ] Use LDAP search filters
* [ ] Try LDAP Injection for access control bypass

**Testing For XML Injection**

* [ ] Check if the application is using XML for processing
* [ ] Identify the XML Injection point by XML metacharacter
* [ ] Construct XSS payload on top of XML

**Test For Server Side Includes**

* [ ] Use Google dorks to find the SSI
* [ ] Construct RCE on top of SSI
* [ ] Construct other injections on top of SSI
* [ ] Test Injecting SSI on login pages, header fields, referrer, etc

**Test For XPATH Injection**

* [ ] Identify XPATH Injection point
* [ ] Test for XPATH Injection

**Test For IMAP SMTP Injection**

* [ ] Identify IMAP SMTP Injection point
* [ ] Understand the data flow
* [ ] Understand the deployment structure of the system
* [ ] Assess the injection impact

**Test For Local File Inclusion**

* [ ] Look for LFI keywords
* [ ] Try to change the local path
* [ ] Use the LFI payload list
* [ ] Test LFI by adding a null byte at the end

**Test For Remote File Inclusion**

* [ ] Look for RFI keywords
* [ ] Try to change the remote path
* [ ] Use the RFI payload list

**Test For Command Injection**

* [ ] Identify the Injection points
* [ ] Look for Command Injection keywords
* [ ] Test Command Injection using different delimiters
* [ ] Test Command Injection with payload list
* [ ] Test Command Injection with different OS commands

**Test For Format String Injection**

* [ ] Identify the Injection points
* [ ] Use different format parameters as payloads
* [ ] Assess the injection impact

**Test For Host Header Injection**

* [ ] Test for HHI by changing the real Host parameter
* [ ] Test for HHI by adding X-Forwarded Host parameter
* [ ] Test for HHI by swapping the real Host and X-Forwarded Host parameter
* [ ] Test for HHI by adding two Host parameters
* [ ] Test for HHI by adding the target values in front of the original values
* [ ] Test for HHI by adding the target with a slash after the original values
* [ ] Test for HHI with other injections on the Host parameter
* [ ] Test for HHI by password reset poisoning

**Test For Server Side Request Forgery**

* [ ] Look for SSRF keywords
* [ ] Search for SSRF keywords only under the request header and body
* [ ] Identify the Injection points
* [ ] Test if the Injection points are exploitable
* [ ] Assess the injection impact

**Test For Server Side Template Injection**

* [ ] Identify the Template injection vulnerability points
* [ ] Identify the Templating engine
* [ ] Use the tplmap to exploit

#### **ERROR HANDLING TESTING**

**Test For Improper Error Handling**

* [ ] Identify the error output
* [ ] Analyze the different outputs returned
* [ ] Look for common error handling flaws
* [ ] Test error handling by modifying the URL parameter
* [ ] Test error handling by uploading unrecognized file formats
* [ ] Test error handling by entering unrecognized inputs
* [ ] Test error handling by making all possible errors

#### **WEAK CRYPTOGRAPHY TESTING**

**Test For Weak Transport Layer Security**

* [ ] Test for DROWN weakness on SSLv2 protocol
* [ ] Test for POODLE weakness on SSLv3 protocol
* [ ] Test for BEAST weakness on TLSv1.0 protocol
* [ ] Test for FREAK weakness on export cipher suites
* [ ] Test for Null ciphers
* [ ] Test for NOMORE weakness on RC4
* [ ] Test for LUCKY 13 weakness on CBC mode ciphers
* [ ] Test for CRIME weakness on TLS compression
* [ ] Test for LOGJAM on DHE keys
* [ ] Ensure the digital certificates should have at least 2048 bits of key length
* [ ] Ensure the digital certificates should have at least SHA-256 signature algorithm
* [ ] Ensure the digital certificates should not use MDF and SHA-1
* [ ] Ensure the validity of the digital certificate
* [ ] Ensure the minimum key length requirements
* [ ] Look for weak cipher suites

#### **BUSINESS LOGIC TESTING**

**Test For Business Logic**

* [ ] Identify the logic of how the application works
* [ ] Identify the functionality of all the buttons
* [ ] Test by changing the numerical values into high or negative values
* [ ] Test by changing the quantity
* [ ] Test by modifying the payments
* [ ] Test for parameter tampering

**Test For Malicious File Upload**

* [ ] Test malicious file upload by uploading malicious files
* [ ] Test malicious file upload by putting your IP address on the file name
* [ ] Test malicious file upload by right to left override
* [ ] Test malicious file upload by encoded file name
* [ ] Test malicious file upload by XSS payload on the file name
* [ ] Test malicious file upload by RCE payload on the file name
* [ ] Test malicious file upload by LFI payload on the file name
* [ ] Test malicious file upload by RFI payload on the file name
* [ ] Test malicious file upload by SQL payload on the file name
* [ ] Test malicious file upload by other injections on the file name
* [ ] Test malicious file upload by Inserting the payload inside of an image by the bmp.pl tool
* [ ] Test malicious file upload by uploading large files (leads to DOS)

#### **CLIENT SIDE TESTING**

**Test For DOM Based Cross Site Scripting**

* [ ] Try to identify DOM sinks
* [ ] Build payloads to that DOM sink type

**Test For URL Redirect**

* [ ] Look for URL redirect parameters
* [ ] Test for URL redirection on domain parameters
* [ ] Test for URL redirection by using a payload list
* [ ] Test for URL redirection by using a whitelisted word at the end
* [ ] Test for URL redirection by creating a new subdomain with the same as the target
* [ ] Test for URL redirection by XSS
* [ ] Test for URL redirection by profile URL flaw

**Test For Cross Origin Resource Sharing**

* [ ] Look for “Access-Control-Allow-Origin” on the response
* [ ] Use the CORS HTML exploit code for further exploitation

**Test For Clickjacking**

* [ ] Ensure “X-Frame-Options” headers are enabled
* [ ] Exploit with iframe HTML code for POC

#### **OTHER COMMON ISSUES**

#### Card Payment Functionality

*

**Test For No-Rate Limiting**

* [ ] Ensure rate limiting is enabled
* [ ] Try to bypass rate limiting by changing the case of the endpoints
* [ ] Try to bypass rate limiting by adding / at the end of the URL
* [ ] Try to bypass rate limiting by adding HTTP headers
* [ ] Try to bypass rate limiting by adding HTTP headers twice
* [ ] Try to bypass rate limiting by adding Origin headers
* [ ] Try to bypass rate limiting by IP rotation
* [ ] Try to bypass rate limiting by using null bytes at the end
* [ ] Try to bypass rate limiting by using race conditions

**Test For EXIF Geodata**

* [ ] Ensure the website is striping the geodata
* [ ] Test with EXIF checker

**Test For Broken Link Hijack**

* [ ] Ensure there is no broken links are there
* [ ] Test broken links by using the blc tool

**Test For SPF**

* [ ] Ensure the website is having SPF record
* [ ] Test SPF by nslookup command

**Test For Weak 2FA**

* [ ] Try to bypass 2FA by using poor session management
* [ ] Try to bypass 2FA via the OAuth mechanism
* [ ] Try to bypass 2FA via brute-forcing
* [ ] Try to bypass 2FA via response manipulation
* [ ] Try to bypass 2FA by using activation links to login
* [ ] Try to bypass 2FA by using status code manipulation
* [ ] Try to bypass 2FA by changing the email or password
* [ ] Try to bypass 2FA by using a null or empty entry
* [ ] Try to bypass 2FA by changing the boolean into false
* [ ] Try to bypass 2FA by removing the 2FA parameter on the request

**Test For Weak OTP Implementation**

* [ ] Try to bypass OTP by entering the old OTP
* [ ] Try to bypass OTP by brute-forcing
* [ ] Try to bypass OTP by using a null or empty entry
* [ ] Try to bypass OTP by response manipulation
* [ ] Try to bypass OTP by status code manipulation
{% endtab %}

{% tab title="API" %}
### API Testing Checklist

MindAPI - [API Testing Mindmap ](https://dsopas.github.io/MindAPI/play/)

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

* [ ] Search for API documentation, if not provided, tsee if it can be discovered
  * [ ] Example API doc Wordlist [here](https://github.com/hAPI-hacker/Hacking-APIs/blob/main/api\_docs\_path)
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
| < >        | \<find-function>                                                                                                             | Angle Brackets represent a DomString, which is a 16-bit string                                                                                                                                                           |

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

**Mass Assignment Vulnerabilities**\


Mass Assignment with account registration for PrivEsc:

Admin Registration

```json
POST /api/admin/create/user
Token: AdminAuthToken
-Redacted-
{
"username": "admin2",
"pass": "Iforgetit0ften",
"admin": true
}
```

```json
POST /create/user
Token: StandardUserAuthToken
-Redacted-
{
"username": "tester",
"pass": "Test1234",
"admin": true
}
```



Blind Mass Assignment: \
If you suspect an API is vulnerable to Mass Assignment, there is a chance it may ignore the irrelevant variables and accept the variable that matches the expected name and format.

```json
{
"username":"testern",
"email":"tester@site.com",
"admin": true,
"admin":1,
"isadmin": true,
"role":"admin",
"role":"administrator",
"user_priv": "admin",
"password":"Password1!"
}
```

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

{% tab title="Labs" %}
**crAPI Lab Setup**

```bash
mkdir /apilab
cd /apilab
sudo curl -o docker-compose.yml https://raw.githubusercontent.com/OWASP/crAPI/main/deploy/docker/docker-compose.yml
sudo docker-compose pull
sudo docker-compose -f docker-compose.yml --compatibility up -d
```

crAPI Landing page will be located at http://127.0.0.1:8888 with the crAPI Mailhog Server at http://127.0.0.1:8025

***

**vAPI lab setup**

```bash
mkdir /apilab
cd /apilab
sudo git clone https://github.com/roottusk/vapi.git
cd /vapi
sudo docker-compose up -d
```



#### OWASP DevSlop's Pixi

<pre class="language-bash"><code class="lang-bash"><strong>git clone https://github.com/DevSlop/Pixi.git
</strong>cd Pixi
sudo docker-compose up
</code></pre>



#### Damn Vulnerable GraphQL Application (DVGA)

```bash
sudo docker pull dolevf/dvga
sudo docker run -t -p 5000:5000 -e WEB_HOST=0.0.0.0 dolevf/dvga
```
{% endtab %}

{% tab title="Thick Clients" %}
## THICK CLIENT PENTESTING CHECKLIST

**OWASP Based Checklist by** [Hariprasaanth R](https://github.com/Hari-prasaanth/Thick-Client-Pentest-Checklist)

Also available on [Notion ](https://hariprasaanth.notion.site/THICK-CLIENT-PENTESTING-CHECKLIST-35c6803f26eb4c9d89ba7f5fdc901fb0)\


#### **INFORMATION GATHERING**

**Information Gathering**

* [ ] Find out the application architecture (two-tier or three-tier)
* [ ] Find out the technologies used (languages and frameworks)
* [ ] Identify network communication
* [ ] Observe the application process
* [ ] Observe each functionality and behavior of the application
* [ ] Identify all the entry points
* [ ] Analyze the security mechanism (authorization and authentication)

**Tools Used**

* [ ] CFF Explorer
* [ ] Sysinternals Suite
* [ ] Wireshark
* [ ] PEid
* [ ] Detect It Easy (DIE)
* [ ] Strings

#### **GUI TESTING**

**Test For GUI Object Permission**

* [ ] Display hidden form object
* [ ] Try to activate disabled functionalities
* [ ] Try to uncover the masked password

**Test GUI Content**

* [ ] Look for sensitive information

**Test For GUI Logic**

* [ ] Try for access control and injection-based vulnerabilities
* [ ] Bypass controls by utilizing intended GUI functionality
* [ ] Check improper error handling
* [ ] Check weak input sanitization
* [ ] Try privilege escalation (unlocking admin features to normal users)
* [ ] Try payment manipulation

**Tools Used**

* [ ] UISpy
* [ ] Winspy++
* [ ] Window Detective
* [ ] Snoop WPF

#### **FILE TESTING**

**Test For Files Permission**

* [ ] Check permission for each and every file and folder

**Test For File Continuity**

* [ ] Check strong naming
* [ ] Authenticate code signing

**Test For File Content Debugging**

* [ ] Look for sensitive information on the file system (symbols, sensitive data, passwords, configurations)
* [ ] Look for sensitive information on the config file
* [ ] Look for Hardcoded encryption data
* [ ] Look for Clear text storage of sensitive data
* [ ] Look for side-channel data leakage
* [ ] Look for unreliable log

**Test For File And Content Manipulation**

* [ ] Try framework backdooring
* [ ] Try DLL preloading
* [ ] Perform Race condition check
* [ ] Test for Files and content replacement
* [ ] Test for Client-side protection bypass using reverse engineering

**Test For Function Exported**

* [ ] Try to find the exported functions
* [ ] Try to use the exported functions without authentication

**Test For Public Methods**

* [ ] Make a wrapper to gain access to public methods without authentication

**Test For Decompile And Application Rebuild**

* [ ] Try to recover the original source code, passwords, keys
* [ ] Try to decompile the application
* [ ] Try to rebuild the application
* [ ] Try to patch the application

**Test For Decryption And DE obfuscation**

* [ ] Try to recover original source code
* [ ] Try to retrieve passwords and keys
* [ ] Test for lack of obfuscation

**Test For Disassemble and Reassemble**

* [ ] Try to build a patched assembly

**Tools Used**

* [ ] Strings
* [ ] dnSpy
* [ ] Procmon
* [ ] Process Explorer
* [ ] Process Hacker

#### **REGISTRY TESTING**

**Test For Registry Permissions**

* [ ] Check read access to the registry keys
* [ ] Check to write access to the registry keys

**Test For Registry Contents**

* [ ] Inspect the registry contents
* [ ] Check for sensitive info stored on the registry
* [ ] Compare the registry before and after executing the application

**Test For Registry Manipulation**

* [ ] Try for registry manipulation
* [ ] Try to bypass authentication by registry manipulation
* [ ] Try to bypass authorization by registry manipulation

**Tools Used**

* [ ] Regshot
* [ ] Procmon
* [ ] Accessenum

#### **NETWORK TESTING**

**Test For Network**

* [ ] Check for sensitive data in transit
* [ ] Try to bypass firewall rules
* [ ] Try to manipulate network traffic

**Tools Used**

* [ ] Wireshark
* [ ] TCPview

#### **ASSEMBLY TESTING**

**Test For Assembly**

* [ ] Verify Address Space Layout Randomization (ASLR)
* [ ] Verify SafeSEH
* [ ] Verify Data Execution Prevention (DEP)
* [ ] Verify strong naming
* [ ] Verify ControlFlowGuard
* [ ] Verify HighentropyVA

**Tools Used**

* [ ] PESecurity

#### **MEMORY TESTING**

**Test For Memory Content**

* [ ] Check for sensitive data stored in memory

**Test For Memory Manipulation**

* [ ] Try for memory manipulation
* [ ] Try to bypass authentication by memory manipulation
* [ ] Try to bypass authorization by memory manipulation

**Test For Run Time Manipulation**

* [ ] Try to analyze the dump file
* [ ] Check for process replacement
* [ ] Check for modifying assembly in the memory
* [ ] Try to debug the application
* [ ] Try to identify dangerous functions
* [ ] Use breakpoints to test each and every functionality

**Tools Used**

* [ ] Process Hacker
* [ ] HxD
* [ ] Strings

#### **TRAFFIC TESTING**

**Test For Traffic**

* [ ] Analyze the flow of network traffic
* [ ] Try to find sensitive data in transit

**Tools Used**

* [ ] Echo Mirage
* [ ] MITM Relay
* [ ] Burp Suite

#### **COMMON VULNERABILITIES TESTING**

**Test For Common Vulnerabilities**

* [ ] Try to decompile the application
* [ ] Try for reverse engineering
* [ ] Try to test with OWASP WEB Top 10
* [ ] Try to test with OWASP API Top 10
* [ ] Test for DLL Hijacking
* [ ] Test for signature checks (Use Sigcheck)
* [ ] Test for binary analysis (Use Binscope)
* [ ] Test for business logic errors
* [ ] Test for TCP/UDP attacks
* [ ] Test with automated scanning tools (Use Visual Code Grepper - VCG)
{% endtab %}

{% tab title="APKs" %}
`TargetSdkversion` \
OS version an app was designed for\
\
`< package= com.vulnerableapp.test>` \
`Describes package/app name`\
\
`<uses-sdk android:minSdkVersion="17" android:minSdkVersion="21"/>` \
`App minimum and maximum supported versions(range)`



\
[APKLeaks](https://github.com/dwisiswant0/apkleaks) - analyze compiled APK file



#### Pulling an APK

1. Download app from google play store on the android device OR an .apk file will be provided by client
2. To get apk from the phone to your computer use the following commands
   * [ ] adb shell pm list packages (this will list all packages) or adb shell pm list packages | grep \<identifier>
   * [ ] adb pm path (domain.com)
   * [ ] adb pull \<copied file path> OR adb pull \<copied file path> \<newname>.apk (second command renames the base apk)

#### Methodology

Source: [https://mobile-security.gitbook.io/mobile-security-testing-guide/android-testing-guide/0x05b-basic-security\_testing](https://mobile-security.gitbook.io/mobile-security-testing-guide/android-testing-guide/0x05b-basic-security\_testing)

1. Open android studio
2. Plug in phone and make sure it connects to android studio
3. Run the following to make a connection over usb to get traffic from the phone through burp. (physical phone)&#x20;
   * [ ] adb revserse tcp:\<port from burp i.e 8082> tcp:\<same port i.e 8082>
4. Pull the APK or install the APK
5. Throw the APK in mobsf for static analysis (mobsf will look through all the files and pull out data for you)&#x20;
   * [ ] Check mobsf findings (url's, harded coded keys, etc)&#x20;
   * [ ] Check out the manifest.xml (where some important things can be stored)
6. Use apktool to pull files from the phone to do a more manual static analysis&#x20;
   * [ ] apktool d \<example.apk>&#x20;
   * [ ] Manuel click through of the files
7. Can also use jadx-gui to search files manually&#x20;
   * [ ] jadx-gui&#x20;
   * [ ] Pick apk file to drop in&#x20;
   * [ ] Look at manifest.xml file&#x20;
   * [ ] Check resrources.arsc for strings, xml, json i. Resrouces.ars -> res -> values&#x20;
   * [ ] Can also use the search to look through all the files i. i.e password, api\_key, etc
8. Open the APP on phone or emulator
9. Make sure traffic is being proxied through burp
10. Run objection&#x20;
    * [ ] objection --gadget explore
11. Disable sslpinning if the app is preventing from exploring&#x20;
    * [ ] a. android sslpinning disable --quiet
12. Check android keystore for any credentials&#x20;
    * [ ] a. android keystore list
13. Run Drozer and the following commands&#x20;
    * [ ] Check attack surface&#x20;
      * [ ] run app.package.attacksurface \<com.app.android>&#x20;
    * [ ] Check activity info&#x20;
      * [ ] run app.activity.info -a \<com.app.android>&#x20;
    * [ ] Check package info&#x20;
      * [ ] run app.package.info -a \<com.app.android>&#x20;
    * [ ] Check Broadcasts&#x20;
      * [ ] run app.broadcast.info -a \<com.app.android>&#x20;
    * [ ] Scan URI's&#x20;
      * [ ] run scanner.provider.finduris -a \<com.app.android>&#x20;
    * [ ] Directory traversal&#x20;
      * [ ] run scanner.provider.traversal -a \<com.app.android>&#x20;
    * [ ] SQL Injection&#x20;
      * [ ] Run scanner.provider.injection -a \<com.app.android>
14. if there is a firebase url navigate to the url and add the following json check to see if its vulnerable&#x20;
    * [ ] a. https://example-mobile.firebaseio.com/.json&#x20;
    * [ ] b. If this is denied you can try and fuzz an endpoint i. i.e https://example-mobile.firebaseio.com/FUZZ/.json
15. In android studio check the /data/data/\<com.example.android>&#x20;
    * [ ] Check xml files, strings, .json files, DB's
16. Copy db to sdcard&#x20;
    * [ ] adb shell "su -c cp /data/data/\<com.exampleapp.android>/databases/ /sdcard/Dwonload"
17. Pull dbs to local machine&#x20;
    * [ ] adb pull /sdcard/Download/
18. View dbs in db browser sqlite
19. Do a manual click through and generate some traffic with burp
20. Run a burp scan
21. Test app like it’s a web app. (XSS, SQL injection, login bypass etc)
22. Check logs in android studio to see if any sensitive data is passed through.&#x20;
    * [ ] a. Can also use the command line tool to check the logs or you can use android studio to view the logs&#x20;
    * [ ] b. adb logcat
{% endtab %}

{% tab title="iOS" %}
Jailbreak Tools:

Linux Jailbreak Software Checkra1n\
[Palera1n (newer iOS Jailbreak)](https://github.com/palera1n/palera1n)\
\
Windows version of Checkra1n - iRa1n \
3utools.com - iOS device management tool

Testing Tools:\
OpenSSH\
BurpPro mobile assistant

#### Application Testing setup

1. Install iproxy `npm install iproxy` and BurpSuite application proxy on host
2. Start Burp suite and add a listener on port 8082 for all interfaces
3. Go to iOS settings, set a manual proxy using the Burp Suite host's IP and port 8082
4.  Connect host PC to mobile device using SSH through iproxy using&#x20;

    a. `iproxy 2222 22 & ssh -R 8082:localhost:8082 root@localhost -p 2222`
5. On iOS device visit http://burpsuite to verify connectivity and download Burp CA certificate
6. Go to apple device settings in the "profile downloaded" section and install certificate
7. Go Settings >General >About > Certificate Trust Settings and activate toggle switch&#x20;



#### Methodology

Source: [https://mobile-security.gitbook.io/mobile-security-testing-guide/ios-testing-guide/0x06b-basic-security-testing](https://mobile-security.gitbook.io/mobile-security-testing-guide/ios-testing-guide/0x06b-basic-security-testing)\


1. Download app from appstore OR install ipa file from local machine to iphone
2. Proxy iphone with iproxy this will establish a usb connection
   * [ ] iproxy 2222 22 & ssh -R 8082:localhost:8082 root@localhost -p 2222
3. Proxy traffic through burp
4. Pull ipa off the phone to a local directory by using frida-ios-dump
   * [ ] a. python3 dump.py -l (this will check all the files on the phone)
   * [ ] b. python3 dump.py com.example.ipa
5. Make a copy of the file and rename it to Payload.zip
6. Unzip the file from the command line
   * [ ] Unzip example.ipa OR unzip in the file location
7. From finder go into the Payload folder and into the next payload folder. This is where the example.app is stored
8. Right click on the example.app and click show package contents
9. Look at all the files. Some can be opened in xcode
10. Look more specifically at the info.plist file and open it with xcode
    * [ ] Plists generally have a lot of info and this is where we can find API keys and other juciy items
11. Open and look at json files if any are available.
12. Run mobsf and drop the example.ipa file in
    * [ ] Mobsf is not as verbose with ios compared to android which is why we do more of a manual click through of the files
    * [ ] Still use it as it can save some time
13. Run Objection
    * [ ] objection --gadget com.example.ipa explore
    * [ ] Once objection is running use the follow commands to search and dump different files
    * [ ] Check binary info
      * [ ] ios info binary
    * [ ] Check Ios KeyChain
      * [ ] ios keychain dump
    * [ ] Check plist files
      * [ ] ios plist cat info.plist
    * [ ] Check user credential storage
      * [ ] ios nsurlcredentialstorage dump
    * [ ] Check userdefaults
      * [ ] ios nsuserdefaults get
    * [ ] Check cookies
      * [ ] ios cookies get
    * [ ] Disable cert pinning
      * [ ] ios sslpinning disable --quiet
      * [ ] If you have issues with sslpinning you can use sslkillswitch or try patching with objection manually
14. Do a manual click through and generate some traffic with burp
15. Run a burp scan
16. Test app like it’s a web app. (XSS, SQL injection, login bypass etc)
17. Check IOS logs
    * [ ] a. Connect the iPhone or iPad you want to view logs for to a Mac by using a USB connection, be sure to unlock the iOS device as well
    * [ ] b. Open the “Console” app on Mac OS, found in the /Applications/Utilities/ directory
    * [ ] c. From the Console app sidebar, look under the ‘Devices’ section and select the iPhone or iPad that is connected to the Mac


{% endtab %}
{% endtabs %}

