# **Installing Ubuntu based Armbian Linux on H96 Max X3 TV Box**
![H96X3Max](/11-H96-max-x3-S905X3-rounded-mini-android-tv-box.jpg)

Ok the main question is how did I end up with a TV Box instead of going with the popular miniature computers like Raspberry Pis. The thing is, Raspberry Pis here in my country are frikin expensive compared to these TV Boxes. A base model Raspberry Pi 3 with 1 GB RAM cost around Rs 8000 while I can get a TV Box with same performance CPU and RAM of 4 GB with just Rs 5800, not to forget about the plus points like built in heat sink, pre built plastic box for the board , built in EMMC memory of 32 GB or more, and so on.

So, getting a TV Box is definitely a smart choice. But the problem is getting Linux run on it. Since these TV Boxes comes with Android OS pre installed and has a different way of booting, getting it to work with Linux is very tedious job. 

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
Download the files from this link : https://mega.nz/folder/A5kmDZAC#6t5FO2NUlIr-070EsGtfPA

* Burn the ISO from the downloaded files you want on to your USB Flash Drive using Balena Etcher
* Once it's complete, you should see a boot drive or any drive. Go there
* Copy the  “h96max-x3-test8.dtb” ( from the files you downloaded ) to  /dtb/amlogic/ of your USB Drive
* Then modify the uEnv.txt to load that dtb and uncomment the 'APPEND' entry on aml s9xxx section

It should look something like this
```javascript
LINUX=/zImage
INITRD=/uInitrd

# rk-3399
#FDT=/dtb/rockchip/rk3399-rock-pi-4.dtb
FDT=/dtb/rockchip/rk3399-nanopc-t4.dtb
APPEND=root=LABEL=ROOT_EMMC rootflags=data=writeback rw console=uart8250,mmio32,0xff1a0000 console=tty0 no_console_suspend consoleblank=0 fsck.fix=yes fsck.repair=yes net.ifnames=0

# rk-3328
#FDT=/dtb/rockchip/rk3328-box-trn9.dtb
#FDT=/dtb/rockchip/rk3328-box.dtb
#APPEND=root=LABEL=ROOT_EMMC rootflags=data=writeback rw console=uart8250,mmio32,0xff130000 console=tty0 no_console_suspend consoleblank=0 fsck.fix=yes fsck.repair=yes net.ifnames=0

# aw h6
#FDT=/dtb/allwinner/sun50i-h6-tanix-tx6.dtb
#APPEND=root=LABEL=ROOT_EMMC rootflags=data=writeback rw console=ttyS0,115200 console=tty0 no_console_suspend consoleblank=0 fsck.fix=yes fsck.repair=yes net.ifnames=0
#APPEND=root=LABEL=ROOT_EMMC rootflags=data=writeback rw console=ttyS0,115200 console=tty0 no_console_suspend consoleblank=0 fsck.fix=yes fsck.repair=yes net.ifnames=0 mem=2048M video=HDMI-A-1:e

# aml s9xxx
FDT=/dtb/amlogic/h96max-x3-test8.dtb
#FDT=/dtb/amlogic/meson-g12b-ugoos-am6-no-cvbs.dtb
#FDT=/dtb/amlogic/meson-g12b-odroid-n2.dtb
APPEND=root=LABEL=ROOT_EMMC rootflags=data=writeback rw console=ttyAML0,115200n8 console=tty0 no_console_suspend consoleblank=0 fsck.fix=yes fsck.repair=yes net.ifnames=0
```

* Now once everything is done save the file and disconnect the USB from the PC
* Get your TV Box ready with TV Screen or Monitor and connect the USB in to you TV Box.
* Make your your TV Box is powered off, now get that toothpick I talked about earlier and put it inside the AV Jack port, inside the AV Jack port there should a small clickable button, press and keep holding it with your toothpick and power on the TV Box until you see the Linux kernel loading screen, then release it.

You are done !! If everything was done properly you should see the Armbian Linux screen. Follow the basic guide there and you should see a homescreen like this 
![armbianhome](/home.png)

## Dual boot with Android or Permanent Linux Box ?
Since you have booted the Linux you can also permanently install it in to the box's built in EMMC, this will remove the existing Android OS and Linux will boot instead. IF you don't want to do that and use your USB drive as a portal bootable Armbian Linux then you should leave as it is, and skip the steps below.

## Installing Armbian Permanently into the TV Box ( You can reinstall Android OS by flashing original Box's firmware if you want but it will remove the Linux )
* Look for the file install-aml.sh on /root and execute it or just directly execute it without looking for it by sudo ``/root/install-aml.sh ``. Follow the procedure and Linux will be installed into your TV Box's Storage. You can remove the USB Flash Drive and restart the TV Box.

## So, what next ?
![neofetch](/neofetch.png)
It is basically running a Ubuntu 20.7, you can host or do whatever you want. For me, I am currently using this TV Box as a headless server and making do :
* **Hosting Pi-Hole and using it as a primary DNS Sever**

![pihole](/pihole.png)
* **Hosting OpenVPN Server**

![openvpn](/openvpn.png)
* **Connected a 1 TB External HDD to the TV Box on USB 3.0 and enabled SAMBA , currently using it for NAS alternative.**

![nas](/nas.png)![copy](/copy.png)
* **Qbittorent Server**

![torrent](/torrent.png)
* Using as a Printer Server
* Docker
* Dicord Bots Hosting
* Heck you can even host a paper minecraft server on it. And it performs well. Don't belive me ? Check here https://youtu.be/2WHLUiJtN4E



