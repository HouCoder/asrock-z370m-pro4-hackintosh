# asrock-z370m-pro4-hackintosh

OpenCore is more advanced than Clover in many ways, check out the [clover-deprecated](https://github.com/HouCoder/asrock-z370m-pro4-hackintosh/tree/clover-deprecated) branch if you want to see Clover configurations.

This project can not be used as is, if you want to use it beaware these two issues.

1. You need to generate `PlatformInfo` -> `Generic` by yourself, see [corpnewt/GenSMBIOS](https://github.com/corpnewt/GenSMBIOS).
2. Do not use `OC/Kexts/USBPorts.kext`.

## Hardware Specifications

CPU: Intel i5 8400

Motherboard: Asrock Z370M Pro4

Graphic Card: SAPPHIRE PULSE Radeon™ RX 560 4GD5

Wi-Fi & BT: BCM943602CS

RAM: Micron 8G DDR4 2666 x 4

SSD0: Intel 760P 512G NVMe M.2 (macOS)

SSD1: Samsung 970 EVO Plus 250G（macOS）

HDD0: Seagate 4TB (time-machine and file storage)

Display0: Dell U2718QM

Display1: Dell U2414H

Wi-Fi & BT are natively supported by macOS, work out of box.

## What's working

- [x] Sleep and awake
- [x] Multi-monitor support
- [x] Bluetooth, Wi-Fi and ethernet
- [x] iMessage, Handoff, Continuity, FaceTime and AirDrop
- [x] Audio in/out put
- [x] Headless Intel iGPU
- [x] Time Machine
- [x] Boot into Recovery Mode

*It works just like a genuine Mac.*

## BIOS Settings

BIOS version: 3.20

Advanced \ Chipset Configuration → Vt-d : Disabled

Advanced \ Super IO Configuration → Serial Port: Disabled

Advanced \ USB Configuration → XHCI Hand-off : Enabled

Advanced \ Chipset Configuration → Share Memory : 128MB

Advanced \ Chipset Configuration → IGPU Multi-Monitor : Enabled

## Caveats

### CPU

[SSDT-PLUG](https://github.com/acidanthera/OpenCorePkg/blob/master/Docs/AcpiSamples/SSDT-PLUG.dsl) requires the correct CPU ID on your system and compile it to an aml file, without it you won't see Powernap option in Energy Saver panel.

Here we use [MaciASL](https://github.com/acidanthera/MaciASL) to find the correct CPU ID, open MaciASL and search `processor`, the first match is your CPU ID:

![MaciASL](images/MaciASL.png)

Then change `External (_PR_.CPU0, ProcessorObj)` to `External (_PR.PR00, ProcessorObj)`，`Scope (\_PR.CPU0)` to `Scope (\_PR.PR00)` in SSDT-PLUG.dsl.

Last but not least, in MaciASL click File -> Save As..., set File Format to `ACPI Machine Language Binary` and click OK.

### FileVault

No, don't use it, let's keep it simple.

### Enegy Saver

Disable Power Nap, it may wake your Hackintosh up during sleep.

### Audio

To make audio work, AppleALC's layout id must be `1`, you can either add `alcid=1` to `boot-args` or use [gfxutil](https://github.com/acidanthera/gfxutil) to get the device ID and set `layout-id`'s value to `01000000` under DeviceProperties / Add / [your audio device ID].

```
➜  gfxutil-1.78b-RELEASE ./gfxutil -f HDEF
DevicePath = PciRoot(0x0)/Pci(0x1f,0x3)
```

![audio-device-injection](./images/audio-device-injection.png)

### Use USB 2.0 port to install macOS

Recommend to use a USB 2.0 port to install macOS if you have not configured your USB patch - [AppleUSBHostPort::disconnect: persistent enumeration failures](https://www.tonymacx86.com/threads/solved-appleusbhostport-disconnect-persistent-enumeration-failures-and-shows-stop-sign.265606/#post-1857030).

### USB Port Configuration

Recommend to generate your own USB port map file - [The New Beginner's Guide to USB Port Configuration](https://www.tonymacx86.com/threads/the-new-beginners-guide-to-usb-port-configuration.286553/).

### iGPU

Just follow the steps here - [Coffee Lake / DeviceProperties](https://github.com/dortania/OpenCore-Install-Guide/blob/master/config.plist/coffee-lake.md#deviceproperties).

### Data backup

Hackintosh or genuine Mac, it's always a good thing to use Time Machine to backup your data.

## How to upgrade macOS

1. Backup your system, suggest to use [SuperDuper](https://www.shirt-pocket.com/) make a bootable backup, you can boot from your backup and restore the whole system if the update fails.

2. Update kexts、UEFI drivers and OpenCore, recommend to use [Hackintool](https://www.insanelymac.com/forum/topic/335018-hackintool-v286/) to update them.

3. Be cautious, check online forums and OpenCore doc for potential issues before updating.

## System upgrade history

| Version | Date | Comment |
|-------------------------------|-----------|----------|
| macOS Mojave 10.14.2 (18C54)  | 2018.12.7 | No issue |
| macOS Mojave 10.14.3 (18D42)  | 2019.1.23 | No issue |
| macOS Mojave 10.14.3 (18D109) | 2019.2.11 | No issue |
| macOS Mojave 10.14.4 (18E226) | 2019.3.26 | No issue |
| macOS Mojave 10.14.5 (18F132) | 2019.5.14 | No issue |
| macOS Mojave 10.14.6 (18G84)  | 2019.7.23 | No issue |
| macOS Mojave 10.14.6 (18G87)  | 2019.8.6  | No issue |
| macOS Mojave 10.14.6 (18G95)  | 2019.8.31 | No issue |
| macOS Mojave 10.14.6 (18G103) | 2019.9.27 | No issue |
| macOS Catalina 10.15 (19A583) | 2019.10.14 | No issue |
| macOS Catalina 10.15 (19A602) | 2019.10.18 | No issue |
| macOS Catalina 10.15.1 (19B88) | 2019.11.1 | No issue |
| macOS Catalina 10.15.2 (19C57) | 2019.12.15| No issue |
| macOS Catalina 10.15.4 (19E287) | 2020.4.9| No issue |
| macOS Catalina 10.15.5 (19F96) | 2020.5.30| No issue |
| macOS Catalina 10.15.6 (19G73) | 2020.8.4| No issue |
| macOS Catalina 10.15.6 (19G2021) | 2020.8.13| No issue |
| macOS Catalina 10.15.7 (19H15) | 2020.11.8| No issue |

## USB port mapping

HSXX means USB 2.0，SSXX means USB 3.0.

Onboard ports:

![port mapping](./images/motherboard-usb-mapping.png)

Bluetooth: HS05

Front panle USB (up)：HS09 SS06

Front panle USB (down)：HS09 SS06

## Benchmarks

### Geekbench CPU

<img src="./images/geekbench-cpu.png" alt="geekbench-cpu-score" width="400px">

### Geekbench GPU

<img src="./images/geekbench-gpu-opengl.png" alt="geekbench-gpu-opengl-score" width="400px">

### Cinebench

<img src="./images/cinebench.png" alt="cinebench-score">

## Some useful links

1. [Dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/)
