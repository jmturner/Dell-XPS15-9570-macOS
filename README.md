# 介绍
该EFI可以使`Dell XPS 9570 4K`在Mojave环境下正常工作，大部分内容是基于[Xigtun](https://github.com/Xigtun/xps-9570-mojave),[bavariancake](https://github.com/bavariancake/XPS9570-macOS)两位朋友的EFI综合改进得到。其中两位同仁向我们提供了非常关键的修复：
* @0xFireWolf 提供了DPCH、[HDMI](https://www.tonymacx86.com/threads/fix-coffee-lake-intel-uhd-graphics-630-on-macos-mojave-hdmi-output-issue-public-testing-stage.275126/)的修复补丁，使XPS 9570的正常睡眠与HDMI原生输出有了可能！
* @807133286 提供了[触控板驱动方案](https://github.com/Xigtun/xps-9570-mojave/issues/23)，是XPS 9570拥有将近白苹果触控板的体验！

在这里，我要对@0xFireWolf、@bavariancake、@Xigtun、@807133286的无私帮助和奉献表示感谢。还有在[XPS 9570 Hackintosh Guide](https://www.tonymacx86.com/threads/wip-guide-xps-9570-hackintosh-guide.259844/)中，很多兄弟提交他们所遇问题，分享各种解决方案，让我领悟到许多Hackintosh的配置方式，这个EFI是以上所有朋友铸就的！再次谢谢他们！
我总结了Xigtun和bavariancake的配置优缺点,内容如下：
## Xigtun 
 ### 优点
 * 解锁触控板的大部分高级手势
 * 支持触控屏幕
 * 亮度正常
 * 支持typec 转换成HDMI\DP输出
 ### 缺点
 * 睡眠唤醒黑屏
 * 无法驱动原生声卡
 * config过于冗余
 
## bavariancake
 ### 优点
 * 支持睡眠

 ### 缺点
 * 触控板不支持高级手势
 * 不支持屏幕触控
 * DSDT加载方法存在错误
 
## 我的改进
当然，以上配置已经可以让XPS 9570的几个版本正常使用，但离真正的fawlessly还是有差距。我致力于融合以上两位的工作成果，得到一个完善的配置。在`Mojave 10.14.3`版本下,我的配置解决了以下问题:

 * 支持Type-C外接显示器输出
 * 支持HDMI口外接显示器输出
 * 支持睡眠与唤醒
 * 支持原生声卡驱动
 * 支持触控板手势与屏幕触控
 * 更少的DSDT加载错误
 * 利用CpuFriend注入Macbook pro 15.1的变频信息
 

# 硬件配置
 ## 已驱动
  * Machine :Dell XPS 9570
  * CPU: Intel i7-8750H
  * GPU: UHD630 + 1050Ti
  * RAM: 16GB RAM
  * Display: 4K Sharp
  * SSD: PC401 NVMe SK hynix 512GB SSD
  * Audio: Realtek ALC298
  * Touchscreen
  * WLAN + Bluetooth : DW1830（已更换）
 ## 未驱动
  * Killer 1535 (无解)
  * Goodix fingerpint reader (无解)
  * Nvida Geforce 1050Ti (无解，已屏蔽)

# 软件环境
 * BIOS: 1.7.0,1.5.0
 * Mojave 10.14.3 + Windows 10 1809系统
 * macOS: 10.14.2, 10.14.3

# 使用方法
 * 将CLOVER放入EFI分区，使用config_install.plist进系统完成安装
 * 进入桌面后运行`sudo kextcache -i /`重建缓存
 * 用config.plist使能集显加速
 * 加入自生成的三码
 
 `config_10.14.4.plist`是我为了想升级10.14.4版本的朋友准备的，因为精力有限我还未能进行测试，期待有人反馈结果。

# 已知问题
 * 睡眠唤醒后，蓝牙随机出现不可用。
 * -v 模式无法进入系统
 
# 待测试
 * 雷电三接口
 * 非4k、8750H的机型
 * 在10.14.4上运行
 
# 关于本机
![关于本机](https://github.com/LuletterSoul/Dell-XPS-15-9570-macOS-Mojave/blob/master/screenshots/2048_mem.png)
![Nvme固态硬盘](https://github.com/LuletterSoul/Dell-XPS-15-9570-macOS-Mojave/raw/master/screenshots/NVME.png)
![集显](https://github.com/LuletterSoul/Dell-XPS-15-9570-macOS-Mojave/raw/master/screenshots/Graphic.png)
![双显示器输出](https://github.com/LuletterSoul/Dell-XPS-15-9570-macOS-Mojave/raw/master/screenshots/dual_displays.png)
![输出细节](https://github.com/LuletterSoul/Dell-XPS-15-9570-macOS-Mojave/raw/master/screenshots/dual_displays_details.png)
![USB3.1](https://github.com/LuletterSoul/Dell-XPS-15-9570-macOS-Mojave/raw/master/screenshots/USB3.1.png)
![电池](https://github.com/LuletterSoul/Dell-XPS-15-9570-macOS-Mojave/raw/master/screenshots/Battery.png)
![DW1830蓝牙](https://github.com/LuletterSoul/Dell-XPS-15-9570-macOS-Mojave/raw/master/screenshots/DW1830%20Bluetooth.png)
![DW1830 Wifi](https://github.com/LuletterSoul/Dell-XPS-15-9570-macOS-Mojave/raw/master/screenshots/DW1830%20Wifi.png)
![原生管理](https://github.com/LuletterSoul/Dell-XPS-15-9570-macOS-Mojave/raw/master/screenshots/Extention.png)
![变频](https://github.com/LuletterSoul/Dell-XPS-15-9570-macOS-Mojave/raw/master/screenshots/Intel%20Turbo%20Boost.png)
# 更新历史
## 修复HDMI输出
XPS 9570的HDMI输出问题终于有了进展：依旧是来自@0xFireWolf的出色工作：[Coffee Lake Intel UHD Graphics 630 on macOS Mojave: HDMI Output Issue ](https://www.tonymacx86.com/threads/fix-coffee-lake-intel-uhd-graphics-630-on-macos-mojave-hdmi-output-issue-public-testing-stage.275126/)。（大佬也曾针对CoffeLake UHD 630 Graphic造成的panic问题提出了解决方案，真是太强了）！解决方式如下：

1.使用FireWolf发布的WhateverGreen。

2.在Devices/Properties中添加如下entry:
 * `framebuffer-con1-enable 01000000`
 * `framebuffer-con1-alldata 01050900 00040000 87010000`
 * `framebuffer-con2-enable 01000000`
 * `framebuffer-con2-alldata 03040A00 00080000 87010000`

本机上双屏输出成功的样例：
 * `2K 60Hz display<--->HDMI 2.0 cable<---->HDMI 2.0 port(支持HDMI Audio)`
 * `4k 60Hz display<--->Type C to DP cable<---->Type C port`
 
单屏幕输出成功的样例：
 * `4k 60Hz display<--->HDMI 2.0 cable<---->HDMI 2.0 port`
## 禁用board id侦测
此前，使用macbook pro 15的board-id存在问题(因为Mac OS的主板侦测)，通过修改board-id为iMac,14,可以驱动Type-C接口。但是，经测试该方法有一定几率使电池图标在重启后消失，也可能使DA300 Hub失效。现使用原生的Mbp,15的board-id,同时使用WhateverGreen 中的启动参数agdpmod=vit9696禁用其侦测。
## 更新Voodool2CHID v2.1.5
  可能修复了一些bug。
## 将显存修改为2048MB
  通过WhateverGreen修改显存为2048M,可能会解决一些机型的花屏问题。
# 声明
我尝试直接升级10.14.4，失败了。因此我选择我停留在10.14.3（18D42）,在这个版本上机器工作得很好，希望有意愿的朋友可以尝试升级到10.14.3更高版本进行测试，期待更多的朋友可以加入进来，让XPS 9570 实现真正的Hackintosh!

如果你需要发布此EFI或转载给他人，请务必注明我的仓库出处，以及[Xigtun](https://github.com/Xigtun/xps-9570-mojave),[bavariancake](https://github.com/bavariancake/XPS9570-macOS)的仓库地址，请勿用于商业行为！尊重开源与劳动！您的合作与支持是我们持续维护和分享的动力。
