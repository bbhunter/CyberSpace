---
description: General Queries and Dashboards for Splunk
---

# Splunk Queries



Failed login attempts

```splunk-spl
index=security login_status=failed
```

Suspicious network connections

```splunk-spl
index=network (src_ip=*.*.*.* AND dst_ip=malicious_IP) OR (src_ip=internal_IP AND dst_ip=external_IP)
```

Unauthorized file access

```splunk-spl
index=files file_access_status=unauthorized user!=authorized_user_1 AND user!=authorized_user_2
```

Abnormal system behavior

```splunk-spl
index=system (process_name=unexpected_process OR process_command_line=suspicious_command)
```

Brute force attacks

```splunk-spl
index=security login_status=failed src_ip=*.*.*.* | stats count by src_ip | where count > 10
```

System service disruptions

```splunk-spl
index=system (service_name=failed OR service_name=crashed)
```

Suspicious user activity

```splunk-spl
index=system (user=* AND (file_accessed=sensitive OR command_executed=unusual))
```

Excessive resource usage

```splunk-spl
index=system (cpu_utilization>90 OR memory_utilization>90)
```

Potential malware infections

```splunk-spl
index=system (file_hash=known_malware OR dst_ip=malicious_IP)
```

Unusual network traffic

```splunk-spl
index=network (traffic_volume>normal OR src_ip=internal AND dst_ip=external)
```

Potential data exfiltration

```splunk-spl
index=network (file_name=sensitive AND (protocol=ftp OR protocol=http))
```

Suspicious user accounts

```splunk-spl
index=system (user_permissions_changed=* OR user_type=admin_account_created)
```

Abnormal network behavior

```splunk-spl
index=network (traffic_volume_change>normal OR new_connection=true)
```

Potential ransomware attacks

```splunk-spl
index=system (file_encryption=true OR file_name=ransom
```

Suspicious network connections to known malicious domains

```splunk-spl
index=network dst_domain=malicious_domain
```

Potential remote access attempts

```splunk-spl
index=system (protocol=ssh OR protocol=rdp)
```

Potential denial of service attacks

```splunk-spl
index=network (traffic_volume>normal OR resource_usage>normal)
```

Suspicious file modifications

```splunk-spl
index=system (file_modified=true AND (file_type=system OR file_path=sensitive_directory))
```

Potential phishing attempts

```splunk-spl
index=email (link=suspicious OR attachment=suspicious)
```

Potential SQL injection attacks

```splunk-spl
index=system (query_text=* OR query_syntax=suspicious)
```

Suspicious user login attempts

```splunk-spl
index=system (login_status=failed OR (username=* AND password=*))
```

Potential unauthorized access to sensitive data

```splunk-spl
index=system (file_access=sensitive OR database_access=sensitive) AND user!=authorized_user
```

Abnormal system performance

```splunk-spl
index=system (cpu_utilization>normal OR memory_utilization>normal OR response_time>normal)
```

Potential data breaches

```splunk-spl
index=system (data_exfiltration=true OR user_account_access=unauthorized)
```

Potential cross-site scripting attacks

```splunk-spl
index=web (code_injection=true OR javascript_executed=unexpected)sp
```

Suspicious website traffic

```splunk-spl
index=web (traffic_volume_change>normal OR new_referral_source=true)
```

Potential unauthorized access to web servers

```splunk-spl
index=web (access_attempt=suspicious OR (username=* AND password=*))
```

Abnormal website behavior

```splunk-spl
index=web (new_page_appeared=true OR error_generated=true)
```

Potential directory traversal attacks

```splunk-spl
index=web (directory_access=suspicious OR traversal_technique=used)
```

Suspicious network connections from trusted IP addresses

```splunk-spl
index=network (src_ip=trusted AND (dst_ip=external OR dst_ip=malicious))
```

Potential cryptographic attacks

```splunk-spl
index=system (crypto_weakness=exploited OR crypto_algorithm=unexpected)
```

Suspicious system configuration changes

```splunk-spl
index=system (config_changed=true AND config_change_authorized=false)
```

Potential exploitation of vulnerabilities

```splunk-spl
index=system (vulnerability_exploited=true OR exploit_used=true)
```

Abnormal user behavior

```splunk-spl
index=system (command_executed=unexpected OR (file_accessed=unexpected AND directory_accessed=unexpected))
```

Potential exploits of privileged accounts

```splunk-spl
index=system (account_type=privileged AND (access_authorized=false OR usage_authorized=false))
```

Suspicious system log entries

```splunk-spl
index=system (new_log_source=true OR log_entry_type=error)
```

Potential data manipulation attacks

```splunk-spl
index=system (data_changed=true AND (data_type=database OR data_fake=true))
```

Suspicious user accounts or devices

```splunk-spl
index=system (user_account_access=unexpected OR device_access=unexpected OR (device_type=suspicious AND software_type=suspicious))
```

Potential security policy violations

```splunk-spl
index=system (data_access=restricted OR command_executed=unauthorized)
```

Suspicious email activity

```splunk-spl
index=email (attachment_received=suspicious OR data_sent=sensitive)
```

Potential privilege escalation attacks

```splunk-spl
index=system (privilege_level=elevated OR privilege_escalation_attempt=true)
```

Abnormal system log activity

```splunk-spl
index=system (log_deleted=true OR log_error_generated=true)
```

Potential data leakage

```splunk-spl
index=system (data_transferred=sensitive OR data_shared=unauthorized)
```

Suspicious system process activity

```splunk-spl
index=system (process_executed=unexpected OR process_arguments=unexpected)
```

Potential password cracking attempts

```splunk-spl
index=system (login_attempts=repeated AND password_attempts=different) OR (attack_technique=dictionary)
```

