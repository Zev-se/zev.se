+++
draft = false
date = 2024-03-17T17:00:17+01:00
title = "Building a Voron 2.4"
description = ""
slug = ""
authors = ['zev']
tags = []
categories = []
externalLink = ""
series = []
+++

I had so many issues with my old small 3D printer I decided it was time to upgrade. I spent more time on fixing issues then printing and it got frustrating really fast so here we are. I bought a Formbot kit in the end of January. It has been sitting in it's box for a bit more then a month but this week was finally that week. This post will be a list of issues I found with the build, where the instructions simply were wrong or where I found it to be hard to follow. But to put this into context this build has for the most part been a lot of fun and of several hundred pages of documentations there are a few where things got unclear. The Voron team both surprise me of how well put together this is and inspire me. Vivedino (the company behind the formbot kit) has put together an amazing kit, I just wish they spent a few hours on the documentation. With that said let's begin, but first things first. Credit where credit is due. This build would not have gone as well as it did if it wasn't for the amazing helt of people on the Voron and Formbot Discord (do note most problems I could solve by just searching in the discord channels, please try this first). Here's a list of people I would like to thank:

Formbot Discord:
- cashmoney
- Browzzrr V2.6568
- unkown
- ĴînRΦђ V2⁶²⁵⁷ | M⁰⁸¹
- Everest V2.6256 VT V0 ERCF
- Zv0n

Voron Discord:
- Troglomike
- rec
- ZeroBrain | V0 VT
- Hagbard V2.1070
- MemorableC V2.1002

I also watched a bunch of youtubers, for inspiration before buying and also to help me understand where things were a tiny bit unclear. As I don't have a complete list I wont include it but Voron-youtube, thanks!

Last but not least course a huge thanks to the Voron team!


I used a long list of tools to get this kit together. If you're not a DIY person with a pasion think twice before entering this journey. There's no complete bill of tools needed. Mostly because it varies what you need. For instance I needed drillbits to fix a few holes a fraction to small(see image below). If you self source everything you will need a JST-crimping tool. There is a tools tab on the sourcing guide but it's not complete. What you will need no matter what is a nice set of ball head hex key, trust me, you will use this so much is worth getting.
![](/images/tolarance_too_small.jpeg)

If (when) I'm to do this again, I will also spend a few bucks on some plastic sorters. Dealing with screws in ziplock-bags got old very quickly. Anything will do but I would probably buy something along the one below. If they have loose compartments use some hotglue to save yourself from dealing with walls getting loose,

![](/images/sortment_box.jpg)
![](/images/screws_in_bags.jpeg)

