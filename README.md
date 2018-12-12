# asrock-z370m-pro4-hackintosh

[English version](./README-EN.md)

该项目只针对我的配置，仅供参考，不要盲目使用。一些软件版本信息：

macOS version：10.14.1 (18B75)

BIOS version：3.20

## 硬件

CPU：Intel i5 8400

主板：[Asrock z370m Pro4](https://www.asrock.com/MB/Intel/Z370M%20Pro4/index.asp)

显卡：[蓝宝石RX560 4G D5 白金版 OC (75W)](http://www.sapphiretech.com/productdetial.asp?pid=C12A4F7E-B791-4DDB-8D32-47BB6ACA68BD&lang=chs)

Wi-Fi 和蓝牙：BCM943602CS

内存：Micron 8G DDR4 2666 x 2

硬盘：Intel 760P 512G NVMe M.2

显卡、 Wi-Fi 和蓝牙芯片在 macOS 下插上就能用，不需要任何配置。

## BIOS 设置

Advanced \ Chipset Configuration → Vt-d : Disabled

Advanced \ Super IO Configuration → Serial Port: Disabled

Advanced \ USB Configuration → XHCI Hand-off : Enabled

Advanced \ Chipset Configuration → Share Memory : 128MB

Advanced \ Chipset Configuration → IGPU Multi-Monitor : Enabled

## 安装注意事项

### 音频

为了让音频正常工作，Audio Inject 的值必须为 `1`。

### 使用 USB 2.0 接口安装

制作完 USB 安装盘后务必插在主板背部的 USB 2.0 的接口上安装，否则安装会报错 - [AppleUSBHostPort::disconnect: persistent enumeration failures](https://www.tonymacx86.com/threads/solved-appleusbhostport-disconnect-persistent-enumeration-failures-and-shows-stop-sign.265606/#post-1857030)。

### 让 USB 顺利工作

USB 不正常工作的表现有：

1. USB 不能识别。
2. 睡眠后会立即醒来。
3. USB 3.0 的速度会限制在 480 Mbps。
4. 重启后 USB 设备丢失，需要重新插拔。

为了让 USB 和睡眠正常的工作需要制作 USB 补丁，macOS 10.14.1 下有 USB 端口限制，需要安装之前版本的 macOS 来制作 USB 补丁，以 macOS 10.13.6 下制作的安装补丁为例。

**1 移除 USB 端口限制**

安装完 macOS 10.13.6 后需要移除 USB 端口限制，如果不移除你只能在 FB Patcher 上看到 15 个 USB 端口。移除方法请参考 [List of Hackintosh USB Port Limit Patches (10.14 Updated)](https://hackintosher.com/forums/thread/list-of-hackintosh-usb-port-limit-patches-10-14-updated.467/)。

**2 使用 FB Patcher 制作 USB 补丁**

安装完上面的补丁后重启电脑应该可以看到所有的 USB 接口了，按照 [USB Port Patching](https://www.tonymacx86.com/threads/release-intel-fb-patcher-v1-6-5.254559/) 的教程来制作属于你自己的 USB 补丁。

**3 保存好制作的补丁**

补丁制作完成后一定要好好保存，因为是针对自己电脑独有的文件，网上找不到第二份。

## 已知的一些问题

### 睡眠后小概率出现蓝牙不可用的情况

重启下蓝牙服务即可：`` $ sudo kill -9 `pgrep bluetoothd` `` - [Restart Bluetooth Daemon on Mac OS X without restarting](https://gist.github.com/nicolasembleton/afc19940da26716f8e90#gistcomment-2636787)。


## 升级系统怎么办？

不要第一时间升级，新系统推送后过两周去社区看看问题反馈。决定升级前备份好系统，即使升级失败也能回滚到历史版本。

## 升级记录

| 版本 | 日期 | 备注 |
|------------------------------|-----------|----------|
| macOS Mojave 10.14.2 (18C54) | 2018.12.7 | 正常升级，无异常 |

## USB 端口映射关系

HSXX 代表的是 USB 2.0，SSXX 代表的是 USB 3.0。

主板背部：

![port mapping](./images/motherboard-usb-mapping.png)

蓝牙：HS05

机箱前置 USB（上）：HS09 SS06

机箱前置 USB（下）：HS10 SS05

## 参考链接：

1. [如何正确的黑苹果](https://catty-house.blogspot.com/2018/10/hackintosh.html)
