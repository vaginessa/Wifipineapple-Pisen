## Part 1
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

## Part 2
0x00 official configuration analysis

Since I ca n’t afford the original equipment, I do n’t have a picture of the corresponding PCB, but we can purchase the corresponding hardware according to the official CPU and memory configuration.



Figure 0-1 WIFI pineapple configuration on the Wifipineapple wiki

The official website is very clear, even the CPU model and memory model are written in great detail. The CPU is Qualcomm's AR9331, and the memory is 64m of DDR2.

 

Figure 0-2 AR9331 data sheet description of the DDR memory controller

Because the firmware is 8m or more, it is said that norflash is also 8M or more. At present, the maximum size of the norflash in the sop8 package is 32m (MX25L25645).

 

Figure 0-3 SPI FLASH description in AR9331 data sheet.

But after checking the data sheet of the AR9331, it only supports a maximum of 16M SPI flash. So, we can only use 16m SPI flash (not memory)

0x01 Material preparation:

1. Integrated host:

It is recommended to use Pin Sheng Yunzuo Easy Charge (about 70 fish) or Lenovo PWR-G60 (about 100 fish). Why recommend these two? Because the CPU and memory of these two machines are the same as the official configuration. At the same time, a built-in amp circuit and a battery group are built in. Lenovo's built-in 6000mah battery, PISEN's built-in 5000mah two 18650 batteries. Lenovo is relatively easy to disassemble. Pinsheng is not easy to disassemble, but two 18650 battery compartments are reserved. For qualified friends, you can directly connect two 3500mah Sanyo batteries or something. The sample win machine has up to 7000mah Battery.

2.NOR flash:

The general ar9331 router ROM is 8MB. The official configuration of wifipineapple is 16MB, so if we want to use this machine, we must change to a 16MB nor flash (ROM), because the interface is SPI interface, I recommend using 25q128fvsig of WINBORD

3. programmer

If you have a programmer on hand, this step is omitted. If you don't have a programmer and want to buy one. I recommend the use of the CH341A programmer, for a dozen dollars on a certain treasure. Used to flash the norflash chip

3. If you think the above is troublesome? What if I do n’t have a soldering iron at home and I wo n’t disassemble the chip?

Don't worry, we can buy a router with the same official configuration. GL.-iNET's ar150 router is recommended. This is a completely lazy version. After you basically buy it, you can use the program after brushing it. What about the disadvantages? Just because there is no built-in battery, you cannot write and carry it. But for us as geeks, it doesn't matter, just change a module by ourselves. Wouldn't it be nice to integrate a USB serial port, USBHUB and UPS module?

0x02 hardware transformation

In fact, the hardware reconstruction is relatively simple. We just need to remove the old flash chip and write the new flash's BootLoader. It ’s ok to put it on. The Lenovo pwr-g60 I recommend above also operates the same as the following tutorial

1.First we have to take apart the shell

As for how to dismantle? Please move your mind

 

Figure 2.1 Pinsion Cloud Easy Charge

2. Separate the cell from the PCB

The reason is that the FLASH chip is on the back of the board. If we directly heat the flash on the back, it may cause the front panel cells to heat up. Cause danger

 

Figure 2.2.1 The process of separating the cell from the PCB

I directly inserted a knife into the middle of the battery pack and the pcb, and opened it as soon as I inserted it.

 

Figure 2.2.2 after opening

3.Disconnect the connection between the battery core and the motherboard

For safety reasons, it is recommended to remove the battery connection cable first. Finally, connect the battery.

4.Remove the built-in flash

First we find the location of the spiflash. The picture below is the flash location of Pinsheng Cloud

 

Figure 2.4.1 Location of SPI Flash

The picture below is the flash position of Lenovo PWR-G60. Is everyone familiar with it? WIIFPINEAPPLE selling 700 yuan in one eye

 

 
Figure 2.4.2 2.4.3 Location of Lenovo PWR-G60 SPI Flash

The flashes carried by these two routes are 25m64 standard 8m spi flash. Remove the solder paste air gun at 350 degrees from level 3-4 directly. Remove it and clean the pads a little

 

Figure 2.4.4 Remove SPI Flash

5. Firmware programming

We open a new flash 25q128. Don't rush to install it, let's put it on the programmer and flash BootLoader. BootLoader I recommend using the BrePad BootLoader of HackPascal's predecessor, the graphical BootLoader. Easy to use
First pay tribute to the hackpascal seniors who have adapted the Breed BootLoader to various routes for a long time without charge! 
Indicates that my programmer is SkyPRO II offline programmer from SkyPRO. However, the programmers are used in much the same way. Here, how do other programmers use them? I won't do narration!

