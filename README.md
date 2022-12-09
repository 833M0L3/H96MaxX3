# **Installing Ubuntu based Armbian Linux on H96 Max X3 TV Box**
![H96X3Max](/11-H96-max-x3-S905X3-rounded-mini-android-tv-box.jpg)

Ok the main question is how did I end up with a TV Box instead of going with the popular miniature computers like Raspberry Pis. The thing is, Raspberry Pis here in my country are frikin expensive compared to these TV Boxes. A base model Raspberry Pi 3 with 1 GB RAM cost around Rs 8000 while I can get a TV Box with same performance CPU and RAM of 4 GB with just Rs 5800, not to forget about all the plus points like built in heat sink, pre built plastic box for the board , built in EMMC memory of 32 GB or more, and so on. [Read here for more info](https://ozkolonur.medium.com/here-is-why-i-am-replacing-my-raspberry-pi-4-nodes-with-this-ce7170c71a60)

So, getting a TV Box is definitely a smart choice. But the problem is getting Linux to run on it. Since these TV Boxes come with Android OS pre installed and have a different way of booting, getting it to work with Linux is a very tedious job. 

## Device specifications

Basic   | Spec Sheet
-------:|:-------------------------
SoC     | Amlogic S905X3 64 bit 
GPU     | G31™ MP2 GPU Processor
Memory  | 4 GB RAM
Storage | 32/64/128 GB EMMC
WiFi    | IEEE 802.11 A/B/G/N ; 2.4G / 5G
Ethernet| Support 100M/1000M Gigabit
USB     | 1 x USB 3.0 ; 1 x USB 2.0
Bluetooth| BT 4.0 (Support Voice Remote)
HDMI    | HDMI 2.1 ,Support HDMI CEC, Dynamic HDR And And 8Kx4K@24 Max Resolution Output

## Things you will be needing
* H96 Max X3 ( Ofcourse )
* A toothpick ( Yes , I am being serious )
* USB Flash Drive/Pendrive
* PC with any OS
* Balena Etcher

## Next Steps
Download the image file based on your SoC i.e : S905x3 from this link : https://github.com/ophub/amlogic-s9xxx-armbian/releases

* Burn it on to your USB Flash Drive using Balena Etcher
* Mount newly created BOOT volume, and:
  ```
  cp u-boot-x96maxplus.bin u-boot.ext
  vi uEnv.txt # change FDT=/dtb/amlogic/meson-sm1-h96-max-x3.dtb
  ```
* Get your TV Box ready with TV Screen or Monitor and connect the USB in to you TV Box.
* Make sure your TV Box is powered off, now get that toothpick I talked about earlier and put it inside the AV Jack port. Inside the AV Jack port there should a small clickable button, press and keep holding it while you power on the TV Box until you see the Linux kernel loading screen, then release it.

You are done !! If everything was done properly you should see the Armbian Linux screen. Follow the basic guide there and you should see a homescreen like this 
![armbianhome](/home.png)

## Dual boot with Android or Permanent Linux Box ?
Since you have booted the Linux you can also permanently install it in to the box's built in eMMC Memory, this will remove the existing Android OS and Linux will boot instead. If you don't want to do that and use your USB drive as a portable bootable Armbian Linux then you should leave as it is, and skip the steps below.

## Installing Armbian Permanently into the TV Box ( You can reinstall Android OS by flashing original Box's firmware if you want but it will remove the Linux )
*  Just directly execute this command ``armbian-install``. Follow the procedure and Linux will be installed into your TV Box's eMMC Memory. You can remove the USB Flash Drive and restart the TV Box. For more information you can check out his awesome github repo https://github.com/ophub/amlogic-s9xxx-armbian

## How to revert back to the original Android TV Box Firmware or incase if you bricked your box how to unbrick it?
There are possibilities that things might go wrong and you might end up bricking your device. Or maybe you just wan to get your device back to the what it used to be. Well , the unbricking process is very easy. You need a PC running Windows OS and **a USB Male to Male Type A cable**.  Go to this site https://www.h96tvbox.com/content/6-Firmware-upgrade and select download which you can find near the H96 Max X3 option.

Download all the files listed there. Watch the video which shows you how to install the USB Burning Tool properly. **This is very important !** . After you are done installing it and doing other stuffs like copying the license folder to the main installation folder. Get your TV Box, open USB Burning Tool and import the image file that you downloaded. And wait few sec and click on start. Then get the toothpick and and the USB Male to Male Type A  cable. Press and hold the AV hole button with the toothpick, and connect the the USB Male to Male Type A  to the black port of the TV BOX and with PC. Then it should start downloading the firmware on the USB Burning Tool. Please remember this, you don't need your TV Box to be connected to a power source. Only connecting your PC with TV Box using USB Male to Male Type A cable is enough.

## So, what next ?
![neofetch](/neofetch.png)
It is basically Linux server running Ubuntu, you can host or do whatever you want. For me, I am currently using this TV Box as a headless server and using to do cool stuffs like :
* **Hosting Pi-Hole and using it as a primary DNS Sever**

![pihole](/pihole.png)
* **Hosting OpenVPN Server**

![openvpn](/openvpn.png)
* **Connected a 1 TB External HDD to the TV Box on USB 3.0 and enabled SAMBA , currently using it for NAS alternative.**

![nas](/nas.png)![copy](/copy.png)
* **Qbittorent Server**

![torrent](/torrent.png)
* **Using as a Printer Server**

![printer](/printer%20server.png)
![printerserv](/printerserv2.png)
* Docker
* Dicord Bots Hosting
* Heck you can even host a paper minecraft server on it. And it performs well. Don't belive me ? Check here https://youtu.be/2WHLUiJtN4E

## Credits
* https://forum.armbian.com/topic/13992-h96-max-x3-specifics-only/
* https://forum.freaktab.com/forum/tv-player-support/amlogic-based-tv-players/s905x3/firmware-roms-tools-ds/812507-rom-mod-hk1-x3-h96-max-x3-vontar-x3-transpeed-x3-air-bqeel-y8-max-amlogic-s905x3/page14
* https://github.com/ophub/amlogic-s9xxx-armbian
