+++
draft = false
date = 2023-01-22T22:00:17+01:00
title = "A few hours at the makerspace"
description = ""
slug = ""
authors = ['zev']
tags = []
categories = []
externalLink = ""
series = []
+++

This is mainy a quick note about a day at the local makerspace. Today my plan was to get as many of the things on my list done as possible but in a specific order. First and formost I needed a case for my new Rock Pi-E. Yet another one you may ask? Why so? Well this one is to be used as a proxy for the ILO (integrated lights out) interface on my server. It's one of those embarrassing TO-DOs that I've for too long held off fixing. Today the ILO-card has a public IP and is end-of-life since a few years ago. This is bad as it could give access to the server, especailly of you had a zero-day. The ILO-card itself is a small signle board computer where you can connect to and manage the server. See it as a KVM-Switch ofeter ethernet, a remote window and mouse and keyboard access to the servers terminal. You can also reboot it from there and possibly reinstall it. Now that is no easy task as it requires very old JRE (Java Runtime Envionment) and a internet explorer brower will all security features turned off but it's still possible (I should know as I've done it a few times). It's still password protected, both in the ILO-card and on the host but yet I feel it probably should not be on the internet. Thus I've bought a Rock with two ethernet interfaces, so that I can run VPN to it and then run the ILO on a local interface once connected. TO protect the board I needed a case and in this case (pun inteded) the easiest way was to just 3d-print one. I choose this horrible color because the filament was lying around and this will sitt in a serverhall no one ever visits. Thus ugly case isn't a problem.

Secoundly, my parents need a new sign for there postbox. I quickly made a design in Inkscape and tried to import that in lightburn, which is the program we run our lasercutter from. But everytime it crashed. I then instead saved it as a png and imported it that way. More luck this time. I won't show their names and address but heres another part of the design. The idea is to paint it black and then do the infill with white. So this project is half done.

![](/images/laser-cut-mail-box-plate.jpg)

While I was there I also painted some covers for my Apple watch black. I could only get them in rose gold which isn't really my color but I need then for climbing as I don't wat to scratch the glass. It does not need to be perfect so spray paint it is. Worked out good enough. Not something I would have on for client meetings but better then tapeing the screen which is what I've done before.

![](/images/watch-screen-protector.jpg)

Now here's where we run into the first of three issues for the day. I wanted to switch filament in the 3D-printer to print holders for electric toothbrushes, in this case neon-green was not a good fit. Thus I tried to switch the filament, but here something happened. All of a sudden the nossle wasn't getting any heat. Spent an hour or so on tinkering with it finding out what was wrong. Found a cable that had broken off, a head resistant cable that you simply can't solder (I tried). Need to order a new one and install that. I insted spent some time cleening up the head. and putting that to the side for now. Informing others in our Slack it's out of order for now. Thus no Toothbrush holder.

![](/images/broken_3d-printer.jpg)

I also need to fix some case for my Rock Pi 4SE (as I've already broken one, more on that in a later blogpost). I tried to get this quick and dirty way by just copying a raspberry svg-file and changing the placement of the holes plus adding a cutout for the CPU. However, somewhere the dimentions got messed up and it became 20-isch percent to large. Guess I'll have to spend some time on doing it the correct route and create a real svg and uploading it to thingiverse. But I did not have time for that today.

![](/images/rock-pi-e-case.jpg)

Finally on makerspace I raced to get a new wallet cut out. Mine is fine but falling apart. I made it as a proof of concept a year or two back, and really like it. However the stitching isn't very nice, the edges are inconsistant to say the least and the holes don't really line up. However, there simply wan't time to finnish, the svg is done by I also need to get the settings in the lasercutter to be correct for the leather I will use. I guess this will be a separat blogpost as well.

Well home I started to prepare for server fix this weekend. I got a new external drive of 3TB to replace the broken one, only to discover that this external drive not consisting of an internal drive and a PCB but rather a specially designed drive including the USB-interface. As 3TB drives are hard to get ahold off I will insted have to mount a 5TB drive I have lying around. It's a bit sad as 2TB of it wont be used but there's not much to do. You live and you learn. Drives shorter then 120mm I would be suspicius of in the future. Below are some pictures that Illustrates what I mean. In this case the specially designed drive is a Western Digital (WDBU6Y0030BBK-WESN).

![](/images/old_drive.jpg)
Old type of drive

![](/images/new_drive.jpg)
New drive
