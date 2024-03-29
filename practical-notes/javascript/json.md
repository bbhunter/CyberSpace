# JSON

**Manipulating JWTs**

1. Paste the token into jwt.io
2. Replace the "alg" value with "none" in header. (try the alg header variations such as "none", "None", "nOnE", "NONE".)
3. Replace arbitrary values of the payload e.g. "username" with "admin".
4. Empty the signature field

If the error "Invalid Signature" occured, we can manually create Base64 value for each section (remove the "=" symbol). If you want to empty the signature field manually, you can delete the final section.

5. Now copy the JWT.&#x20;
6. Go to the website and replace the original JWT with the new one in HTTP header.

**Changing Expiration**

During JWT testing, you should try to modify the "exp" value:

`"exp": 1679156071 -> 991679156071`

**JQ Queries**

| Command                                                     | Description                                           |
| ----------------------------------------------------------- | ----------------------------------------------------- |
| `cat vulnapp.json \| jq '.Servers[]'`                       | Retrieve the top level object (Servers array element) |
| `cat vulnapp.json \| jq '.Servers[].Instances'`             | Access an object within an array using dot notation   |
| `cat vulnapp.json \| jq '.Servers[].Instances[]ServerType'` | Access an individual object deeper within an array    |

Quietly download a list of ip ranges, use jq tp parse through the file, sort the data, and output the results to a text file

```
wget -qO https://ip-ranges.cloudvendor.com/ip-ranges.json | jq '.prefxes[] | if .region == "country-region-1" then ip_prefixes else empty end' -r | sort -u > country-region-range.txt
```
