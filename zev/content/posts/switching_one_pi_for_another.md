+++
draft = false
date = 2023-01-22T20:37:17+01:00
title = "Switching one PI for another"
description = ""
slug = ""
authors = ['zev']
tags = []
categories = []
externalLink = ""
series = []
+++
This post could be read as a long whiny story about the difficulties of getting a simple project working. How stuff turn out to take ten times the time and resources and how you should lever host anything yourself but buy something that already works. This is of course a point that is fully valid, one could just pay it's way out of it. But I instead would like you to read it with learning in mind. This is a learning experience, this is how you get better at anything. You try, fail, learn och try again.

With that said, I often start projects not only to learn but also to solve some issue. In this case, we have a raspberry 3b+ at home which runs two docker containers. One for Ubiquity and one for homeassistant. This was never really meant as a long-term solution. When I bought our AP I did not realize I needed a controller to use it at all, I thought some config via SSH would be good enough but never got it to work with my then firewall/router. So I found you could run a container on a raspberry and got it working. Later I added homeassistant to build a wake up lamp. Today we still run out network on that PI and our one wakeup light have now become at least half the lights in the apartment. The other day I saw one of my containers aren't updating as supposed to. I did some digging and found [this](https://info.linuxserver.io/issues/2021-11-25-unifi/):

![](/images/unifi_out_of_support.png)

I do realize I had some options. These would be upgrading my PI to a 64-bit system, I could find another docker image which keeps support up for 32 bit, I also could buy new hardware and migrate. I choose the later, mainly for two reasons. Firstly the SD-card in the PI failed once, that meant no internet and no turning lamps on and off before I had fixed the issue. I had no backup of the card as this used to be an experiment. Thus all Zigbee devices had to be re-paired, network had to be rebuilt and so on. It was a long night to say the least. Secondly migrating instead of switching meant I can more easily switch back if needed. Something I think my partner will apprichiate.

So new hardware? But what to choose? Well, raspberrys inventory says -1700 and there are no rumors of new pi's comming any time soon so that seems to be a bad bet. Instead I found the Rock 4. One of many raspberry pi inspired single board computers. This has more the specifications of a raspberry pi 4, has a faster CPU, more ram, and a M.2 NVME port. It's a bout three times as expensive as the raspberry Pi was but were still talking about a computer for just over 100 euros.

Once I got the Rock I quickly found my first problem. If I fit a NVME on the board it will stick out like a tail, if it was flipped it would be so close to the CPU it would probably cook so I understand why they did this, I just did not look at it closly enough when ordering. I also can't really have it that way is I will snap the drive by accident eventually. They do thankfully sell a raser board which bridges the port up to a new PCB. It's a less nice solution but it's a solution. As no Swedish stores has any ones home I hade to make an order off AliExpress. Never done that before so we'll need to see how it goes. Meanwhile we can create a temp board on a nylon cutting board to get started.

Second problem, black screen. I downloaded the software and flashed it to a USB, plugged that in and booten the board. No screen, nothing. Tested this on two separat monitors, no luck. Read a bit on the wiki, figured out it was one of tho things. Either the board is broken, or it simply lacks a bios and thus can't be booted over a usb-device. The later one is simpler to test. I instead flash the SD card with the image again and TADA! It works! This brings new questions, what happens if more then one plugged in media has an OS? In what order will it check? Where will it check? Can I run the OS from my NVME-drive? How would I then install it?

I found two ways of installing the image on the drive. I either, switched one of my drives on my motherboard of my desktop out and tried to flash it that way. I wasn't to keen in this solution as it's a lot of hassle. I instead opted to install the drive in a USB-inclosure and install it that way. This brough new issues. The write fails. It could be many things, let's try to list some hypothosis and see if we can exclude any of them:
- The drive is to large for the image
- You can't install the image on an external device connected via USB
- The program I use for flashing contains some bug
- The drive is broken
- The drive is incompatable
- I ran into some weird software bug that rarly happens

The later we can test, update all software, reboot the PC and run it again, some outcome. Download a different OS and try flashing that instead, same issue. Problably not the issue.

The program could contain some bug. Let's switch from Fedora (my OS of choice at the moment) and Etcher to Windows and Rufus. Let's also reformat the drive to make sure it works as smooth as possible and does not try to write to some smaller partition.

When getting here I instead google a bit and realized the hardware I've bought wont really work the way I hoped ([Source](https://forum.radxa.com/t/rock-4-se-nvme-boot/11621)).

