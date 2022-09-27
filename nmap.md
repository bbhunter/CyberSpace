# Nmap

Scan a port with Nmap via proxy with the `-Pn` flag to skip host discovery and scripts

```shell-session
nmap --proxies http://127.0.0.1:8080 SERVER_IP -pPORT -Pn -sC
```