2.5.1 Backup ART

First, let ’s put the old chip in the programmer ’s chip holder. At this time, we do n’t need to worry about flashing the BootLoader. We first back up the data in the system's flash.

 

Figure 2.5.1.1 programmer interface

Then open a hex editor 010editor or winhex casually. 
Go to the position 0x7F0000 and select 65535 bytes (64KB). The conversion to hexadecimal is to choose the size of 10000, that is, to 0x800000. Create a new file named ART, paste this content and save it for future use. This file should be exactly 64kb, no more and no less! This data is the factory tuning data of the built-in wireless network card. Generally, the router manufacturer generally makes the optimal adjustment of the wireless transmission power of the factory product router. Advanced routers are likely to have one data per machine. Therefore, downloading this thing online will never be better. The art extracted on the same brand router is never as good as that extracted on other brand routers. Attachment of this article, I will attach my extracted art

2.5.2 Flashing BootLoader

We directly put the new 16m spi flash on the programmer and directly opened the breed-ar9331-pisen-r1163.bin file. Select the correct chip and flash it directly.

 

Figure 2.5.2.1 SPI Flash card to the programmer's programming socket

 

Figure 2.5.2.2 Successful programming

Please everyone must remember to check after writing, because it is very likely that the rom you bought can be written but can read bad blocks. Maybe the installation can not start or after starting wifi does not appear the system can not boot up a certain command can not wait for all kinds of strange problems. So in order to avoid unnecessary trouble after installation. I recommend that you always verify when programming the ROM. This can prevent malfunctions

6, flash installation

Install the new flash on the motherboard. Be careful not to install the flash upside down. There is a small circle in the upper left corner of the chip, and there is a mark on the pcb. After installing the flash, remember to solder the connection wire of the battery cell

 

Figure 2.6.1 Flash the flash to the corresponding pad

The welding level of the author is limited.

7, ART flashing and firmware flashing test

 

Figure 2.7.1 Screenshot of Breed interface

Turn on the switch and find a network cable to connect directly to the computer from this router. The computer starts to automatically obtain the IP address and access 192.168.1.1 to enter the Breed BootLoader

 

Figure 2.7.2 Modify MAC Address

When this interface appears, it means that all previous operations are correct. If the interface does not appear, the previous steps may not be correct. Please check the previous steps again. 
First click LSDK / QSDK settings and enter the MAC address posted on the PCB. The first line fills in the MAC address behind the PCB sticker, the second line fills in this MAC address +1 and the third line fills in this MAC address +2

 

Figure 2.7.3 Modify mac address

Fill in the mac address pasted on the PCB in the tp-link settings, and then click Save. Select firmware update

 

Figure 2.7.4 Select flash image

Firmware selection The official firmware art of wifipineapple selects the 64kart file just backed up. After confirming that there is no problem, you can directly flash

 


  
 
Figure 2.7.5-6 Screenshot of the flashing process

Prompt to restart after successful flashing

0x03 test articles

After a long hardware transformation, we can finally test whether our transformation is smooth or not. Can this pineapple pie be used normally? Then let ’s test it.

3.1 Connect Pineapple Pie

 

Figure 3.1.1 Screenshot of wifi scanned by notebook

After restarting, turn on your mobile phone or computer and connect to wifi. You will find a wifi starting with Pineapple. The wifi ending with the last four digits of your mac address

3.2 Login Management Address and Initialize Pineapple Pie

 

Figure 3.2.1 Pineapple Pie Welcome Screen

Connect to this wifi browser and open 172.16.42.1:1471 This interface appears to indicate that the installation was successful!

 

Figure 3.2.2 Pineapple Pie safe boot interface

When you get here, please use a clip or a sharp object to press the reset on the machine.

 

Figure 3.2.3 Pineapple Pie Setting Interface

Set user name password time zone management SSID password and wireless area code

 

Figure 3.2.4 Confirm the settings

Complete setup

 

Figure 3.2.5 Rescan WIFI and connect

Reconnect the management wifi you just set up

 

Figure 3.2.6 Login to Wifipineapple

Enter password and login

 

Figure 3.2.7 Wifipineapple dashboard interface

The presence of this interface indicates that the flashing was successful.
