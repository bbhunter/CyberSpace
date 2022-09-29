---
description: >-
  The script below takes the base64 value from a Web request that includes a
  base64 encoded image.
---

# Base64 Web Image decoder

\#`Save the data value to a text file (image.txt) and run the script below to generate an image.` \
\
`#!/bin/python`\
`import base64`\
``\
`file = open('image.txt', 'rb')`\
`encoded_`_`data = file.read()`_\
_`file.close()`_\
_``_\
_`decoded_data = base64.b64decode((encodeddata))`_\
_``_\
_`img_file = open('image.png','wb')`_\
_`img_file.write(decoded_data)`_\
_`img_file.close()`_\


\
\
\
\


\
\
