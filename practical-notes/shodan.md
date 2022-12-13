# Shodan

| Query                                   | Description                                                                                                 |
| --------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| ssl.cert.subject.CN:"\*.google.com"+200 | Returns all SSL services that has issued a certificate for \*.google.com with an HTTP response code of 200. |
| ssl.cert.issuer.cn:"DOD SW CA-60" 200   | Returns all SSL certificates that have been issued by the DoD with reponse code of 200                      |