#### Jumping between different PDF:s
It's a bit hard to know where to jump when, there are at least four different PDF:s you will need, plus an image of your controller board with all pins listed (this is linked on the voron guide on page 178). The PDF's are:
- (The Voron 2.4R2 Assembly Manual)[https://github.com/VoronDesign/Voron-2/raw/Voron2.4/Manual/Assembly_Manual_2.4r2.pdf]
- (The Stealthburner Assembly Manual)[https://github.com/VoronDesign/Voron-Stealthburner/raw/main/Manual/Assembly_Manual_SB.pdf]
- (The Voron Tap Assembly Manual)[https://github.com/VoronDesign/Voron-Tap/blob/main/Manual/Assembly_Manual_Tap.pdf]
- (The Formbot wiering guide)[https://drive.google.com/file/d/19wdkwaP-MP6JrulkZ-r0Kav1kbvxzPzk/view?usp=sharing]

I'll try summerising the jumps here:
- Start with the Voron 2.4R2 PDF
- At page 30 turn the DIN-rails 90 degres (if Formbot, we'll get to why later) then continue
- At page 39, if you build a 300x300 Formbot turn one of the motors 90 degrese so that the cable is on the same side as the two screws of the bracket, this will be Z1 later
- At page 129 jump to the Voron TAP pdf and build that, the version of tap is slightly different see below. At page 31 of the TAP PDF go back to the Voron 2.4R2 PDF and do steps on page 131 through 142, then go back and finnish the TAP instructions tightening the belts
- Now go to the stealthburner PDF and do that top to page 58, note cabeling will be different, for this check the Formbot wiering PDF, also note there are two different dimentions of PTFE tube included, choose the correct one. Then go back to page 148 of the Voron 2.4R2 instructions
- Do page 150 through 157, but don't mount anything. Also note there's no 5V PSU but instead a extra PCB
- Jump to page 162 and follow along through page 167
- Jump to page 175 and follow along to page 177
- Now switch to page one of the Formbot Wiering instructions, mount the components as shown on the image, note that is the 350x350 so if you build a smaller printer it will be tighter. There's a picture further down in this blog-post with what is what.
- Jump back to the Voron V2.4R2 PDF at page 180 and follow along, this won't be 100% correct as there's no 5V PSU and there's an extra PCB, be carefull here.
- When at page 194 mount cables in chains before mounting chains as it will be hard to do otherwise. Also don't forgett the extra LED cable which is separat from the other cable (if your kit is newer then mine it's sold with CAN-bus and this will be totally different as you probably won't have cable chains at all)
- On page 200 the B-motor cable is routed in the grove under the gantry with a plastic strip instead of zipties
- When you have attached the last few cables you are mostly done with what you can do now, don't forgett to download and install the Big tree tech PI version and from it flash the octopus board via the other smaller included SD-card.
- Now follow the post build instructions to make sure you've done everything correct

#### Notes from the build

##### The printed parts kit from Formbot
As my old printer had acted up I decided to buy a kit of parts from formbot (instead of using the print it forward program). This kit was mostly fine but there are three templates used when mounting the rails on the extrusion. I'm guessing most people who buy this kit of printed parts don't have a working printer at the moment. It would be nice if these were included. I guess some would have a printer that could print these in PLA but still. It's three very small parts to include I would happily pay an extra few bucks for. They are referenced as MGN12_rail_guide_x2.stl and MGN9_rail_guide_x2.stl and pulley_jig.stl in the Voron build guide.

A quick note about that (kit)[https://www.formbot3d.com/products/high-quality-3d-printed-parts-for-voron-24-pro-kit?VariantsId=11047], it also would be nice if they linked what filament they used so that one could print new matching parts when done.

One of these printed parts was I bit to tight. The part holds the gantry together. One of the A-B belt weels got too pinched. This happens, the tolarances are very fine. I shimed the part with two layers of craft paper and it now works perfectly.

The bracket for the cables between the smaller cable chains shown on page 204 of the Voron 2.4R2 PDF was a bit to tight, I used a drillbit and just removed some plastic by hand. It's also hard to cram all cables and a cable sleeve into, if I did not plan on modding the printer with a canbus I would probalby redesign this.

The Voron Tap plate seems to be of a different kind. Not sure if this is a old revision or if this is some custom Formbot thing. See image below.
![](/images/SB_mount.jpg)

Original tap design:
![](/images/SB_original_mount.png)

The tap plate also did not have the cone guiding you to the correct depth of the heatset incerts. Not sure why this has been changed.
![](/images/tap_unclear_depth_heatset_incertsjpeg)

How the original STL looks:
![](/images/tap_cone-png)

Bending the mounts with a screwdriver helped with negitioating them to bend the way they need to.
![](/images/sitff_mount_tip.jpeg)

###### Positives with the Formbot kit
The driver assembly shown on page 21 of the Stealthburner PDF came pre assembled which is nice.

The neopixels on page 46 of the Stealthburner PDF came pre-soldered which was nice.

###### Larger issues
The mounting of the DIN rails are different in the Voron setup. This was by far the most anoying thing in the whole build. I ofcourse did not notice this before trying to mounting the A and B motor cables. I had then spent some time tidying thing up. Had to redo everything. Also one of the motors has to be turned for the PSU to fit. I have no idea why they choce to do it this way nor why the documentations is so poor. It just seems odd to not make this very clear and spend some time making sure the electrical configuration guide is very clear. In frustration I asked about this on the Discord but mostly got a "everyone knows the documentation from Formbot sucks". I hope the new kits will force an update. I will also email about this. If there's a response I'll update this page.

This is what the Voron guide says on page, note where front and back is.
![](/images/voron_din_rails_mount.png)

This is the first page of the Formbot wiring, this is where your supposed to see that you've mounted the DIN-rails wring some 100 page earlier.
![](/images/voron_din_rails_mount.png)

This lead to everything needing remounting, you could probably smell the frustration
![](/images/din_rails_original_mount.jpeg)
![](/images/remounting.jpeg)
![](/images/Electrics_mounted.jpeg)

Here's the problem with the morots on the 300x300 size.
![](/images/motor_cables_not_fitting.jpeg)

No mention to also drag neopixel cable, this you will probably find out after you've mounted everything making you have to redo the cable chains. If you have an octopus V1.1 it should be routed to the led pins, there should be three, this cable should be connected to the two on the USB-port side, with the 5V being closest to that side. They share ground with the rest of the board so that cable isn't needed.

###### Minor issues
In the kit the M3x10 BHCS screws are missing. I replaced these with the M3x12 BHCS. I was a bit affraid I might regrett this when they are needed later but so far I'm not sure where they are used. The Formbot-kit also seems to include a few extra of every screw which is very nice.

The arm to cables mounted on the back of the Clockwork 2 is the wrong color. Not a big deal, just be aware when looking for it.

On page 28 of the Stealthburner PDF, it's not clear which way the motor is supposed to be mounted, I did mine the same way the video linked on that page showed.

The original CW2 latch broke, this is a known issue. I hope to voron team redesigns this. If you have access to a printer, or a friend with a printer ask them to print a replacement (a reinforced replacement, i printed (this one)[https://www.printables.com/model/508340-updated-latch-for-voron-stealthburner-clockwork-2-]) before you even start, this could be PLA for now, it's good enough. Just make sure to print a new one in ABS ASAP. 
![](/images/broken_latch.jpeg)
One of the stepper-driver's heatsink was missing it's sticky thermal pad. This is a BTT QA issue and has nothing to do with Formbot. I solved this with some tape and thermal paste for now. I've ordered the correct tape to change it with whenever that arrives.
![](/images/missing_heat_sink_pad.jpeg)
The split ground cable is a bit to short to make the routing nice, it also is to small to fit the screw so to make it fit one has to cut it.
![](earth_too_short.jpeg)
All screws in the kit are stainless steal, it's nice for everything but on page 27 of the TAP manual. The two M3x6 FHCS needs to me magnetic. I had to find my own and change these out.
![](/images/replaced_screws.jpeg)

The cable below is wrongly labled. It should say "Power to BED-Power". In later kits they've solved this with a sharpie.
![](wrongly_labled_cable.jpeg)

###### Notes

For anyone new here's a breakdown of what is what.
![](/images/what_is_what.png)
RED - Motor turned 90 degrees (see more further down)
PINK - This is the on off switch for the heated bed, it's not an invertor as one might think. In the Voron documentation this is called the AC BED CONTROL.
YELLOW - PSU, the powersupply. In the Voron documentation this is called the LRS-200-24 PSU.
GREEN - RASPBERRY PI.
DARK BLUE - Controller. This board controlles the motors and is basically a break out board. Before Klipper this board used to run on Marlin and there was no PI. It's a bit confusing. Just know this is refered to as the CONTROLLER BOARD in the Voron documentation.
LIGHT BLUE - Break out board (this is replaced with canbus is later kits)
ORANGE - This is Formbots own PCB, in the Voron documentation this is the same as using the WAGO clamps.

The plastic bracket included in the kit which is for a SBB EBB board isn't needed. Just skip this.

To mount the SBB EBB break out board i used M3x6 screws from the kit.

The Bearings on page 17 of the Stealthburner PDF are different from the ones in the kit. Not a problem, just be aware.
![](/images/other_bearings.jpeg)

There's no z endstop included because of TAP, there's also no 5V PSU included because the BTT PI runs on 24V. Not a problem, just be aware so you don't spend time searching for items that simply aren't there.

On page 163 one of the Voron 2.4R2 PDF the limit switches are installed a different way then the once in the kit, this does not make a difference, it's just a bit confusing.
![](/images/voron_limit_switch.png)
![](/images/wrongly_mounted_switch.jpeg)

I found it to be unclear how many of what panel mounts are needed. But the STLs actually says that I noticed later. For instance bottom_panel_clip_x4.stl, the x4 is the about needed. I printed these in PLA for now. I need the panels to print ABS so it's a bit of a catch 22.

The cable chains are a bit too long, you can remove links so this really isn't an issue. Rather nice having a few extra. A tip is to mount the ends separatly and connect them once all the cables are inside (as the part that closes will face down towards the 20x20 extrusion).
![](/images/Cable_chain_too_long.jpeg)
![](/images/cable_chain_tip.jpeg)

From what I remember, the kit said to include a nevermore filter. It dosen't. It does include some hardware, fans, coal, WAGO-clips, a cable, some screws. But it does not include the plastic parts. This is a bit of an issue. I would want the filter to print ABS, but to print ABS I want that filter. I opted to first print all panel clips in PLA and then print the nevermore parts it with a window open. The printer isn't tuned properly but I also don't want to do that without the filter. So this is good enough for now. When the printer is tuned I will reprint this. I can also say mounting this was hell, getting the headed bed back in place took some time. As you can see I choose to print the (V6 version)[https://github.com/nevermore3d/Nevermore_Micro/tree/master/V6] and not the (Formbot version)[https://drive.google.com/file/d/13Aie-BDK4WHfmduJOtDo85zog0QI33kh/view] (if link is broken, they can be found (here)[https://drive.google.com/file/d/13Aie-BDK4WHfmduJOtDo85zog0QI33kh/view]). I didn't have a JST connector over so I've temporarily used other connectors.
![](/images/never_more_temp_connectors.jpeg)

As you can see the non tuned printer has a bit of work ahead before it prints well.
![](/images/untuned_printer_0.jpeg)
![](/images/untuned_printer_1.jpeg)

As there were more 1mm foam-tape included I also added it to the inside of the doors which made a real impact.

#### Summary
All in all it's been a fun build. It now prints parts and seems happy. It took some time getting the config correct with all pins. I also mounted some led strips at the top of the chamber. I was a bit affraid of crashing the whole printer badly but thanks to the well written (initial setup guide)[https://docs.vorondesign.com/build/startup/] everything work out fine. Just remember TAP will figure out where true Z is. Make sure to put you <INCERT NAME OF Z DISTANCE> to what it should be. I used <INECERT NUMBER> and that seems to work fine. Also remember there is a huge community, I asked for help several times when I needed it. Just be mindful it's a community and not a support. I'm really happy I toke this project on and built what seems like a printer that will be my new working horse. Looking forward on tweeking it and improving print quality, one commit at a time.

If you're interested in my config files they are available (here)[].