---
description: Working Dashboards for Splunk
---

# Splunk IR

IPS High Risk Alert Not Blocked. Below is an example using Palo Alto Networks (PAN) IPS

```
index=pan sourcetype="pan:threat" ",threat," (critical OR high) (severity=critical OR severity=high) action!="blocked" action!="dropped" | bucket span=1h _time | stats values(signature) as signature mode(dest) as dest values(dest_port) as dest_port values(file_name) as file_name values(file_hash) as file_hash count by _time, src, severity, action | eval signature=mvjoin(signature," , ") | eval dest_port=mvjoin(dest_port," , ") | eval file_name=mvjoin(file_name," , ") | eval file_hash=mvjoin(file_hash," , ")
```

DOS- Firewall Large number of DENIED Connections by Firewall

```
| tstats summariesonly=1 allow_old_summaries=1 count from datamodel=Network_Traffic.All_Traffic where All_Traffic.action="blocked" sourcetype=* AND host=* by All_Traffic.dvc host _time span=1h | rename All_Traffic.dvc AS dvc | eval dvc=if(dvc="unknown",host,dvc) | timechart span=1h sum(count) by dvc
```

Detect Many Unauthorized Access Attempts

```
| `Load_Sample_Log_Data(Windows Logons with Failure Codes)` | search Failure_Reason=* Status=0xC000015B
```

Data Exfiltration - Suspicious Destinations

```
| tstats summariesonly=1 allow_old_summaries=1 sum(All_Traffic.bytes) as bytes dc(All_Traffic.src) as "Unique Sources" from datamodel=Network_Traffic.All_Traffic where host=* by _time span=1h All_Traffic.dest
| rename All_Traffic.* as *
| eval MBytes=round(bytes/1024/1024,2)
| eventstats dc(_time) as Frequency by dest
| eval Risk=round(MBytes/(pow(Frequency,Frequency))/'Unique Sources')
| sort - Risk
| head 250
| iplocation dest
| fillnull value="" Country
| table _time, Risk, dest, "Unique Sources", MBytes, Country
```
