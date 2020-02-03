## Wifipineaple-Pisen-WPR001N
## Intro

Usually, in order to make the router more abundant, we will choose to flash the third-party custom firmware to the router. 
My goal is to let the router automatically log in to authenticate the campus network. Flashing third-party firmware here is only the first step. 
Not all routes can be flashed with third-party firmware. Now policies are becoming more and more stringent on manufacturers, and it is estimated that there will be fewer and fewer flashes in the future. 
These two routes are basically the same as TL-WR703N routing module hardware of TP-Link, and you can use the OpenWrt firmware of TL-WR703N.

This article is an entry-level brush OpenWRT tutorial, you can ignore it. 
If you play the router, if the official Bootloader flashes the firmware and accidentally brushes it, then the router is bricked. The 
flashing boot is the first step to play routing. Then as long as the firmware is not flashed, the boot partition will not hang.

## For Pinsheng's cloud routers WPR001N and WMM003N, we need to flash the third-party bootloader to replace the official one.

I am using a closed source Bootloader developed by hackpascal 
http://www.right.com.cn/forum/thread-161906-1-1.html

The file name is breed-ar9331-pisen.bin 
for exclusive use of Pinsheng Cloud Routing (Pisen Easy Charge WMM003N / Wireless Music Routing WPR001N), baud rate 115200, reset key GPIO # 12

## Ready to work

Download breed-ar9331-pisen.bin, copy to the root directory of the USB flash drive

Brush Bootloader

telnet login to routing

Utilize the telnet function opened by the router's original firmware to flash in this new U-Boot file. The network cable is directly connected to the computer and the router. Use Telnet to log in to the router. 
Linux terminal can directly enter telnet command; 
Windows telnet is closed by default, open in Windows function, specific self-search. 
The default account of the firmware: root, password: ifconfig 
connection command:

```
$ telnet 192.168.222.254
```

Default location after

```

loginroot@PISENWIFI:~#

```

Backup the original partition file

All the following commands are executed in the default directory after logging in to the route

View system disk partition information, you can see u-bootand artpartition

```

$ cat /proc/mtd

```

Back up the original u-boot and art to the / tmp directory:

```
$ dd if=/dev/mtd0 of=/tmp/uboot.bin
$ dd if=/dev/mtd4 of=/tmp/art.bin

```
Check the disk space occupation of the file system before inserting the USB flash drive

```

$ df

```

Insert U disk and then execute df
can find more of a 

```
/dev/sda4
```
is U disk,
```
mount/tmp/mnt/disk-a4
```

Move the backup uboot.bin and art.bin to a USB stick

```

$ mv /tmp/uboot.bin /tmp/mnt/disk-a4
$ mv /tmp/art.bin /tmp/mnt/disk-a4

```

See if the backup was successful

```

$ ls /tmp/mnt/disk-a4

```

See if there are u-boot.bin and art.bin just backed up in the list

Brush breed to replace the original u-boot

Copy the breed-ar9331-pisen.bin from the USB disk to the router / tmp directory

```

$ cp /tmp/mnt/disk-a4/breed-ar9331-pisen.bin /tmp

```

Flash u-boot file

```

$ mtd -r write /tmp/breed-ar9331-pisen u-boot

```

The router will restart automatically after execution. 
Then you can flash the firmware in the Breed Boot console.

Flash Openwrt firmware

Into the console as follows: 
the route off, the computer is arranged to automatically obtain IP, routing power to quickly hold the reset button, until the LED starts flashing let go, the computer input http://192.168.1.1
can enter control Breed Stage. 
Note in the console settings to see if the MAC address is still the router's MAC. If not, please change it back. (The router MAC is in the fuselage description section)

Download the latest Chaos_Calmer OpenWrt firmware (2015.9) on the OpenWrt official website, and download the TL-WR 703N firmware. The link is as follows: 
http://downloads.openwrt.org/chaos_calmer/15.05/ar71xx/generic/openwrt-15.05-ar71xx-generic-tl-wr703n-v1-squashfs-factory.bin

In the console firmware update , check the firmware , select the downloaded firmware, and then upload and update. It is recommended to use Chrome or FireFox browser.

## The end

These two routes from PISEN have MicroUSB interfaces, which can be powered by a universal mobile charger or mobile power supply. 
When the school is powered off at night, using the WPR001N with a mobile power supply can continue to use wireless after the dormitory is powered off at night!
