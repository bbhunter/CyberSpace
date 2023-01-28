---
description: Reliable Resources for AppSec
---

# Application Security

#### Getting Started

| Component              |  Description                                                                                                                                                                                                   |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Back end Servers       | The hardware and operating system that hosts all other components and are usually run on operating systems like Linux, Windows, or using Containers.                                                           |
| Web Servers            | Web servers handle HTTP requests and connections. Some examples are Apache, NGINX, and IIS.                                                                                                                    |
| Databases              | Databases (DBs) store and retrieve the web application data. Some examples of relational databases are MySQL, MSSQL, Oracle, PostgreSQL, while examples of non-relational databases include NoSQL and MongoDB. |
| Development Frameworks | Development Frameworks are used to develop the core Web Application. Some well-known frameworks include PHP, C#, Java, Python, and NodeJS JavaScript                                                           |

#### Field References

{% tabs %}
{% tab title="General" %}
| [TCM Security PWST Lab Environment !](https://github.com/mttaggart/pwst-resources)                                   | [Burpsuite: Commercial Web app testing tool](https://portswigger.net/burp) !                                                            | [Awesome Burp Extensions](https://github.com/snoopysecurity/awesome-burp-extensions)                             |
| -------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| [OWASP Cheat Sheet Series](https://github.com/OWASP/CheatSheetSeries)                                                | [Awesome Web Hacking from @infoslack](https://github.com/infoslack/awesome-web-hacking)                                                 | [Awesome Web Security](https://github.com/qazbnm456/awesome-web-security)                                        |
| [PortSwigger Web Security Academy Lab Files from @rkhal101](https://github.com/rkhal101/Web-Security-Academy-Series) | [Hack-Tools Chrome Extension for Web Pentesting](https://chrome.google.com/webstore/detail/hack-tools/cmbndhnoonmghfofefkcccljbkdpamhi) | [OWASP Vulnerability Scanner Tool List](https://owasp.org/www-community/Vulnerability\_Scanning\_Tools)          |
| [Awesome Hacking Resources](https://github.com/vitalysim/Awesome-Hacking-Resources)                                  | [Damn Vulnerable PHP App](https://github.com/c0brabaghdad1/DVPA)                                                                        | [Vulnerable Java Application](https://github.com/CSPF-Founder/JavaVulnerableLab)                                 |
| [OWASP Secrets Management focused vulnerable app](https://github.com/commjoen/wrongsecrets)                          | [403 byebye](https://github.com/nxenon/403-byebye)                                                                                      | [Awesome Application Security Checklist](https://github.com/MahdiMashrur/Awesome-Application-Security-Checklist) |
{% endtab %}

{% tab title="Bug Bounty" %}
| [Bug Hunter Handbook](https://gowthams.gitbook.io/bughunter-handbook)            | [Awesome Bug Bounty Resources](https://github.com/djadmin/awesome-bug-bounty) | [Awesome Bug Bounty Hunting Tool](https://github.com/0xApt/awesome-bbht) |
| -------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| [All About Bug Bounty Note Repo](https://github.com/daffainfo/AllAboutBugBounty) | [BugHunter Handbook](https://gowthams.gitbook.io/bughunter-handbook/)         | [Bug Bounty Wiki](https://bug.bounty.wiki/)                              |
|                                                                                  |                                                                               |                                                                          |
{% endtab %}

{% tab title="Extensions/Plugins" %}

{% endtab %}

{% tab title="Static Code Analysis" %}


* [SonarQube](https://www.sonarsource.com/products/sonarqube/downloads/) website and [Git Repo](https://github.com/SonarSource/sonarqube)
* [CodeCat](https://github.com/CoolerVoid/codecat) - open-source tool to help find/track user input sinks and other security bugs
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Recon" %}
#### Reconnaissance

|                                                                                                     |                                                                |                                                                          |
| --------------------------------------------------------------------------------------------------- | -------------------------------------------------------------- | ------------------------------------------------------------------------ |
| [Final Recon (Web Reconnaissance) from @thewhiteh4t](https://github.com/thewhiteh4t/FinalRecon)     | [Sublist3r](https://github.com/aboul3la/Sublist3r)             | [patator](https://github.com/lanjelot/patator)                           |
| [ffuf](https://github.com/ffuf/ffuf)                                                                | [wfuzz](https://github.com/xmendez/wfuzz)                      | [xnLinkFinder](https://github.com/xnl-h4ck3r/xnLinkFinder)               |
| [WebOSINT](https://github.com/C3n7ral051nt4g3ncy/webosint)                                          | [All in One Recon Tool (AORT)](https://github.com/D3Ext/AORT)  | [katana by ProjectDiscovery](https://github.com/projectdiscovery/katana) |
| [Domain to IP converter (Python) by @YSSVirus](https://github.com/YSSVirus/domain-to-ip\_converter) | [Cariddi by @edoardott](https://github.com/edoardottt/cariddi) |                                                                          |

#### SubDomain/DNS Enumeration

|                                                            |                                                         |                                          |
| ---------------------------------------------------------- | ------------------------------------------------------- | ---------------------------------------- |
| [MayorSec DNS Scan](https://github.com/dievus/msdnsscan) ! | [PureDNS](https://github.com/d3mondev/puredns)          | [DNSrr](https://github.com/A3h1nt/Dnsrr) |
| [AquaTone](https://github.com/michenriksen/aquatone)       | [DNSReaper](https://github.com/punk-security/dnsReaper) |                                          |
{% endtab %}

{% tab title="Add-ons" %}
## Extensions and Plugins

| Extensions                                                                                                                     |                                                                                    |                                                                 |
| ------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| [HackTools Browser Extension Repo (Easier install from extension menu)](https://github.com/LasCC/Hack-Tools.git)               | [Penetration Testing Kit Browser Extension](https://pentestkit.co.uk/index.html) ! | [Wappalyzer Browser Extension](https://www.wappalyzer.com/apps) |
| [Vulners Browser Extension](https://chrome.google.com/webstore/detail/vulners-web-scanner/dgdelbjijbkahooafjfnonijppnffhmd?hl) |                                                                                    |                                                                 |

| Burp Suite                                                                                                                                                                                                            |                                                                                                                                                                                 |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Nuclei burp plugin](https://github.com/projectdiscovery/nuclei-burp-plugin) (also in [Bapp store](https://portswigger.net/bappstore/9c7f7ae2844c4828b28be2398c02b7f7)) - generate nuclei template from burp requests | [HackBar Extension](https://github.com/d3vilbug/HackBar) (also in [Bapp store](https://portswigger.net/bappstore/526f5564b7414bfe978e650d8ea6567b)) - Security testing Payloads |
|                                                                                                                                                                                                                       |                                                                                                                                                                                 |
{% endtab %}

{% tab title="WAF" %}
#### Detection and Evasions

|                                                                           |     |     |
| ------------------------------------------------------------------------- | --- | --- |
| [wafw00f from @enableSecurity](https://github.com/EnableSecurity/wafw00f) | --- | --- |
{% endtab %}
{% endtabs %}
