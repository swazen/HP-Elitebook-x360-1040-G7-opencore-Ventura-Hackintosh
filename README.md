# HP Elitebook x360 1040 G7 Opencore Ventura Hackintosh

Inspired by olarila method by [MaLd0n](https://www.olarila.com/topic/20908-easy-fast-and-perfect-vanilla-hackintosh-clover-and-opencore-windows-linux-or-macos/) + work of [kodowiec](https://github.com/kodowiec/HP-Elitebook-x360-1040-G6-Opencore) + french tutorial by [Mikaël GUILLERM](https://tinyurl.com/4buk3nrt).

I share a complete EFI/OC ready to use, you just need to adapt SMBIOS values with GenSMBIOS, i 've delete my personnal data in config.plist. 
Do not start macOS Ventura installer without moded your SMBIOS values in config.plist with GenSMBIOS otherwise it's an assured failure.

Be patient, be zen and enjoy !

## Specs HP (all native)

* Intel Core i5-10210U Comet Lake-U @1.6GHz
* Intel UHD Graphics (9.5 gen - rev 5, [same HD360 architecture with base clock @300Mh](https://www.techpowerup.com/gpu-specs/intel-comet-lake-gt2.g925)).
* 16 GB DDR3
* 512 Go SSD WDC SN520 NVMe 
* Intel AX201 wifi6 /BT
* 14" 1080P touch screen
* BIOS Version : S93 ver. 01.10.00 from 2022/07/18

## Specs Hackintosh 

* SMBIOS MacbookPro16.1 (late 2019)
* macOS Ventura 13.0.1
* OpenCore 0.8.5
* Full hardware accelerated (Metal 2)
* Geekbench 5  : [668 single-core, 3091 multi-core](https://browser.geekbench.com/v5/cpu/18642368)

## What works

* WIFI (need Heliport, view HowTo)
* Bluetooth
* Webcam
* HDMI
* Trackpad with gestures
* Touchscreen
* USB 3 & USB-C Ports (but not optimized)
* Natives function keys for volume and brightness
* Battery status
* Speakers
* Headphone jack

## What doesn't work (todo)

* **TouchID** (HP EliteBook has a fingerprint sensor but isn't working at the moment)
* **Internal mic** (use headphone/mic in USBC)
* **Sleep wake up** (switch off sleep mode in ventura, USB mapping can normally fix the sleep issue)

## ssdt
* **SSDT-AWAC**
* **SSDT-EC-USBX-LAPTOP**
* **SSDT-OLARILA-MOBILE**
* **SSDT-SSDT-PLUG-DRTNIA**
* **SSDT-PLNF** 
* **SSDT-USBX** 
* **SSDT-XOSI**

## kexts:
* AppleALC.kext
* BlueToolFixup.kext
* BrightnessKeys.kext
* CpuTscSync.kext
* ECEnabler.kext
* IntelBluetoothFirmware.kext
* IntelBTPatcher.kext
* itlwm.kext
* Lilu.kext
* USBInjectAll.kext
* VirtualSMC.kext (with plugins SMCBatteryManager.kext, SMCLightSensor.kext and SMCProcessor.kext)
* VoodooI2C.kext
* VoodooI2CHID.kext
* VoodooPS2Controller.kext
* WhateverGreen.kext
* XHCI-unsupported.kext


## How to make your HP Elitebook x360 1040 G7 Hachintosh

1. download my [EFI.7z](https://github.com/swazen/HP-Elitebook-x360-1040-G7-opencore-Ventura-Hackintosh/blob/main/EFI.7z) archive which contains EFI/OC folder for HP EliteBook x360 1040 G7 and extract where you want on your windows system (hack made under Windows 11 21H2)
2. download Ventura raw image on [olarila.com](https://direct-link.net/462274/olarila-ventura-final-mf) and unzip
3. download [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) for generate your personnal MacbookPro16.1 SMBIOS and unzip
4. open GenSMBIOS.bat and choose option 1 for update the mac database, and 2 for select config.plist stocked in EFI/OC folder by dragndrop and finally option 3 for generate SMBIOS infos in the config.plist selected. Choose MacbookPro16.1 for generate yours serial, board serial, SmUUID and Apple ROM.
5. download [balena etcher](https://www.balena.io/etcher/), install it and flash the raw image of ventura on USB stick or drive (min 16Go). Stay your USB drive connected.
6. download [minitool partition wizard](https://www.minitool.fr/gestionnaire-partition/partition-wizard-accueil.html), install it and assign a letter to EFI partition of your USB drive for mount it.
7. download [explorer++](https://explorerplusplus.com/download), run it with admin privileges, delete EFI folder on EFI partition and past your EFI folder (which contains BOOT and OC).
8. reboot and press Esc/F10 to enter bios settings, go security tabs and desactivate sure start and secure start, go advanced tabs and unchek HP Sure recover, wake on lan and fix video memory to 64Mo and desactivate power management. Save and exit.
9. reboot and press F9 to boot on your USB EFI and install ventura (be patient). Reboots are frequent, choose USB EFI every time.

## Post install
* patches are allready installed but you need put your EFI folder on your SSD for start your hackintosh without USB drive. Exist many macOS app for mount EFI like [ESP mounter pro](https://www.olarila.com/files/Utils/ESP%20Mounter%20Pro.app_v1.9.1.zip). Just mount both EFIs partitions, delete folder EFI on SSD, copy USB EFI folder and paste on SSD.
* for wifi, download and install [Heliport](https://github.com/OpenIntelWireless/HeliPort) and switch off native wifi.
* for a native scaled display (vectorial) you must download and install [one-key-hidpi](https://github.com/xzhih/one-key-hidpi).
