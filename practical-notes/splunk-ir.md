---
description: Working Dashboards for Splunk
---

# Splunk IR

IPS High Risk Alert Not Blocked. Below is an example using Palo Alto Networks (PAN) IPS

```
index=pan sourcetype="pan:threat" ",threat," (critical OR high) (severity=critical OR severity=high) action!="blocked" action!="dropped" | bucket span=1h _time | stats values(signature) as signature mode(dest) as dest values(dest_port) as dest_port values(file_name) as file_name values(file_hash) as file_hash count by _time, src, severity, action | eval signature=mvjoin(signature," , ") | eval dest_port=mvjoin(dest_port," , ") | eval file_name=mvjoin(file_name," , ") | eval file_hash=mvjoin(file_hash," , ")
```
