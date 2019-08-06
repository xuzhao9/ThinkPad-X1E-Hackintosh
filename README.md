# xz's Hackintosh profile on Thinkpad X1E

## Hardware: Thinkpad X1 Extreme Gen 1

- CPU: Core i7-8750H 2.2GHz
- Memory: 16G 2667MHz DDR4
- SSD1: SAMSUNG PM981 512 GB
- SSD2: Intel 660P 1T NVMe
- Display: 1080p, non-touch
- Graphics: Intel UHD Graphics 630
- Wireless: Intel Wireless-AC 9260
- Sound card: Realtek ALC285
- BIOS: v1.23
- OS: OS X Mojave 10.14.6

## Result

<img align="middle" src="https://github.com/xuzhao9/Thinkpad-X1E-Hackintosh/blob/master/screenshots/overview.png" alt="Overview" />

### What works

- Base OS
- Sleep, wakeup, hibernation
- Brightness, function keys for brightness control, NightShift
- Intel Ethernet LAN (mini RJ45) 
- Touchpad and TrackPoint
- Audio, function keys for volume control, headphone jack
- USB 3.1 ports

### What doesn't work

- Function keys Fn+F7-F12
- Intel Wireless and Bluetooth
- Smooth brightness adjustment
- SSD1: SamSung PM981 512GB
- Nvidia Graphics Card 1050Ti
- Thunderbolt 3 ports
- HDMI output to external display

## Add-ons

- [USB Wifi Dongle 1200M 802.11ac](https://www.amazon.ca/gp/product/B07P7JQVKB/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
  This model requires the [Realtek 8811AU driver](http://u6v.cn/5ovGu2), which works on Mojave but not on Catalina.
  If you want to use Catalina with this USB dongle, try [Chris1111's driver](https://github.com/chris1111/Wireless-USB-Adapter) (Disclaimer: haven't tested).

## DSDT and SSDT modifications

### DSDT
I made my own `DSDT.aml` from the vanilla version.

- Removed the two redundant lines of `One`to fix the compiling error.
- Applied the [RehabMan/ThinkPad X230i patch](https://github.com/RehabMan/Laptop-DSDT-Patch/blob/master/battery/battery_Lenovo-X230i.txt) to fix battery indicator.
- Fixed brightness function keys (Fn+F5/F6) by applying the _Q14 and _Q15 patch.

### SSDT

- Added SSDT_NVMe-Pcc.aml to disable the PM981 SSD1, which will cause the kernel panic unpredictably.

## kext versions and modifications

- AppleALC.kext v1.3.9

  Set `alcid=21` in `E/C/config.plist`. According to [AppleALC support matrix](https://github.com/acidanthera/AppleALC/wiki/Supported-codecs), either layout 11 or layout 21 should work. However, sound card stops working unpredictably when using layout 11. Use layout 21 instead solves the problem.
  
- FakeSMC.kext
- Lilu.kext
- NoTouchID.kext
- USBInjectAll.kext
- VoodooPS2Controller.kext
- WhateverGreen.kext
- L/E/ACPIbatterymanager.kext
- L/E/Codeccommander.kext
- L/E/HibernationFixup.kext
- L/E/IntelMausiethernet.kext
- L/E/XHCI-unsupported.kext

# Misc

OS X is the only operating system on this machine. No dual boot.

# Acknowledgements

- [zysuper's Hackintosh](https://github.com/zysuper/Thinkpad-X1-extreme-EFI) 
- [Errrneist's Hackintosh](https://github.com/Errrneist/Hackintosh-Thinkpad-X1-Extreme)
- [RehabMan's DSDT patches](https://github.com/RehabMan/Laptop-DSDT-Patch)
- [Telegram Hackintosh Group](https://t.me/joinchat/FSuP2UI4ALt1uIVmQ5E6lg)
