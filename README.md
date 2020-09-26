# Dell PowerEdge T30 Hackintosh

**** NOTE THIS IS A WORK IN PROGRESS AND NEEDS A BUNCH OF CLEANUP/TUNING ****

![A24G_1_201708251625270941](https://user-images.githubusercontent.com/849044/88466592-c090b200-ce82-11ea-9990-4153b817b115.jpg)

## System Specs

![Screen Shot 2020-09-21 at 10.38.33 PM](https://user-images.githubusercontent.com/849044/93849315-b875a880-fc60-11ea-8dad-da2a51beb5ba.png)

| Part        | Model Number
| ---         | ---
| CPU         | Intel(R) Xeon(R) CPU E3-1225 v5 @ 3.30GHz (Quad Core)
| PSU         | Corsair 500W 80 Plus Gold w/ 24-pin to 8-pin adapter
| Motherboard | Dell 07T4MC
| BIOS        | 1.3.1
| Chipset     | Intel C236
| Memory      | Corsair Vengeance LPX 64GB DDR4-3200MHz non-ECC 16GB x 4 (PN: CMK32GX4M2B3200C16)
| GPU         | Intel HD P530 iGPU
|             | MSI RX 570 GAMING X 8GB - slot 1
| Monitor     | LG 27UK650-W 27" 4K IPS w/ HDR10
| Display Cable | included LG DP cable
| Storage     | Samsung 830 Series 250GB SSD ()
|             | PNY CS900 240GB SSD (Revision CS900J13) x2
|             | Toshiba MQ01ABD100 1TB HDD
| Bluetooth   | ASUS USB-BT400 (Firmware: v14 c4096)
| Wifi        | ASUS AC1200 USB-AC53 Nano (using chris111's drivers)
| Ethernet    | Intel I219LM2 (onboard)
| USB         | Intel 100 Series/C230 Series USB 3.00 xHCI Controller
| Sound       | Realtek ALC899 (Layout ID: 3)
| Keyboard    | Logitech MX Keys (connected using Logitech Unified receiver)
| Mouse       | Logitech M590 (connected using Logitech Unified receiver on a USB extension to prevent lag from RF interference)
| Bootloader  | Clover r5120

## BIOS Configuration

- optimized defaults
- storage to AHCI mode
- enable USB powershare
- set preferred graphics to AMD (don't use auto! set to P530 if you are using the iGPU)

The rest of the recommended settings are already the defaults used by this BIOS. DVMT is 32MB for the iGPU and setup doesn't expose a means to change this. I modified it via `setup_var` and the modified GRUB shell while trying to get an iGPU-only setup working with a 4k display with no luck. Many forum posts say not to try and change DVMT pre-alloc via GRUB; if you break your system don't be upset as you were warned.

[add screenshots]

## UEFI Modifications

These are __MY__ settings given BIOS version 1.3.1 and board 07T4MC. You need to check these offsets and make sure that they're correct for your machine before trying to change things.

1. Disable __CFG Lock__

`setup_var 0xAF 0x0`

2. Enable __Above 4GB MMIO BIOS Assignment__

`setup_var 0x355 0x1`

This EFI will not work unless you make both UEFI modifications. If you're not up for that, you'll need to add `npci=0x2000` to your boot args, enable `KernelPm` and `AppleIntelCPUPM` in your `config.plist`, and add memory configuration info (slot, size, brand, and type).

## Readme

- Read everything first and be careful
- Tested on macOS Catalina 10.15.6 (vanilla)

## macOS Updates

- fresh install of 10.15.6
- updated to 10.15.7 without any issues (did not update clover or kexts since everything was running perfectly smooth as-is)

## Geek Bench

[add screenshot]
