---
layout: post
title: "Linux Test Session: Manually Mounting a SDHC Card"
date: 2025-04-06 12:00:00
description: "Manually mounting a SDHC Card in Linux"
---


![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/uoxzx0gm8o0d580yip8n.jpg)

The system failed to detect ( and mount) the card when inserted. Ultimately, had to manually mount it.

##### #1. Check if the device is read by the system:

- Before inserting

`*$ ls /dev/* | wc -l`

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/mrkd736spkltpaf0ixim.png)

- After inserting

`*$ ls /dev/* | wc -l`

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/pc31avlvhn3eepf0f6bt.png)

*538 to 542 tells some files or directories were added

- Also 

`*$ dmesg | tail -n 7*`

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/wqyz3ct7u59wvrrk93d2.png)

Notice : `mmcblk0`, that's the device name

##### #2. Check if the device is listed (Other ways to see if device is recognized in some way)

`*$lsblk*`

Lists block devices

`*$lsusb*`

Lists usb devices

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/3glisipspwxplsmv17rm.png)

Notice the name : `*mmcblk0*` and `*mmcblk0p1*`

Also the size : *3.7G*

##### #3. Mount

`*$mount -t type device dir`

Mounts a device name *device* of fs type *type* to directory *dr*

Here:

`*$ sudo mount -t vfat /dev/mmcblk0p1 Desktop/card/`

- Attempt 1 

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/qs897vv15yohjf09isbb.png)


- Attempt 2

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/40j0m7o9oc8xlzbxj3ot.png)


*[-t] option indicates fstype ie. the filesystem type with which the device is formatted; which in here is vfat
The most common are ext2, ext3, ext4, xfs, btrfs, vfat, sysfs, proc, nfs and cifs *


#DONE!

