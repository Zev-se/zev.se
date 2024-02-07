+++
draft = false
date = 2024-01-22T14:53:17+01:00
title = "Lerning more about docker volumes"
description = ""
slug = ""
authors = ['zev']
tags = []
categories = []
externalLink = ""
series = []
+++

This project wasn't meant to happen. Niether was it supposed to learn more about containers. It all started with a crashed harddrive. I changed it out but something went wrong in one of the VM:s and all of a sudden a had a crashed cloud. This was probably almost a year ago. It's been a long ride but long story short getting the VM back up and running was a no go. As theres terrabytes of data just moving stuff is also hard. The data seemed to be okay but given I don't know and theres tens of thousends of files it's hard checking that all is good. I did try running a vm and seeing if I could get the database back up to extract everything but the files. In the end the only data I really needed was the calendar which I could export from the phones who had it synced before it all crashed. In all of this I also got ahold of a new, better, smaller server. So not only is it time to fix this issue but it's also time to migrate to new hardware.

Setting this up was fun, I got proxmox updated, got a new cloud up. Got calenders working. Fix fix fix. I then migrated my containers, and while doing so thought it would be good making some changes for the better. For gorcery shopping and recipes I used to run open-eats, it's been good but a bit outdated so I started looking around and found [Tandoor](https://github.com/TandoorRecipes/recipes) which seems to be a alternative. Setting this up as I'm used to, which is using bind mounts does not work for this project. Trust me, I tried. After a chat in their [Discord](https://discord.gg/RhzBrfWgtp) I moved from my setup to docker volumes insted, I also had to learn using .env-files. Now I'm inspired to fix all my bind mounts to volumes instead. It's been a lot of frustation and my issues aren't over yet. So far I've been blessed with the simplicity of using Nginx Proxy Manager in front of the contaiers and using that to insert TLS certificats. Howerever, Tandoor does not seem to work with Nginx Proxy Manager, and I've growe a bit tired of the manual work. Thus I decided to take the leep over to [SWAG](https://docs.linuxserver.io/general/swag/). I've now gotten this to work. As I haven't found any good documentation of how to set this up given you don't run SWAG in the same stack I thought I'd share my configs. They are listed below.

For this to work I needed to create two DNS-entries manually. Not sure how the second one was handled by Nginx Proxy Manager. This took a few tries to figure out.

#### DNS
`A-record:   Tandoor.domain.tld <IP>`
`CAA-record: tandoor.domain.tld <0 issue "letsencrypt.org">`

#### SWAG docker

###### SWAG compose file

Do note I have a main site (the one you're on) and several subdomains in thes config. If you only run tandoor, put that whole domain in the URL row and remove or comment out the SUBDOMAIN row.
```yaml
---
version: "3.8"
services:
  swag:
    image: lscr.io/linuxserver/swag
    container_name: swag
    cap_add:
      - NET_ADMIN
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Stockholm
      - URL=<CHANGE ME>
      - SUBDOMAINS=tandoor,
      - VALIDATION=http
      - EMAIL=<CHANGE ME>
      - DEBUG=True
    volumes:
      - config:/config
    ports:
      - 443:443
      - 80:80
    restart: unless-stopped
    
volumes:
  config:
```

Tandoor nginx-file. Place this in /path/to/volumes/swag_config/_data/nginx/site-confs/tandoor.domain.tld.conf. In my case this lives in /var/lib/docker/volumes/swag_config/_data/nginx/site-conf.

When the file is modified and saved make sure to restart the SWAG container and check container logs for failures, I do this through portainer.

```bash
server {
  listen 443 ssl http2;
  listen [::]:443 ssl http2;

  server_name tandoor.*; #If your site is called something else then tandoor change this

  include /config/nginx/ssl.conf;

  client_max_body_size 0;

  location / {
    include /config/nginx/proxy.conf;
    include /config/nginx/resolver.conf;
    set $upstream_app tandoor-nginx_recipes-1; #This is the name of the tandoor nginx container
    set $upstream_port 80;
    set $upstream_proto http;
    proxy_pass $upstream_proto://$upstream_app:$upstream_port;
  }
}

```

#### Tandoor docker

Do note:
- I use portainer and import the env-file. Thus the env_file is called stack.env.
- The swag_default network is created by the SWAG stack, thus it needs to be started before this stack for this to work.

###### Tandoor
```yaml
---
version: "3.8"
services:
  db_recipes:
    restart: always
    image: postgres:15-alpine
    volumes:
      - postgresql:/var/lib/postgresql/data
    env_file:
      - stack.env

  web_recipes:
    restart: always
    image: vabene1111/recipes
    env_file:
      - stack.env
    volumes:
      - staticfiles:/opt/recipes/staticfiles
      # Do not make this a bind mount, see https://docs.tandoor.dev/install/docker/#volumes-vs-bind-mounts
      - nginx_config:/opt/recipes/nginx/conf.d
      - mediafiles:/opt/recipes/mediafiles
    depends_on:
      - db_recipes

  nginx_recipes:
    image: nginx:mainline-alpine
    restart: always
    networks:
      - default
      - swag_default
    ports:
      - :80
    env_file:
      - stack.env
    depends_on:
      - web_recipes
    volumes:
      # Do not make this a bind mount, see https://docs.tandoor.dev/install/docker/#volumes-vs-bind-mounts
      - nginx_config:/etc/nginx/conf.d:ro
      - staticfiles:/static:ro
      - mediafiles:/media:ro

volumes:
  nginx_config:
  staticfiles:
  mediafiles:
  postgresql:

networks:
   swag_default:
      external: true
```

###### Tandoor .env-file
```env
SECRET_KEY=<CHANGE ME>
DB_ENGINE=django.db.backends.postgresql
POSTGRES_HOST=db_recipes
POSTGRES_DB=djangodb
POSTGRES_PORT=5432
POSTGRES_USER=djangouser
POSTGRES_PASSWORD=<CHANGE ME>
```

If you later want to add other subdomains to other stacks, just add the subdomain to the SWAG stack configuration, create a copy of the nginx config and add the two records. Reboot the SWAG container. Make sure the new containers are part of the swag_default network and that the port in the ngix config is correct. Good luck!