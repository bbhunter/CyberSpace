# JSON

JQ Queries

| Command                                                     | Description                                           |
| ----------------------------------------------------------- | ----------------------------------------------------- |
| `cat vulnapp.json \| jq '.Servers[]'`                       | Retrieve the top level object (Servers array element) |
| `cat vulnapp.json \| jq '.Servers[].Instances'`             | Access an object within an array using dot notation   |
| `cat vulnapp.json \| jq '.Servers[].Instances[]ServerType'` | Access an individual object deeper within an array    |
