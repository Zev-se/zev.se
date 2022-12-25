---
title: "Getting Started"
date: 2022-12-25T17:45:17+01:00
draft: false
---

# blogpost_getstarted
Parent: 
Tags: 

---

So I thought I would not publish yet. I still have no logo, the first page isn't modified yet, not sure I like the font sizes and spacing. But then I realized, thsi is the exact oposite of what this page is supposed to be. I'm trying to get things good and polished before publishing when this page in fact is for all the half done, good enough projects. The proof-of-concept, might fix later-projects. So here we go, this is what you'll get and if, when you read this, the page has a logo there's probably a post about designing it.

To get this page up I found XXX. It can also be hosted via Docker. So it should be fairly simple. The modified codes looks like this (note this is wrong and will be changed further down):

```
version: "3.3"

services:
  web:
    image: joseluisq/static-web-server:2
    environment:
      - SERVER_HOST=127.0.0.1
      - SERVER_PORT=1111
      - SERVER_ROOT=/public
    volumes:
      - /opt/docker-data/www-public:/public
    networks:
      - npm-proxy

networks:
  npm-proxy:
    external: true
```

Original code can be found here: https://sws.joseluisq.net/features/docker/#docker-compose

Now time to modify the DNS record of my provider to point towards my VM:s public IP (the VM is the underlying OS the docker images runs on). We also need to configure the proxy to point towards the correct internal IP. That IP can be found under the container in portainer.

We now have a bit of a DNS issue. The DNS was earlier pointed at another IP, thus it is cashed. Not only in our system but also upstream. Even when changed it will take up to a day before the change is fully applied everywhere. It will work for all ISP:s which did not previously have it in their cashe but I did ping it earlier so my only hope is to override the upstream server sonfig with my local one. We'll add `193.11.113.26 zev.se` to `/etc/hosts` on a new line. Then try it out:

```bash
➜  ~ dig zev.se 

; <<>> DiG 9.18.8 <<>> zev.se
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 9703
;; flags: qr aa rd ra ad; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;zev.se.				IN	A

;; ANSWER SECTION:
zev.se.			0	IN	A	193.11.114.26

;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Sun Dec 25 10:50:56 CET 2022
;; MSG SIZE  rcvd: 51

➜  ~ 
```

Seems to work. Let's now work on portainer. We can see the docker image has gotten a IP in our network, this printscreen is from the stack view for anyone wondering.
![[Pasted image 20221225105323.png]]
Time to get this into our NPM-manager. 
![[Pasted image 20221225111244.png]]

It simply won't work. So I started digging. Found some errors in the docker-compose file. One way to test this is to curl from the terminal of the server. The NPM network is reachable so if it does not respond there it's not a proxy issue but a configuration error in the container. This however seems to work:
```bash
version: "3.8"

services:
  web:
    image: joseluisq/static-web-server:2
    environment:
      - SERVER_PORT=80
    volumes:
      - /opt/docker-data/www-public:/public
    networks:
      - npm-proxy
    ports:
      - :80

networks:
  npm-proxy:
    external: true
```

We can now again turn to our proxy manager. Changing mainly port.
![[Pasted image 20221225111511.png]]

Lets add TLS. This is honestly the best part of the proxy, we can simply turn TLS with Let's Encrypt on. Fantastic!
![[Pasted image 20221225172840.png]]
![[Pasted image 20221225173006.png]]

So finally time to compile the webpage and get things up and running. I've used GoHugo and use Github to keep track of it. As I'm lazy let's write a small script that does most things for us:

```bash
#!/bin/bash
cd ~/zev.se
git pull
hugo -d ~/site-tmp/
read -p "Are you sure? " -n 1 -r
echo    # new line
if [[ $REPLY =~ ^[Nn]$ ]]
then
	echo "Quitting"
    break;
fi
if [[ $REPLY =~ ^[Yy]$ ]]
then
    # move old files to backup
    zip -jr ~/www-backup/"$(date '+%F-%T').zip" /opt/docker-data/www-public
    rm -r /opt/docker-data/www-public/*
    # Move compiled page to /opt/docker-data/www-public
    cp -r ~/site-tmp/* /opt/docker-data/www-public/
    echo "please reboot docker image in portainer"
    read -p "press Enter to continue"
    rm -r ~/site-tmp/
fi
```
