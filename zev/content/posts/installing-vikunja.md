+++
draft = false
date = 2022-12-23T17:45:17+01:00
title = "Installing a todo web app"
description = ""
slug = ""
authors = ['zev']
tags = []
categories = []
externalLink = ""
series = []
+++

Yet another project of trail and error. This one about installing a Getting Thing Done web app for me and my partner.

This is a very typical of my projects. Found cool Free and Open Source Software I could self host that would some some problems. Found it could be hosted via docker. Figured I should probably get at better setup where I have more control, so I installed a new server. This time with fedora instead of Ubuntu. This small project now got a bit larger. Anyhow, download a ISO, upload ISO to proxmox, spawn new server, login via webgui and set an IP, turn off and then on the interface. No connection. No route. Add route through the `route add` command, ssh in and set long password, reboot the machine. No longer any connection. I then remember `route` isn't percistant. I then type my long password into the web-CLI and instead use nmcli to add a default gateway. Try to upgrade but have issues with repos. No DNS configured... Adding DNS. Restart interface and  it works. Switching to a SSH connection.

After some more fiddling I got docker, portainer and Vikunja installed and working. However, had issues with the database and the frontend containers to talk to each other. In the end a password was off and a container connected to the wrong network. 

Now for putting a proxy infront of it to handle TLS and multiple sites at the same ip. For this I chose NPM proxy manager, mainly for the resons that it works from a docker image and that I'm somwewhat familiar with it. Setting up the container itself wasn't that hard, however getting the frontend of Vikunja to connect and respond to the right address was a bit of a trail and error job. I'm still not certain I understand why it did not work before, when it started working and how I could figure out this. It mainly boils down to this issue. Below is parts of the configuration for the docker container:
```
      VIKUNJA_SERVICE_FRONTENDURL: http://172.19.0.3:4322/
...
  proxy:
    image: nginx
    ports:
      - 4322:80
```

One could then guess the domain and port to put into the proxy would be 172.19.0.3:4322 but I never got this to work. Instead it seems to work good with port 80. No idea why this is. For those who guesses I've just gotten the ports switched around I've checked and [this page](https://docs.docker.com/compose/networking/) tells me that isn't the issue.

EDIT: When configuring the webserver two days after this it finally caught up to me that 4322 is a public port liked to the public IP of the underlying OS. Thus port 80 is linked to the internal IP 172.19.0.3. All I thus need to do to lock down the admin interface from the internet is to change the config and remove that port. But first I need to install a VPN so that I can reach it after that change.
```
  proxy:
    image: nginx
    ports:
      - :80
```

Finally I got it up. The NPM proxy manager comes with the benefit it solves the let's encrypt certificat for us. Thus no manual tinkering every third month. Nice! Bonus fact about Vikunja, it accepts markdown lists to be pasted in. Thus one could use templates (which is what I do in obsidian today). Thus pasting in the template below will not lead to a very weird task but rather 5 individual tasks.
```markdown
- [ ] Computer
- [ ] Charging cable
- [ ] Mouse
- [ ] External drive
- [ ] Mousepad
```

Future improvements:
* Lock down the admin interface with a VPN så that it's not reachable over the internet as it only speaks http from what i found
* See if I can change the logo out