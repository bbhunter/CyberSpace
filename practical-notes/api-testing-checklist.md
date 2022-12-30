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

**Testing**

* [ ] &#x20;To change versions: `api/v3/login` → `api/v1/login`
* [ ] &#x20;Check other AuthN endpoints: `/api/mobile/login` → `/api/v3/login` `/api/magic_link`
* [ ] &#x20;Verb Tampering: `GET /api/trips/1` → `POST /api/trips/1` `POST /api/trips` `DELETE /api/trips/1`
* [ ] &#x20;Try Object IDs in HTTP headers and bodies, URLs tend to be less vulnerable.
* [ ] &#x20;Try Numeric IDs when facing a GUID/UUID: `GET /api/users/6b95d962-df38` → `GET /api/users/1`
* [ ] &#x20;Wrap ID with an array: `{"id":111}` → `{"id":[111]}`
* [ ] &#x20;Wrap ID with a JSON object: `{"id":111}` → `{"id":{"id":111}}`
* [ ] &#x20;HTTP Parameter Pollution: `/api/profile?user_id=legit&user_id=victim` `/api/profile?user_id=victim&user_id=legit`
* [ ] &#x20;JSON Parameter Pollution: `{"user_id":legit,"user_id":victim}` `{"user_id":victim,"user_id":legit}`
* [ ] &#x20;Wildcard instead of ID: `/api/users/1` → `/api/users/*` `/api/users/%` `/api/users/_` `/api/users/.`
* [ ] &#x20;Ruby application HTTP parameter containing a URL → Pipe as the first character and then a shell command.
* [ ] &#x20;Developer APIs differs with mobile and web APIs. Test them separately.
* [ ] &#x20;Change Content-Type to `application/xml` and see if the API parse it.
* [ ] &#x20;Non-Production environments tend to be less secure (staging/qa/etc.) Leverage this fact to bypass AuthZ, AuthN, rate limiting & input validation.
* [ ] &#x20;Export Injection if you see `Convert to PDF` feature.
* [ ] &#x20;Expand your attack surface and test old versions of [APKs](https://apkpure.com/) IPAs.

Additional checks:

#### Check different `Content-Types`

```
x-www-form-urlencoded --> user=test
application/json --> {"user": "test"}
application/xml --> <user>test</user>**
```

If it's regular POST data try sending arrays, dictionaries

```
username[]=John
username[$neq]=lalala**
```

If JSON is supported try to send unexpected data types

```
{"username": "John"}
{"username": true}
{"username": null}
{"username": 1}
{"username": [true]}
{"username": ["John", true]}
{"username": {"$neq": "lalala"}}**
```

If XML is supported, check for XXE
