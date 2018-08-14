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

> https://itunes.apple.com/us/app/macos-high-sierra/id1246284741?mt=12&l=en-us&ls=1

* MultiBeast 10.4.x - High Sierra

> https://www.tonymacx86.com/resources/multibeast-10-4-0-high-sierra.401/

* UniBeast 8.3.x - High Sierra

> https://www.tonymacx86.com/resources/unibeast-8-3-2-high-sierra.383/

* Other [Useful Tools](/tools.md)

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

## Broadcom BCM94352Z

https://hackintosher.com/forums/thread/enabling-third-party-broadcom-wlan-802-11a-b-g-n-wifi-bluetooth-cards-on-a-hackintosh-bcm94352z-bcm94322.6/

### Steps

1. Mount EFI partition
2. Download latest [OS-X-Fake-PCI-ID](https://bitbucket.org/RehabMan/os-x-fake-pci-id/downloads/)
3. Unzip / Open: **./OS-X-Fake-PCI-ID/Release**
4. Open Release folder
5. Copy: *FakePCIID.kext* & *FakePCIID_Broadcom_WiFi.kext* to: **EFI/CLOVER/kexts/Other**
7. Download latest [OS-X-BrcmPatchRAM](https://bitbucket.org/RehabMan/os-x-brcmpatchram/downloads/)
8. Unzip / Open: **./OS-X-BrcmPatchRAM/Release**
9. Copy: *BrcmFirmwareData.kext* / *BrcmPatchRAM2.kext* / *BrcmNonPatchRAM2.kext* to: **EFI/CLOVER/kexts/Other**
10. Reboot

### Issues

Some may have issues putting these kexts in the Other folder where the Kexts wont always work or maybe Wifi is working, but bluetooth isn't. With Clover some kexts can fail to properly initiate so you can try migrating BrcmPatchRAM to /Library/Extensions:

* Move *BrcmPatchRAM2.kext* & *BrcmNonPatchRAM2.kext* to **/Library/Extensions**
* Delete *BrcmFirewareData.kext* from **EFI/CLOVER/kexts/Other**
* Copy *BrcmFirmwareRepo.kext* from **Release** folder to: **/Library/Extensions**

## Enable & Disable System Integrity Protection (SIP) in Clover Boot Loader

https://hackintosher.com/forums/thread/enable-disable-system-integrity-protection-sip-on-a-hackintosh.53/

1. Boot into Clover EFI Menu
2. Select Options (gear icon) using arrow keys
3. Select System Parameters
4. Select System Integrity Protection
5. Change to enable/disable
> **Disable SIP** - Check: Allow Untrusted Kexts, Allow Unrestricted FS, Allow Task for PID, Allow Unrestricted Dtrace, Allow Unrestricted NVRAM
> **Enable SIP** - Uncheck everything
6. Select Return
7. Select Return again
8. Select Return again...
9. Boot macOS partition




