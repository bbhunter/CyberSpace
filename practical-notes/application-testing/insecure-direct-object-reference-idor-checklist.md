---
description: >-
  The IDOR vulnerability that arises when an application uses user-supplied
  input to access objects directly
---

# Insecure Direct Object Reference (IDOR) Checklist

* [ ] Find and replace `IDs` in urls, headers and body : `/users/01`=> `/users/02`
* [ ] Try Parameter Pollution: `users=01` => `users=01&users=02`
* [ ] Special Characters: `/users/01*` or `/users/*`  => Disclosure of every single user
* [ ] Try Older versions of API endpoints: `/api/v3/users/01` => `/api/v1/users/02`
* [ ] Add extension: `/users/01` => `/users/02.json`
* [ ] Change Request Methods: POST /users/01 => `GET, PUT, PATCH, DELETE, OPTIONS,`etc
* [ ] Check if Referer or other Headers are used to validate `IDs:`
  * [ ] `GET /users/02`                                                              \
    &#x20;  `Referer: example.com/users/`<mark style="color:red;">`01`</mark>                                     =>             `403 Forbidden`\

  *   [ ] `GET /users/02`

      `Referer: example.com/users/`<mark style="color:red;">`02`</mark>                                        =>             `200 OK`
* [ ] Encrypted IDs: If application is using encrypted IDs, try to decrypt using hashing/cracking tool
* [ ] Swap GUID with Numeric ID or email:\
  `/users/XXXXXXXX-XXXX-XXXX-XXXXXXXXXXXX`   => `/users/02` or `/users/a@b.com`
* [ ] Try GUIDs such as:\
  `00000000-0000-0000-000000000000` and `11111111-1111-1111-111111111111`
* [ ] GUID Enumeration: Try to disclose GUIDs using `Google Dorks`, `Github`, `Wayback`, `Burp history`
* [ ] If none of the GUID Enumeration methods work then try: `SignUp`, `Reset Password`, and `other endpoints` and analyze the responses. An endpoint may disclose user's GUID within the application.
* [ ] When a server responds with a 401/403, the action may still be performed. Ensure to verify the function within the application.&#x20;
* [ ] Blind IDORs: Look for endpoints/features that may disclose information&#x20;
* [ ] Chain IDOR with XSS for Account Takeovers\
