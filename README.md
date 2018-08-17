# High Sierra Hackintosh Gigabyte GA-H110MSTX-HD3

## Build Specifications

* **Gigabyte GA-H110MSTX-HD3**
* **Intel i5-7500T Kaby Lake - HD Graphics 630**
* **SilverStone Technology 120W AD120-STX**
* **Kingston SSDNow (SMS200S3/240G)**
* **Patriot Signature Line 2x8GB (PSD38G1333SK)**
* **Broadcom BCM94352Z 802.11 AC / Bluetooth 4.0**

## Download

* High Sierra

> https://itunes.apple.com/us/app/macos-high-sierra/id1246284741

* MultiBeast 10.4.x - High Sierra

> https://www.tonymacx86.com/resources/multibeast-10-4-0-high-sierra.401/

* UniBeast 8.3.x - High Sierra

> https://www.tonymacx86.com/resources/unibeast-8-3-2-high-sierra.383/

## BIOS Settings

### Save & Exit Tab

* Load Optimized Defaults

### BIOS Features Tab

* Fast Boot - **Disabled**
* LAN PXE Boot Option ROM - **Disabled**
* Storage Boot Option Control - **UEFI**
* Windows 8/10 Features - **Other OS**

### Peripherals Tab

#### Trusted Computing Section

* Security Device Support - **Disabled**

#### Network Stack Section

* Network Stack - **Disabled**

#### USB Configuration Section

* Legacy USB Support - **Auto**
* XHCI Hand-Off - **Enabled**

### Chipset Tab

* VT-d - **Disabled**
* Wake on LAN - **Disable**
* IOAPIC 24-119 Entries - **Enabled**

## Installation

### Unibeast

On your host machine, use Unibeast to create a UEFI USB installer.

Copy the `BCM94352Z_Patch` and `GA-H110MSTX-HD3.multibeast.mb` and `MultiBeast` on to the USB stick.

### Boot

Boot the system from the USB stick which you created.

### Format Drive

When the installer starts:

* Open Disk Utility
* Click your system drive
* Click Erase

> Name: Hackintosh HD
> 
> Format: Mac OS Extended (Journaled)
> 
> Scheme: GUID Partition Map

* Click the Erase button
* Close the confirmation
* Command-Q Disk Utility

### Initial Setup

Select Install macOS, then the rest of the install should be obvious.

### Install

Clover will load, select the drive with the description `Boot macOS install from Hackintosh HD`.

This will bring up an Apple with a loading bar, then it'll show **Installing on "Hackintosh HD"** and *About 18 minutes remaining.* 

This will go for a minute or so, then the machine will reboot.  After reboot, again select `Boot macOS install from Hackintosh HD`.

The install will complete and you can restart the system.

### Post Install

Again boot from the USB, when Clover loads select the option for `Boot macOS from Hackintosh HD`.  Again it'll show the Apple with the loading bar.

The standard Welcome screen should appear and you complete as normal.

### First Boot

After first boot, open the USB stick.  I generally copy MultiBeast into my Applications.  Open MultiBeast and then click the **Load** option and open the `GA-H110MSTX-HD3.multibeast.mb` file, then click **Build**.  This will automatically configure it for you.

You may reboot here or continue on to install the Wifi & BT kexts.

### Wifi & BT - Broadcom BCM94352Z

https://hackintosher.com/forums/thread/enabling-third-party-broadcom-wlan-802-11a-b-g-n-wifi-bluetooth-cards-on-a-hackintosh-bcm94352z-bcm94322.6/

Open **Terminal**

Lookup Your EFI Partition

		diskutil list

It will display something like the following:

		/dev/disk0 (internal, physical):
		   #:                       TYPE NAME                    SIZE       IDENTIFIER
		   0:      GUID_partition_scheme                        *240.1 GB   disk0
		   1:                        EFI EFI                     209.7 MB   disk0s1
		   2:                 Apple_APFS Container disk1         239.8 GB   disk0s2
		
		/dev/disk1 (synthesized):
		   #:                       TYPE NAME                    SIZE       IDENTIFIER
		   0:      APFS Container Scheme -                      +239.8 GB   disk1
		                                 Physical Store disk0s2
		   1:                APFS Volume HackintoshSystem        20.7 GB    disk1s1
		   2:                APFS Volume Preboot                 20.8 MB    disk1s2
		   3:                APFS Volume Recovery                519.0 MB   disk1s3
		   4:                APFS Volume VM                      20.5 KB    disk1s4
		
		/dev/disk2 (internal, physical):
		   #:                       TYPE NAME                    SIZE       IDENTIFIER
		   0:      GUID_partition_scheme                        *31.0 GB    disk2
		   1:                        EFI                         209.7 MB   disk2s1
		   2:                  Apple_HFS                         30.6 GB    disk2s2

Note that this shows two `EFI` partitions, one is on my USB stick the other is my SSD.

Look at the `SIZE` of the `GUID_partition_scheme` this will help you find your hard drive or SSD.  Obviously my USB is the one marked `*31.0 GB` which is `/dev/disk2`.  The SSD is marked `*240.1 GB` so the `EFI` partition on my SSD is `/dev/disk0s1`, yours may vary.

Make an mount point for your EFI partition and mount it.

		mkdir ~/Desktop/efimount
		sudo mount -t msdos /dev/disk0s1 ~/Desktop/efimount
		open ~/Desktop/efimount/EFI/CLOVER/kexts/Other

Copy all of the **kext files** from this repo's `BCM94352Z_Patch` path to the now open finder window which should be `~/Desktop/efimount/EFI/CLOVER/kexts/Other`.

Close the finder window and unmount the path.

		sudo umount ~/Desktop/efimount
		
Reboot the hackintosh.

		sudo reboot

### Post Reboot

Remove the USB drive and you should boot directly into Clover, here you should select `Boot macOS from Hackintosh HD`.

## Enable / Disable System Integrity Protection (SIP) in Clover Boot Loader

https://hackintosher.com/forums/thread/enable-disable-system-integrity-protection-sip-on-a-hackintosh.53/

* Boot into Clover EFI Menu
* Select Options (gear icon) using arrow keys
* Select System Parameters
* Select System Integrity Protection
* Change to enable/disable

> **Disable SIP** - Check: Allow Untrusted Kexts, Allow Unrestricted FS, Allow Task for PID, Allow Unrestricted Dtrace, Allow Unrestricted NVRAM
> 
> **Enable SIP** - Uncheck everything

* Select Return
* Select Return again
* Select Return again...
* Boot macOS partition




