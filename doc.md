# Installation guide: Windows 10, Ubuntu 15.10, or both
For Macs with OS X El Capitan

## Legal Notice
©2016 EverLearning. All rights reserved. EverLearning and related trademarks, names, and logos are the property of EverLearning Limited and are registered and/or used in the U.S. and countries around the world.
Apple, Mac, and Boot Camp are trademarks of Apple Inc. Windows is a trademark of Microsoft Corporation. All other trademarks are the property of their respective owners.

This guide may not, in whole or part, be copied, photocopied, reproduced, translated, or reduced to any electronic medium or machine readable form without the prior agreement and written permission of EverLearning, except in the case of brief quotations embodied in critical reviews and certain other noncommercial uses permitted by copyright law.

EverLearning assumes no responsibility for any inaccuracies in this document and cannot be held responsible for any damage or data loss. EverLearning reserves the right to change, modify, transfer, or otherwise revise this publication without notice. Use this guide at your own risk.

## Purpose of this guide	
This guide describes how to install the latest versions to date of Windows and Ubuntu (Windows 10 and Ubuntu 15.10) on a Mac that runs OS X El Capitan (10.11).

In this guide, you learn how to:
- use Boot Camp Assistant to install Windows 10
- install rEFInd boot manager to start more than one Operating System (OS)
- install Ubuntu 15.10
- switch between the OSes
It does not describe how to install OS X El Capitan, install earlier or future versions of Windows or Ubuntu, or upgrade existing installations of Windows or Ubuntu. In this guide, the chapters that describe Windows installation and Ubuntu installation are independent. Depending on your needs, you can either follow this guide step by step or skip the sections that do not apply to your installation type.

## Audience for this guide

Caution
{: .label .label-red }
This guide contains procedures that require you to use advanced functionalities, disable vital components of your Mac, and alter the hard disk structure. Before you proceed, make sure that you understand the concept of partitioning and that you have basic knowledge of all three OSes.

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
