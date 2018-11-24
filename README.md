# asrock-z370m-pro4-hackintosh

该项目只针对我的配置，仅供参考，不要盲目使用。软件版本信息：

macOS version：10.14.1 (18B75)

BIOS version：3.20

## 硬件

CPU: Intel i5 8400

主板：[Asrock z370m Pro4](https://www.asrock.com/MB/Intel/Z370M%20Pro4/index.asp)

显卡：[蓝宝石RX560 4G D5 白金版 OC (75W)](http://www.sapphiretech.com/productdetial.asp?pid=C12A4F7E-B791-4DDB-8D32-47BB6ACA68BD&lang=chs)

Wi-Fi&BT：BCM943602CS

内存：Micron 8G DDR4 2666 x 2

硬盘：Intel 760P系列 512G NVMe M.2

显卡和 Wi-Fi&BT 在 macOS 下插上就能用，不需要任何配置。

## 安装注意事项

### 使用 USB2.0 接口安装

制作完成 USB 安装盘后务必插在 USB2.0 的接口上安装，否则安装会报错。

### USB port patching

为了让 USB 和睡眠正常的工作需要使用制作 USB 补丁，macOS 10.14.1 下有 USB 端口限制，需要安装之前的版本来制作 USB 补丁，以 macOS 10.13.6 下制作的安装补丁为例。

注意事项：

1 安装完 macOS 10.13.6 后需要使用 Clover 打 USB 补丁，参考 [List of Hackintosh USB Port Limit Patches (10.14 Updated)](https://hackintosher.com/forums/thread/list-of-hackintosh-usb-port-limit-patches-10-14-updated.467/)。


2 安装完补丁后重启电脑，按照 [USB Port Patching](https://www.tonymacx86.com/threads/release-intel-fb-patcher-v1-6-5.254559/) 的教程来制作属于你自己的 USB 补丁。（⚠️：这篇教程里面的第七步 Reboot with -uia_exclude_hs boot flag 的意思是将第三步添加的 `-uia_exclude_ss` 替换为 `-uia_exclude_hs`）。

3 补丁制作完成后一定要好好保存，因为是针对自己电脑独有的文件，网上找不到第二份。

## 黑苹果完美性

1. iMessage、iCloud、Handoff、continuity 等苹果专属服务都可以正常工作，甚至可以用我的 Apple Watch 解锁这台黑苹果。
2. USB、睡眠、声音、显卡和变频等硬件也都正常工作。

## 黑苹果不完美的地方

暂未发现

## 参考链接：

1. [如何正确的黑苹果](https://catty-house.blogspot.com/2018/10/hackintosh.html)
