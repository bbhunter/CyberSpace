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
Use GitTools gitdumper.sh&#x20;

* [ ] `gitdumper.sh http://IPorURL/.git git`
