+++
draft = true
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

Setting this up was fun, I got proxmox updated, got a new cloud up. Got calenders working. Fix fix fix. I then migrated my containers, and while doing so thought it would be good making some changes for the better. For gorcery shopping and recipes I used to run open-eats, it's been good but a bit outdated so I started looking around and found Tandoor which seems to be a alternative. Setting this up as I'm used to, which is using bind mounts does not work for this project. Trust me, I tried. After a chat in their Discord I moved from my setup to docker volumes insted, I also had to learn using .env-files. Now I'm inspired to fix all my bind mounts to volumes instead. It's been a lot of frustation and my issues aren't over yet. So far I've been blessed with the simplicity of using Nginx Proxy Manager in front of the contaiers and using that to insert TLS certificats. Howerever, Tandoor does not expose the webroot and thus doing a ACME-challenge does not work by default.