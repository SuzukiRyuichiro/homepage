---
title: "Building Lily58"
date: 2023-06-23T18:51:21+02:00
draft: false
toc: true
images:
tags:
  - Keyboard
  - DIY
---

## My first DIY keyboard build

I've been looking into ergonomic mechanical keyboards for a while, and I finally made one. I chose Lily58 since it seemed to be not too far from the normal keyboard layout while having a lot of thumb keys, which is what I wanted. I heavily use keyboard shortcuts while working, and this layout looked promising.

I got the keyboard set that is not pre-assembled, as I wanted to keep it under budget and also enjoy the challenge of soldering all the switches and diodes. Trust me, it was a lot of fun.

### Lay the parts out

Before jumping into the actual build, it was helpful to organize all your parts, especially the small parts. I used a masking tape to layout the small diodes and switch sockets (in the same direction!!!) so I can be efficient when soldering.

### Solder the diodes

Once your workspace is organized, start by pre-solder the PCB where diodes will go. It was difficult to get the right amount on to the board, but I figured putting the iron onto the metallic part of the PCB and heat that part up until the solder melts and spread onto the PCB.

Once that's done for all 58 keys, you can start soldering the diodes onto the PCB. Diodes are polar components, which means they have a direction. Make sure to match the orientation shown on the PCB. This is why you should have all the diodes layed out beforehand.

### Initialize the controllers

First, you can solder the reset switches onto the micro controllers.

### Solder the controllers

After the diodes are in place, it's time to move on to the micro controllers. These can be a bit tricky due to the number of pins involved. Line up the micro controller so that all pins align with the holes on the PCB and start soldering them one by one.

This was a scary part for me since I did not have the pins every Youtube videos or internet tutorials had. I only had a single use pins, which cannot be pulled out after soldering. It got me scared that if I mess this up, the whole board will be a waste, but I made up my mind and soldered it. It worked just fine in the end. All I needed was a courage I guess lol

### Solder the switch sockets

Switch sockets allow you to hot-swap your switches without needing to solder again.

### Check the solder with metallic tweezers

Once all the soldering is done, use a pair of metallic tweezers to check for any mistakes. You can do this by lightly touching each solder joint and ensuring it's well-formed. If you find any solder bridges or cold solder joints, you can fix them using a solder sucker or additional solder as required.

### Put the key switches

Now for the final step: putting in the key switches. Take your switches and carefully press them into the switch sockets you soldered earlier. Make sure they're firmly seated and level. Once all switches are in place, you can proceed to add your key caps.

And there you have it, your very own Lily58 mechanical keyboard! With this new setup, not only do you have a more ergonomic layout, but you also get the satisfaction of having built it yourself.

## Things I wish I had known beforehand

### Difference of pins you can have for your controller

In the Lily58 set I got from Mechboad.co.uk, it came with two Pro Micro controllers. These controllers are sold with header pins, which is packaged together with the board. Those pin headers works, but many websites and tutorials advice not to use them. The reason for that is when you want to swap the controller, default pin headers won't allow that. Occasions you want to swap the controllers are

1. You broke the controller, especially the USB socket which is relatively fragile.
2. You want to upgrade your controller to make it wireless, etc
3. Your controller broke in some other shape or form

Given that, I realized that many build tutorials and website recommended using some other removable pin headers instead. Some retailers sell those pins on top of the default pins that comes with the controllers.

This realization made me very nervous soldering the controllers, because I knew I would be wasting all that money if I make some mistake. In the end, I made up my mind and soldered everything, and turned out to be completely fine. However, now I don't have any upgradeability.

### Difference in USB cable can make you feel you fucked up

To install firmware to the controllers, I plugged the board with my USB-c to USB-c cable that came with my MacBook and tried to flash. However, it never recognized the board no matter what. There was no flashing lights (I didn't know at this point that the controller had LED on it) nor nothing. I initially thought that the controller itself was faulty.

Just to try things out, I changed the cable to USB-A to USB-c cable that came with my nothing ear(1) ear buds. Then the LED came on. That made me hopeful that now I can finally install the firmware. However, when I ran the QMK command and tried to reset the board, although the reset signal was visible, it didn't register on the computer side.

With tiny hope, I changed my cable to another generic USB-A to USB-c cable I use on my bedside. It did flash the LED, and when running the QMK command, it finally registered my reset button and installed the firmware. I did not expect that the board will be this picky about which cable to use. I knew type-c is a mess in terms of standards but if you're building one and facing a similar problem, try out every single cable you got.

## Soldering is not that hard

This is my second time soldering something (first being a headphone I fixed years ago) and given that there are so many parts to solder, I was fearful that I'd mess up something and waste all the money I put in. However, in the end, it wasn't that hard. If you follow the protocol, such as setting the right temperature not to melt your PCB or controller, it was easier than I thought. Also, since you'd be soldering more than 200 points, at the end of it, you'd be much better at soldering than the first few. As for this build, the difference is quite obvious, both in quality and speed of soldering. So have faith in yourself and give it a try.

## You don't have to be overly cautious, yet be careful

In relation to the point above, I thought a millimeter of mistake would cause some problem to the keyboard but it turned out just fine. I was a bit cocky at the end when soldering sockets and stuff but it just worked. I thing one thing I should have been cautious was putting the switches into the sockets. If the pin is unalinged for the tiniest margin, you can bend the connectors and it won't register. I missed sockets in 4 switches, and had to pull them out, straighten the bent pin, then put it back again until it registers a key press. To sum up, be careful enough not to break things, but you can be careless in some parts, and it still works.

## Fuck Brexit

I got my keyboard from an UK mechanical keyboard vendor. I didn't read the fine print so it's my fault but I got charged around €40 for a €140 purchase, and it took around a week to go though custom clearance. That was quite annoying.
