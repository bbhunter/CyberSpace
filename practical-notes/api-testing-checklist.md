# API Testing Checklist

**Passive Reconnaissance**

* [ ] Google Dorking to reveal specific information about the API
* [ ] Git Dorking: `authorization: Bearer` , `filename: swagger.json`&#x20;
* [ ] Shodan Search: `"content-type: application/json"`, `"wp-json"`
* [ ] Wayback Machine snapshots

**Active Reconnaissance**

* [ ] Amass: `amass enum -active -d dns.com | grep api`
  * [ ] `amass enum -active -brute -w /usr/share/wordlists/API_superlist -d example.com -dir [directory name]`
* [ ] Testing Directories: `gobuster dir -u http://10.x.x.x -w /location/to/wordlist.txt`
* [ ] `Check for API calls in Devtools > network Tab or Web App Proxy`
* [ ] Import curl request to Postman

**Endpoint Analysis**

* [ ] Proxy all traffic to Postman/Burp and capture requests for history
* [ ] Perform the actions that can be performed within application; this can be filtered in Postman

OR

* [ ] Import api doc files as new collections

API Documentation Conventions

| Convention | Example                                                                                                                      | Meaning                                                                                                                                                                                                                  |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| : or {}    | <p>/user/:id</p><p>/user/{id}</p><p>/user/1337</p><p>/account/:username</p><p>/account/{username}</p><p>/account/mart1an</p> | The colon or curly brackets are used by some APIs to indicate a path variable. In other words, “:id” represents the variable for an ID number and “{username}” represents the account username you are trying to access. |
| \[]        | <p>/api/v1/user?find=[name]</p><p> </p><p> </p>                                                                              | Square brackets indicate that the input is optional.                                                                                                                                                                     |
| \|\|       | “blue” \|\| “green” \|\| “red”                                                                                               | Double bars represent different possible values that can be used.                                                                                                                                                        |

* [ ] Set parameters to variable in Postman
