# JSON

JQ Queries

| Command                                                                                                                                                                                     | Description                                                                                                                  |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `cat vulnapp.json \| jq '.Servers[]'`                                                                                                                                                       | Retrieve the top level object (Servers array element)                                                                        |
| `cat vulnapp.json \| jq '.Servers[].Instances'`                                                                                                                                             | Access an object within an array using dot notation                                                                          |
| `cat vulnapp.json \| jq '.Servers[].Instances[]ServerType'`                                                                                                                                 | Access an individual object deeper within an array                                                                           |
| `wget -qO https://ip-ranges.cloudvendor.com/ip-ranges.json \| jq '.prefxes[] \| if .region == "country-region-1" then ip_prefixes else empty end' -r \| sort -u > country-region-range.txt` | Quietly download a list of ip ranges, use jq tp parse through the file, sort the data, and output the results to a text file |
