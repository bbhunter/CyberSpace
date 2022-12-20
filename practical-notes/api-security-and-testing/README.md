---
description: This page has how to set up a home lab for training
---

# API Security and Testing

**crAPI Lab Setup**

* [ ] `mkdir /apilab`
* [ ] `cd /apilab`
* [ ] `sudo curl -o docker-compose.yml https://raw.githubusercontent.com/OWASP/crAPI/main/deploy/docker/docker-compose.yml`
* [ ] `sudo docker-compose pull`
* [ ] `sudo docker-compose -f docker-compose.yml --compatibility up -d`

crAPI Landing page will be located at http://127.0.0.1:8888 with the crAPI Mailhog Server at http://127.0.0.1:8025\
\
**vAPI lab setup**

* [ ] `mkdir /apilab`
* [ ] `cd /apilab`
* [ ] `sudo git clone https://github.com/roottusk/vapi.git`
* [ ] `cd /vapi`
* [ ] `sudo docker-compose up -d`

