---
layout: default
title: Home
---
# Installation guide: Windows 10, Ubuntu 15.10, or both
For Macs with OS X El Capitan

## Purpose of this guide	
This guide describes how to install the latest versions to date of Windows and Ubuntu (Windows 10 and Ubuntu 15.10) on a Mac that runs OS X El Capitan (10.11).

In this guide, you learn how to:
- use Boot Camp Assistant to install Windows 10
- install rEFInd boot manager to start more than one Operating System (OS)
- install Ubuntu 15.10
- switch between the OSes
It does not describe how to install OS X El Capitan, install earlier or future versions of Windows or Ubuntu, or upgrade existing installations of Windows or Ubuntu. I"n this guide, the chapters that describe Windows installation and Ubuntu installation are independent. Depending on your needs, you can either follow this guide step by step or skip the sections that do not apply to your installation type.

## Audience for this guide

Caution: This guide contains procedures that require you to use advanced functionalities, disable vital components of your Mac, and alter the hard disk structure. Before you proceed, make sure that you understand the concept of partitioning and that you have basic knowledge of all three OSes.

Consider multi booting if you identify with at least one the following situations:
- you switch between the OSes regularly and want to have access to them on the same computer
- you use OS-specific software
- you are a software developer and want to test your programs on multiple OSes
- you use virtual machines on your Mac to run Windows or Linux and want better 3D acceleration
- you want to experiment with multiple OSes

# What is multi booting?

When you have a multi-boot configuration, you have more than one OS on the same computer and can start — or *boot* — them asynchronously. Whenever you start your computer, you select which OS to run from a menu. Each time that you want to switch between OSes, you restart your computer. Depending on whether you want to have two or three concurrent OSes on your Mac, you can opt for either dual booting or triple booting.

## About virtual machines
Virtual machines also allow you to run multiple OSes on the same computer, but they need to run within a host OS. That host OS uses a significant part of available resources and the OSes that you virtualize share the remaining resources. Multi booting, however, allows you to dedicate all the resources of your computer to the OS that you choose to run.

## About dual booting
Apple allows Macs to double boot natively through Boot Camp. Boot Camp helps you partition your hard disk and install Windows. Boot Camp automatically installs a boot manager to allow you to choose which OS to run.

## About triple booting
Triple boot, unlike double boot, is not a standard mode of installation. It requires that you install unofficial tools and use advanced functionalities. To perform a triple-boot installation, you use Boot Camp to perform a dual-boot installation first. To be able to choose which OS to run, you install a boot manager. The boot manager automatically presents a menu of options at startup and loads the environment, drivers, and system.

## About partitions
If OS X is the only OS on your Mac, it normally uses a single partition that covers the entire hard disk. To install Windows, Ubuntu, or both alongside OS X on your Mac, you create an independent partition for each OS.

Caution: If you want to install both Windows and Ubuntu, follow the entire procedure in this guide so that you install Windows before you install Ubuntu. If you try to install Windows after you install Ubuntu, the Windows installer may overwrite the entire hard disk.

# Advanced users
If you are an advanced user, you can do the following to customize your multi boot:
- choose alternate versions or distributions of Windows and Linux
- install Windows without Boot Camp **(not recommended)**
- install another boot manager

