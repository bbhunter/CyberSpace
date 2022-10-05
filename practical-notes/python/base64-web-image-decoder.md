---
description: >-
  The script below takes the base64 value from a Web request that includes a
  base64 encoded image.
---

# Base64 Web Image decoder

<pre><code># Save the data value to a text file (image.txt) and run the script below to generate an image. 

#!/bin/python
import base64

file = open('image.txt', 'rb')
encoded_data = file.read()
file.close()

decoded_data = base64.b64decode((encoded_data))

<strong># Does not have to be png format
</strong><strong>
</strong>img_file = open('image.png','wb')
img_file.write(decoded_data)
img_file.close()</code></pre>

\


\
\
\
\


\
\
