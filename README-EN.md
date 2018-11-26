# asrock-z370m-pro4-hackintosh

Just for my hardware specifications, you can use it as a reference, don't use it directly. Here are some version infos:

macOS version：10.14.1 (18B75)

BIOS version：3.20

## Hardware Specifications

CPU: Intel i5 8400

Motherboard: [Asrock z370m Pro4](https://www.asrock.com/MB/Intel/Z370M%20Pro4/index.asp)

Graphic Card: [SAPPHIRE PULSE Radeon™ RX 560 4GD5](http://www.sapphiretech.com/productdetial.asp?pid=501EC1E9-91FB-41CD-BD65-31CEBEBCE178&lang=eng)

Wi-Fi & BT: BCM943602CS

RAM: Micron 8G DDR4 2666 x 2

SSD: Intel 760P 512G NVMe M.2

Graphic card and Wi-Fi & BT card are natively supported by macOS, work OOB.

## Installation Caveats

### Audio

In order to make audio work, Audio Inject's value must be `1`.

### Use USB 2.0 port to install macOS

macOS USB installer must be inseted into the USB 2.0 port on the rare of you motherboard. Otherwise, installation will be failed - [AppleUSBHostPort::disconnect: persistent enumeration failures](https://www.tonymacx86.com/threads/solved-appleusbhostport-disconnect-persistent-enumeration-failures-and-shows-stop-sign.265606/#post-1857030)

### Make USB work properly

Here are some symptoms if USB does't work properly

1. Unable to detect USB devices.
2. Computer wakes up immediatelly after sleep.
3. Limit USB 3.0's speed at 480 Mbps.
4. Need replug USB after reboot.

In order to make USB and sleep work properly we need to make a USB patch, macOS 10.14.1 has USB port limit, you need an eailer version of macOS, for example macOS 10.13.6.

**1 Remove USB port limit**

After installing macOS 10.13.6 you need to remove USB port limit, if you don't you'll only see 15 USB ports on FB Patcher. Here is the guide - [List of Hackintosh USB Port Limit Patches (10.14 Updated)](https://hackintosher.com/forums/thread/list-of-hackintosh-usb-port-limit-patches-10-14-updated.467/).

**2 Use FB Patcher to generate USB patch**

After USB port limit removal, reboot your computer, and follow this guide to make your own USB patch - [USB Port Patching](https://www.tonymacx86.com/threads/release-intel-fb-patcher-v1-6-5.254559/).

⚠️ "7. Reboot with -uia_exclude_hs boot flag" means replace `-uia_exclude_ss` with `-uia_exclude_hs`.

⚠️ After generating the patch file, you can remove custom flags and DSDTs that you added during this process.

**3 Store your USB patch file**

Store your USB patch file in a secure place, it's your own patch file, you can't find it anywhere else.

## How perfect?

Haven't found any issue yet.

## How to upgrade macOS

Don't upgraade immediately, wait for a couple of weeks after a new release and check compatibility issues on tonymacx86. Always backup your system before upgrading.

## USB port mapping

⚠️ Just for my case

HSXX means USB 2.0，SSXX means USB 3.0.

Rear of motherboard:

![port mapping](./images/motherboard-usb-mapping.png)

Bluetooth: HS05

Case front panle USB (up)：HS09 SS06

Case front panle USB (down)：HS09 SS06
