# Bug Bounty Checklist

**Information Gathering:**\
LeakIX - often blocked by organizations for gray hat searches\
Shodan - scans less frequently than LeakIX but whitelisted\
Censys - best overall scanner but without vulnerability discovery

PrettyRecon - Active Reconnaissance Tool

| Google Dork                 | Purpose                       |
| --------------------------- | ----------------------------- |
| `intitle:"index of /.git/"` | Searching for Git Directories |
|                             |                               |
|                             |                               |

Sensitive Information Exposure methods\
\
Use [GitTools](https://github.com/internetwache/GitTools) gitdumper.sh

* [ ] `gitdumper.sh http://IPorURL/.git git`

**Adobe Experience Manager (AEM) Configuration Testing**\
\
Shodan Dork:

`http.component:"Adobe Experience Manager"`

Resources\
[AEM Hacker Tool](https://github.com/0ang3el/aem-hacker)\
[SlideShare presentation on AEM by 0ang3el](https://www.slideshare.net/0ang3el/aem-hacker-approaching-adobe-experience-manager-webapps-in-bug-bounty-programs)