![](/home/zev/Documents/zev.se/zev/static/images/rock_4_se_no_support_for_os_on_ssd.png)

I thus have two choices, either run the device from the SD-card or find a new use for it and instead buy more new hardware. For now I'm opting for the first and instead use the SSD I had lying around for a new media PC that will probalby run on a SBC with a SPI flash memory.

This is clearly a setback but we're not aming to win all battles but instead winning the war. We now have a computer with a OS on. Time to install software!

For this we will need to install docker and a handfull docker images, namly portainer (because I'm lazy), home-assistant, unifi-controller and wireguard. There are plenty of guides on how to do this so I'll skip over the details but basically I add a extra network on all containers, to ensure we have access when connected via VPN. We must route this network in the wireguard client config as I'm setting this up as a split tunnel to run most traffic outside of it. Once setup we aim to have a setup looking like this:

![[/images/vpn_network_drawing 1.png]]

The above part of this blogpost was written just before the Christmas break. I will try to summerize what has happend since as well as I can. For the most parts things has gone as expected. I brought the Rock Pi and installed docker, Portainer Enterprise Edition, a handfull containers and a few bits and bobs while gone. Most things went just as expected. I did not have a copy of the old containers with me so for that part I could only go as far as actually setting things up in the default configuration. So far so good. The only larger danger I saw was the migration between home assistant images. When setting up the old PI I choose the [raspberrypi3-homeassistant](https://hub.docker.com/r/homeassistant/raspberrypi3-homeassistant/) image. I wanted to move that to INCERT VERSION image instead. Other then another Portainer installation on a server not much could be done before I came home again and so nothing more happened during the break.

Once back I found out a couple of interesting details that set this operation back by a bit. First and formost, the last time I set this up I was in a bit of a hurry and thus dumped all files into the same directory making a mess. This means unifi and home-assistant files were hard to separate. Secondly it seems the different home-assistant containers stores files a bit differently, simply replacing the files in the new containers config-folder with the files from the last one lead to a state where I could not login. I decided to go the hard route and redo home-assistant in a better manner instead of trying to save and migrate what was setup in a rush. This meant resyncing all zigbee devices, something that, due to a batterypack and an external wifi antenna wasn't as hard as I first imagined it would have been. I simply ran the Rock Pi from a battery pack and connected to it via the Wifi, thus I had a compact package I could carry around and place next to whatever needed to be synced. With a laptop I could give everything names and start controlling them. One room at a time the zigbee network got setup.

Instead of making automations that turned off and on every device one by one I used the group feature that used to only be accessable via the terminal. I also used helpers to turn our Ikea Trådfri smart plugs into lights. This essentially menas I can choose these as i light and thus create a group of lights with them. With a few groups and some config most of our buttons are now also up and running. Most importantly the remote that tunrn everything off.

For my Unify gateway I had larger issues. The problem here is, how do you migrate the controller of the network if you can only access the controller over the network? It's a bit of a catch 22 but in the end what worked for me was first backing up the config via the GUI in the old controller, then releasing the lease of the controller IP and removing the controller from the network. Then (via a temporary IP still assigned to the new controller) login to that and first uploading the configuration backup to the container and then assigning the old controllers IP as a static IP in the underlying operating system and rebooting. This works because the controller and the gateway are separat hardware. I'm a bit surprised it was as painless as it was but I guess we'll just celebrate that small win and move on.

While on vacation I installed a duckDNS container and a wireguard container. DuckDNS basically updates a DNS-recond every x minutes with whatever public IP it now has via an agent. Thus my ISP switch IP:s every now and then is no longer an issue. Wireguard is a VPN-server, meaning I can connect home if gone. The only part left here was a port forward in the new controller. Your home router normally blocks any sessions established from the outside (the internet) but in this case if the connection is made to this specific port the traffic will be let through to the Rock Pi and that can then decide what to do with it. If you have the correct configuration and matching keys you're allowed to connect.


Later projects:
- Add some proxy manager to handle DNS-names and get this to work through the wireguard client
- Backup of all data and configuration
- Version controll of stack configuration through private github repo? I agree this is giving out my data but it becomes a catch 22 if I host my own git that then requires the files in the git to set it up
- Buy and install backup card in case of disaster
- Auto update of containers

Lessons learned:
- Hardware and specs aren't easy
- Not all Raspberry pi looking SBC's are the same
- Not all SBC's have SPI flash and some kind of BIOS
- Direction of ports are important