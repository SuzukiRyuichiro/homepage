---
title: "Building Lily58"
date: 2023-06-23T18:51:21+02:00
draft: true
toc: true
images:
tags:
  - Keyboard
  - DIY
---

## My first DIY keyboard build

## Things I wish I had known beforehand

### Difference of pins you can have for your controller

In the Lily58 set I got from Mechboad.co.uk, it came with two Pro Micro controllers. These controllers are sold with header pins, which is packaged together with the board. Those pin headers works, but many websites and tutorials advice not to use them. The reason for that is when you want to swap the controller, default pin headers won't allow that. Occasions you want to swap the controllers are

1. You broke the controller, especially the USB socket which is relatively fragile.
2. You want to upgrade your controller to make it wireless, etc
3. Your controller broke in some other shape or form

Given that, I realized that many build tutorials and website recommended using some other removable pin headers instead. Some retailers sell those pins on top of the default pins that comes with the controllers. 

This realization made me very nervous soldering the controllers, because I knew I would be wasting all that money if I make some mistake. In the end, I made up my mind and soldered everything, and turned out to be completely fine. However, now I don't have any upgradability.

### Difference in USB cable can make you feel you fucked up

To install firmware to the controllers, I plugged the board with my USB-c to USB-c cable that came with my MacBook and tried to flash. However, it never recognized the board no matter what. There was no flashing lights (I didn't know at this point that the controller had LED on it) nor nothing. I initially thought that the controller itself was faulty. 

Just to try things out, I changed the cable to USB-A to USB-c cable that came with my nothing ear(1) ear buds. Then the LED came on. That made me hopeful that now I can finally install the firmware. However, when I ran the QMK command and tried to reset the board, although the reset signal was visible, it didn't register on the computer side.

With tiny hope, I changed my cable to another generic USB-A to USB-c cable I use on my bedside. It did flash the LED, and when running the QMK command, it finally registered my reset button and installed the firmware. I did not expect that the board will be this picky about which cable to use. I knew type-c is a mess in terms of standards but if you're building one and facing a similar problem, try out every single cable you got. 



## Soldering is not that hard

## You don't have to be overly cautious, yet be careful

## Fuck Brexit
