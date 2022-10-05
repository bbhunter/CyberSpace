# Password Generator

```
# Random Password generator. Insert additional characters as desired

import os

Characters = "aAbBcC3dDeEfFg9GHh2IiJjK8kLlM0m4N&nOoPpQq7RrSs1Tt#5UuVvWwXxYy6Zz"
Length = int(input("Length: "))

urandom = os.urandom(Length)
Index = ""
for i in range(Length):
    Index+=Characters[ord(os.urandom(1)) % len(Characters)]

print(Index)
```
