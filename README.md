# RG350 firmware "Rogue" edition<br>
### An independent fork of the OpenDingux project, focused on improving the user experience. 

Thanks to Tonyjin (https://github.com/tonyjih), Pcercuei (https://github.com/pcercuei), Mthuurne (https://github.com/mthuurne) and opendingux (https://github.com/OpenDingux).

## Goals:
- [X] exFAT support, auto-resize, constant sdcard mount point, show version - 1.7.5 branch
- [ ] Replace Gmenu2x with GmenuNX, Suspend capability - 1.8.x branch
- [ ] Kernel update -2.x branch
- [ ] Modernize 3D APIs - 2.1.x
- [ ] HDMI support - 2.2.x
- [ ] Vulkan?? - Future

# update firmware 1.7.8.1: <br>
https://github.com/Ninoh-FOX/OpenRGH/releases/tag/1.7.8.1

# update firmware 1.7.8: <br>
https://github.com/Ninoh-FOX/OpenRGH/releases/tag/1.7.8

# update firmware 1.7.7: <br>
https://drive.google.com/file/d/13iNEBQlbFkueCSAsnWpv8cVGKJv8ihpX/view

# update firmware 1.7.6: <br>
https://drive.google.com/file/d/1kMVWTWTym6TfN3_nrM9N2QSFf2dUxxjp/view

## Changelog:<br>

### 1.7.8.1:<br>
1. boot partition now is mount too in /media/system in rw mode for recovery the system from pc if this is possible.
### intructions for recovery or external update:<br>

thanks to https://github.com/gcwnow wiki

You can copy the kernel or rootfs to the internal SD card of the RG350 using FTP, SFTP or SCP. I recommend SCP since it is just one line on the command prompt. It does require setting up SSH keypair authentication though.

**for kernel**

scp vmlinuz.bin root@10.1.1.2:/media/system/
scp modules.squashfs root@10.1.1.2:/media/system/update_m.bin

**for rootfs**

scp rootfs.squashfs root@10.1.1.2:/media/system/update_r.bin

Reboot the RG350 to activate the new kernel or rootfs. Don't use the reset button: part of the kernel or of the rootfs may not have been flushed from the write cache yet.

You can use:

ssh root@10.1.1.2
RG350:media/data/local/home# reboot

2. Gmenu2x now can link .opk and .dge files.
3. New boot logo.
4. New flasher sdcatd imagen (thanks to https://github.com/gcwnow/imager )


### 1.7.8:<br>
1. lazy_itable_init = 0 and lazy_journal_init = 0 support added to EXT4 file system.
2. Display version in System Info app.

![](https://fotos.subefotos.com/d74d4f1ba67f0d5f556aa7a43e7c7c84o.jpg)

### 1.7.7:<br>
1. exfAT support added - no more need to download a utility to format 64GB+ SD cards
2. Default SD card mount changed to /media/sdcard - No having to re-do paths when swapping SD cards
3. Auto swap file and partition resize - This takes a while, allow it to finish.  Progress will be shown on screen during first boot
4. Duplicate modules removed from modules.squashfs 
5. Fix the resize in old stock firmwares (bad ext4 partition)
6. Fixed power off and reboot error messages
7. Fixed slowdowns and stuttering during first 15 minutes after first boot
8. Rebuild mininit-syspart from original opendingux code.
9. Autoremove old configs of the system in the first boot.
10. Change file system table.
11. Restore USB-HID suport.
12. update libshake from original code: https://github.com/zear/libShake

## Instructions:<br>
1. Place in /media/data/apps or /media/<your SD card>/apps
2. Run from gmenu2x (not currently working in gmenunx)
3. allow process to complete
4. Reboot
5. If system fails to boot, press Y to boot to last working kernel, or X to boot to last working rootfs. X+Y will load your previous OS version.
  
## Instructions for a clear update/ fix internal sdcard or change of internal sdcard:<br>
1. Download a base system "sd_image.bin" from releases.

### **for Windows:<br>**
2. Format the new sdcard / internel sdcard with SD FORMATTER 5.0.1 ( https://www.sdcard.org/downloads/formatter/ ) two times.
3. Download Win32 disk imager ( https://sourceforge.net/projects/win32diskimager/ ) and flash (writer) the FW base imagen in the sdcard.
#### 4. NOT RESIZER THE EXT4 PARTITION IN WINDOWS!!<br> only put the internal sd in the console and follow the instructions.

### **for Linux:<br>**
2. Format the new sdcard / internel sdcard with gnome-disk-utility.
3. Flash the FW base imagen in the sdcard with gnome-disk-utility.
   Or type in a terminal:
   
   sudo dd if=sd_image.bin of=/dev/[sdcard mount poin]
#### 4. Not resize!! Put the internal sd in the console and follow the instructions.