Suspicious network port activity

```splunk-spl
index=network (new_listening_port=true OR (protocol=unexpected AND port=known))
```

Potential system compromise

```splunk-spl
index=system (malware_detected=true OR (program_executed=unexpected AND script_executed=unexpected))
```

Abnormal user account activity

```splunk-spl
index=system (new_admin_account=true OR user_permissions_changed=true)
```

Potential security device misconfiguration

```splunk-spl
index=security_device (config_changed=true AND config_change_authorized=false)
```

Suspicious network traffic originating from internal IP addresses

```splunk-spl
index=network (src_ip=internal AND (dst_ip=external OR protocol=unexpected))
```

Potential unauthorized access to cloud resources

```splunk-spl
index=cloud (access_attempt=unauthorized OR (username=* AND password=*))
```

Suspicious network traffic originating from external IP addresses

```splunk-spl
index=network (src_ip=external AND (dst_ip=internal OR protocol=unexpected))
```

Potential security vulnerabilities in installed applications

```splunk-spl
index=system (installed_software_vulnerability=known OR (application_outdated=true AND application_supported=false))
```

Suspicious user activity on critical systems

```splunk-spl
index=system (command_executed=unauthorized AND system_type=critical) OR (data_accessed=sensitive AND system_type=critical)
```

Potential security vulnerabilities in network devices

```splunk-spl
index=network_device (device_vulnerability=known OR (firmware_outdated=true AND firmware_supported=false))
```

Suspicious network traffic to/from known malicious IP addresses

```splunk-spl
index=network (src_ip=malicious OR dst_ip=malicious) AND (protocol=unexpected OR protocol=known_malicious)
```

Potential security vulnerabilities in web applications

```splunk-spl
index=web (web_application_vulnerability=known OR (web_application_outdated=true AND web_application_supported=false))
```

Suspicious network connections to internal resources

```splunk-spl
index=network (src_ip=external AND (dst_ip=internal OR dst_resource=internal))
```

Potential security breaches of network perimeter defenses

```splunk-spl
index=network (internal_resource_access=unauthorized OR protocol_executed=unexpected)
```

Potential security breaches via compromised user accounts

```splunk-spl
index=system (user_account_access=unauthorized OR (username=* AND password=*))
```

Suspicious network traffic to known malicious domains

```splunk-spl
index=network (dst_domain=malicious AND domain_blacklisted=true)
```

Potential unauthorized access to system resources

```splunk-spl
index=system (file_access=sensitive OR directory_access=sensitive OR system_setting_access=sensitive) AND user!=authorized_user
```

Potential zero-day exploits

```splunk-spl
index=system (vulnerability_unknown=true OR exploit_unknown=true)
```

Suspicious network traffic to known malicious IP addresses

```splunk-spl
index=network dst_ip=malicious_IP
```

Potential insider threats

```splunk-spl
index=system (data_access=sensitive AND user_type=trusted) OR (command_executed=unauthorized AND user_type=trusted)
```

Potential security risks associated with third-party applications

```splunk-spl
index=system (third_party_application=unapproved OR third_party_application_installation_source=untrusted)
```

Suspicious network traffic to known malicious IP addresses

```splunk-spl
index=network (dst_ip=malicious OR dst_domain=malicious)
```

Potential security breaches involving privileged accounts

```splunk-spl
index=system (privileged_account_access=unauthorized OR privileged_account_permissions_changed=
```

Potential security breaches in third-party applications

```splunk-spl
index=system (third_party_software_vulnerability=known OR (application_outdated=true AND application_supported=false))
```

Suspicious user activity on mobile devices

```splunk-spl
index=mobile (app_installed=unauthorized) OR (data_accessed=sensitive AND device_type=mobile)
```

Potential security vulnerabilities in system software

```splunk-spl
index=system (operating_system_vulnerability=known OR system_library_vulnerability=known OR (system_software_outdated=true AND system_software_supported=false))
```

Suspicious network traffic patterns or anomalies

```splunk-spl
index=network (traffic_volume_change=unexpected OR new_protocol_detected=true)
```

## Dashboards

IPS High Risk Alert Not Blocked. Below is an example using Palo Alto Networks (PAN) IPS

```splunk-spl
index=pan sourcetype="pan:threat" ",threat," (critical OR high) (severity=critical OR severity=high) action!="blocked" action!="dropped" | bucket span=1h _time | stats values(signature) as signature mode(dest) as dest values(dest_port) as dest_port values(file_name) as file_name values(file_hash) as file_hash count by _time, src, severity, action | eval signature=mvjoin(signature," , ") | eval dest_port=mvjoin(dest_port," , ") | eval file_name=mvjoin(file_name," , ") | eval file_hash=mvjoin(file_hash," , ")
```

DOS- Firewall Large number of DENIED Connections by Firewall

```splunk-spl
| tstats summariesonly=1 allow_old_summaries=1 count from datamodel=Network_Traffic.All_Traffic where All_Traffic.action="blocked" sourcetype=* AND host=* by All_Traffic.dvc host _time span=1h | rename All_Traffic.dvc AS dvc | eval dvc=if(dvc="unknown",host,dvc) | timechart span=1h sum(count) by dvc
```

Detect Many Unauthorized Access Attempts

```splunk-spl
| `Load_Sample_Log_Data(Windows Logons with Failure Codes)` | search Failure_Reason=* Status=0xC000015B
```

Data Exfiltration - Suspicious Destinations

```splunk-spl
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

Detects when the number of successful Windows logon events are more than the daily average for a user account

```splunk-spl
index=windows EventCode=4624 | eval user=lower(Account_Name) | timechart span=1d avg(count) as daily_avg by user | where count > daily_avg
```

