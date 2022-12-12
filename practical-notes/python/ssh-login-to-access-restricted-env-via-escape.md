---
description: Invoke python at ssh login
---

# SSH login to access restricted env via escape

`ssh user@host "python -c \"import pty; pty.spawn('/bin/bash")\""`