Note: To date, the most popular boot managers that support multi booting are rEFIt and rEFInd. This guide describes how to download and install rEFInd, as rEFIt is no longer maintained. As an advanced user, you can instead download and learn how to install rEFIt from the [rEFIt Project website](http://refit.sourceforge.net/).
In any case, the overall procedure remains similar and you can still use this guide as a reference.

# Before you start
To improve your installation experience, make sure that you meet all requirements and download all necessary files.

## Prerequisites
The overall procedure takes 3 to 4 hours to complete.
To perform the installations, you must have administrator privileges on OS X. Before you install, make sure that your system meets all hardware and software requirements.

### Hardware requirements
- Enough free space on your hard disk
- A Mac that supports Windows 10
- An 8 GB (or larger) blank USB flash drive

### Software requirements
- An up-to-date installation of OS X El Capitan

Caution: To prevent data loss, make sure to back up your files to an external disk, a CD, a DVD, or USB drive.

## Preparing to install

Your Mac can run 64-bit OSes only. In this section, you download the latest 64-bit disk images (ISO files) from Microsoft and Ubuntu official websites, and check the integrity of your download of Ubuntu. You also download rEFInd boot manager.

If you want to dual boot with Ubuntu, skip to 2.2.2 Downloading Ubuntu 15.10 Desktop disk image.

### Downloading Windows 10 disk image
1. Go to Windows 10 disk image download page (http://www.microsoft.com/en-us/software-download/windows10ISO).
2. Under Select edition, select Windows 10 from the dropdown menu.
3. Click Confirm. The page reloads.
4. Under Select the product language, select your language from the dropdown menu.
5. Click Confirm. A new page opens.
6. Click the 64-bit Download button. The download starts.
7. For more convenience, move Windows 10 disk image to your desktop.

If you want to dual boot with Windows, skip to 3. Installing Windows with Boot Camp Assistant.

### Downloading Ubuntu 15.10 Desktop disk image
1. Go to Ubuntu Desktop disk image download page (http://www.ubuntu.com/download/desktop).
2. In the Ubuntu 15.10 section, make sure that 64-bit — recommended is the active option for the Choose your flavour dropdown menu.
3. Click the Download button. A new page opens.
4. Scroll to the bottom of the page.
5. Click Not now, take me to the download ›. A new page opens and the download starts. If the download does not start, click download now.
6. For more convenience, move Ubuntu 15.10 disk image to your desktop.
7. Check the MD5 Hash of your Ubuntu 15.10 disk image:
    a. From the Utilities folder in the Applications folder, open Terminal.
    b. Enter the following command, where username is your account name, and ubuntu_ISO_file.iso is the Ubuntu 15.10 disk image name: `md5 /Users/username/Desktop/ubuntu_ISO_file.iso`
    Example: `md5 /Users/John/Desktop/ubuntu-15.10-desktop-amd64.iso`
    The command returns the MD5 checksum hash of your download (for example, `ece816e12f97018fa3d4974b5fd27337`).
8. Go to http://releases.ubuntu.com/15.10/MD5SUMS and compare the source MD5 hash for ubuntu-15.10-desktop-amd64.iso against the MD5 hash of your download. If they are different, your download is corrupt and you need to repeat step 1 through step 7.

### Downloading rEFInd boot manager
1. Go to rEFInd download page (http://sourceforge.net/projects/refind/).
2. Click the Download button. A new page opens and the download starts. If the download does not start, click direct link or mirror.
3. For more convenience, uncompress the rEFInd ZIP file onto your desktop.

You have all the installation files that you need to perform your multi-boot installation. Proceed to the installation of the OSes.

## Installing Windows with Boot Camp Assistant
Before you install Windows on your Mac, you create a bootable Windows installer drive and a Windows partition with Boot Camp Assistant. Boot Camp Assistant guides you through the installation of Windows on your Mac and downloads Mac drivers for hardware and software support for Windows 10.

If you already have Windows on your Mac or want to dual boot with Ubuntu, skip this chapter and go to 4. Installing rEFInd boot manager.

### Creating a bootable Windows installer drive
In this section, you use Boot Camp Assistant to copy Windows installation files and Mac drivers onto your USB flash drive. Boot Camp Assistant automatically makes your USB flash drive bootable, so your Mac can read from it at startup instead of its hard disk.

1. Plug your Mac into a power outlet.
2. Start OS X.
3. Connect your USB flash drive.
4. From the Utilities folder in the Applications folder, open Boot Camp Assistant.
5. In the Boot Camp Assistant window, select all three tasks:
    - Create a Windows 8 or later install disk
    - Download the latest Windows support software from Apple
    - Install Windows 8 or later version
6. Click **Continue**. Boot Camp Assistant asks you to locate the Windows 10 disk image (ISO file) and select a USB destination drive.
7. If the ISO image field is empty, click **Choose…** to locate the ISO file manually.
8. If Boot Camp Assistant detects many USB flash drives, select which drive to use as the destination disk.
9. Click Continue.
10. When the warning message appears, click **Continue**. Boot Camp Assistant copies Windows installation files and Mac drivers to your destination drive and makes it bootable.

Boot Camp Assistant asks you to create a Windows partition. Do not remove the bootable Windows installer drive.

### Creating a Windows partition
In this section, you continue to use Boot Camp Assistant to repartition your hard disk and allocate disk space to Windows.

1. To specify a partition size, drag the divider between the OS X and Windows partitions.
Note: Windows 10 requires at least 20 GB of free hard disk space. Make sure that you set the right partition size for Windows because you cannot resize it later on.
2. Click Install. Boot Camp Assistant partitions your hard disk.

When Boot Camp Assistant completes the operation, your Mac restarts to the Windows installer from your USB drive. If the Windows installer does not start, refer to the Troubleshooting section.

## Running the Windows installer
In this section, you use the Windows installer from the bootable Windows installer drive to install Windows in custom mode.

1. Follow the on-screen instructions. The Windows installer asks which type of installation you want to perform.
2. Select Custom: Install Windows only (advanced). The Windows installer asks where you want to install Windows.
3. Select the partition with “BOOTCAMP” in its name (for example, Drive 0 Partition 2: BOOTCAMP).
4. In the advanced drive options, click Format. If you cannot see the Format option, click Drive options (advanced) to reveal it.
5. When the warning message appears, click OK. The Windows installer formats the Windows partition.
6. When the busy cursor disappears, click Next. The Windows installer proceeds to installation and displays the installation status.
7. When your Mac restarts to Windows 10, enter your login and password details and other settings. Windows takes you to your desktop and Boot Camp installer automatically opens.
8. Follow Boot Camp installer on-screen instructions to install hardware and software support.
9. When the installation completes, click Yes to restart.

You have an operational dual boot with two partitions on your hard disk. Its first partition contains OS X and its second partition contains Windows.

If you want to triple boot with Windows and Ubuntu, skip to 4. Installing rEFInd boot manager.

## Switching between OS X and Windows
In this section, you learn how to restart your Mac to OS X or Windows.

Whenever you want to restart to OS X, do one of the following:
- in the Windows system tray, click the Boot Camp icon and select Restart in Mac OS X
- at startup, hold down the option key (⌥) when you hear the startup sound and click the Mac OS X icon

Whenever you want to restart to Windows, do one of the following:
- open System Preferences > Startup Disk, select Boot Camp, and click Restart…
- at startup, hold down the option key (⌥) when you hear the startup sound and click the Boot Camp icon

If you need more help with Boot Camp Assistant, refer to Boot Camp Support from Apple website (https://www.apple.com/support/bootcamp/).

If you only want to dual boot with Windows, stop here.

## Installing rEFInd boot manager
Apple ships Macs with System Integrity Protection (SIP) on by default. SIP prevents accidental or malicious modifications of protected files and folders on your Mac. To install rEFInd, you disable SIP first.

## Disabling System Integrity Protection
In this section, you disable SIP security feature to allow the installation of rEFInd.

1. Start OS X.
2. Check the current status of SIP:
    1. From the Utilities folder in the Applications folder, open Terminal.
    2. Enter: csrutil status
    If the command returns System Integrity Protection status: enabled., SIP is on and you must disable it.
3. Restart in Recovery mode:
    1. Select   > Restart...
    2. When you hear the startup sound, press CMD (⌘) + R.
4. Disable SIP:
    1. From the Utilities menu, open Terminal.
    2. Enter: csrutil disable
    The command returns Successfully disabled System Integrity Protection. Please restart the machine for the changes to take effect.
    3. Select   >  Restart…

To check the new status of SIP, repeat step 2. The command returns System Integrity Protection status: disabled.

Note: To re-enable SIP when you complete Ubuntu installation, repeat steps 3 and 4 but enter csrutil enable instead of csrutil disable. The command returns Successfully enabled System Integrity Protection. Please restart the machine for the changes to take effect.

If you need more help with SIP, refer to:
- the “About System Integrity Protection on your Mac” page from Apple online support (https://support.apple.com/en-us/HT204899)
- the SIP section in rEFInd documentation (http://www.rodsbooks.com/refind/sip.html)

## Installing rEFInd
In this section, you run the refind-install script to install rEFInd.

1. From the Utilities folder in the Applications folder, open Terminal.
2. Enter the following command, where username is your account name and refind_directory is rEFInd uncompressed folder name:
sudo /Users/username/Desktop/refind_directory/refind-install
Example:
sudo /Users/John/Desktop/refind-bin-0.10.1/refind-install

The command returns Installation has completed successfully. Proceed to Ubuntu installation.

## Installing Ubuntu
Before you install Ubuntu on your Mac, you create a bootable Ubuntu installer drive and an Ubuntu partition manually with Disk Utility.

### Creating a bootable Ubuntu installer drive
In this section, you use Terminal commands to copy Ubuntu installation files onto your USB flash drive and make your USB flash drive bootable.

1. From the Utilities folder in the Applications folder, open Terminal.
2. Enter: diskutil list
    The command returns a table with the current list of devices.
3. Look for external disks and identify your USB flash drive (for example, /dev/disk2 (external, physical)).
4. Make a note of its identifier (for example, disk2).
5. Enter the following command, where diskN is the disk identifier: diskutil unmountDisk /dev/diskN
    Example: diskutil unmountDisk /dev/disk2
    The command returns Unmount of all volumes on diskN was successful.
6. Enter the following command, where username is your account name, ubuntu_ISO_file.iso is the Ubuntu 15.10 disk image name, and diskN is the disk identifier: sudo dd if=/Users/username/Desktop/ubuntu_ISO_file.iso of=/dev/rdiskN bs=1m
    Note: To avoid typing errors, drag and drop the ISO file from the Finder to Terminal to insert its full path.
    Example: sudo dd if=/Users/John/Desktop/ubuntu-15.10-desktop-amd64.iso of=/dev/rdisk2 bs=1m
7. Enter your password. File transfer starts. If an error occurs, refer to the Troubleshooting section.

When the operation completes, the command returns a transfer summary (number of bytes and total time). Do not remove the bootable Ubuntu installer drive.

### Creating an Ubuntu partition
In this section, you use Disk Utility to repartition your hard disk and allocate disk space to Ubuntu.

1. From the Utilities folder in the Applications folder, open Disk Utility.
2. In the left pane, select the main internal disk.
3. Click the Partition button. An overlaying panel asks you to choose how you want to resize the disk partitions.
4. In the Partition field, enter a relevant name for the new partition (for example, Ubuntu).
5. To specify how much disk space you want to allocate to Ubuntu, do one of the following:
    - drag the pie chart divider to increase or decrease the size of each partition
    - enter the size of the new partition in the Size field
    Note: Ubuntu requires at least 5 GB of free hard disk space. Make sure that you set the right partition size for Ubuntu because you cannot resize it later on.
6. Click Apply.
    Note: Do not change the Format option, as the Ubuntu installer formats the partition into the Linux default file system at a later stage.

In the main window of Disk Utility, you see the new partition. In the next section, you install Ubuntu in that partition.

### Running the Ubuntu installer
In this section, you use the Ubuntu installer from the bootable Ubuntu installer drive to install Ubuntu in custom mode.

#### Getting started
1. Restart your Mac. The rEFInd menu appears. If the rEFInd menu does not appear, refer to the Troubleshooting section.
    Note: To navigate the menu, use the arrow keys. To select an entry, press Return or Space. 
2. From the menu, click the Ubuntu drive icon. The Ubuntu installer initializes from your USB drive.
3. When the welcome screen appears, select your language from the list and click Install Ubuntu.
4. For best results, select the two options:
    - Download updates while installing
    - Install this third-party software
5. Click Continue.
6. If the Ubuntu installer cannot establish an Internet connection, select a Wi-Fi network from the list and enter the password.
7. When the Ubuntu installer asks which type of installation you want to perform, select Something else.
8. Click Continue.

The Ubuntu installer asks where you want to install Ubuntu.

#### Formatting the Ubuntu partition and installing Ubuntu

1. In the list of partitions, identify the Ubuntu partition by its name and size and select it.
2. Click Change.
3. Set parameters as follows:
Size|do not change
Use as|Ext4 journaling file system
Format the partition|☑
Mount point|/
4. Click OK. Back to the list of partitions, check the information for the Ubuntu partition.
5. From the Device for boot loader installation dropdown menu, select the Ubuntu partition.
    Note: Make sure to select the Ubuntu partition, and not the main partition. To allow you to choose which OS to run at startup, rEFInd must remain the default boot manager for the main partition.
6. Click Install Now.
7. When the warning message appears, click Continue. The Ubuntu installer formats the Ubuntu partition.
8. When the busy cursor disappears, follow the on-screen instructions to enter your location, keyboard layout, login and password details. The installer proceeds to installation and displays the installation status.
9. When the installation completes, click Restart Now.

You have an operational multi-boot configuration. When the rEFInd menu appears, choose the OS that you want to run. If you cannot start correctly, refer to the Troubleshooting section.

## Troubleshooting

Problem|Possible cause|Actions
---|---|---
Your Mac does not start from the bootable installer drive.|In some configurations, you may need to manually select the device that you want to start from.|<ol><li>Select  > Restart...</li><li>When you hear the startup sound, hold down the option key (⌥).</li><li>Click the USB flash drive icon.</li></ol>
The rEFInd menu does not appear at startup.|In some configurations, you may need to restart twice for the rEFInd menu to appear.|Restart again. If the rEFInd menu does not appear on the second restart, other software on your Mac may be responsible for interference.
When you select Ubuntu in the rEFInd menu, Windows starts instead.|The Ubuntu boot loader is on the Windows partition instead of the Ubuntu partition.|Use Boot-Repair to reinstall the Ubuntu boot loader on the Ubuntu partition (https://help.ubuntu.com/community/Boot-Repair).
When you try to execute the dd command, error dd: Invalid number ‘1m’, you are using GNU dd occurs.|With GNU Coreutils, ‘1m’ is not a valid number.|Enter the same command but replace bs=1m with bs=1M.
When you try to execute the dd command, error dd: /dev/diskN: Resource busy, make sure the disk is not in use occurs.|Your USB flash drive is busy.|1.Open Disk Utility (Applications > Utilities). 2. Click Unmount. 3. Try again.

## Legal Notice
©2016 EverLearning. All rights reserved. EverLearning and related trademarks, names, and logos are the property of EverLearning Limited and are registered and/or used in the U.S. and countries around the world.
Apple, Mac, and Boot Camp are trademarks of Apple Inc. Windows is a trademark of Microsoft Corporation. All other trademarks are the property of their respective owners.

This guide may not, in whole or part, be copied, photocopied, reproduced, translated, or reduced to any electronic medium or machine readable form without the prior agreement and written permission of EverLearning, except in the case of brief quotations embodied in critical reviews and certain other noncommercial uses permitted by copyright law.

EverLearning assumes no responsibility for any inaccuracies in this document and cannot be held responsible for any damage or data loss. EverLearning reserves the right to change, modify, transfer, or otherwise revise this publication without notice. Use this guide at your own risk.