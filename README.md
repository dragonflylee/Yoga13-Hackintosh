# Yoga13 黑苹果驱动包

适配型号 一代 Lenovo Yoga 13IKB

## 感谢

* [Clover EFI](https://sourceforge.net/projects/cloverefiboot/files/Bootable_ISO/) 启动器
* 配置文件基于 [@Rehabman](https://github.com/RehabMan/OS-X-Clover-Laptop-Config)
* [Lilu.kext](https://github.com/acidanthera/Lilu/releases/latest)

## 目前不正常的设备

* 无线网卡 Realtek RTL8723A 802.111n 
* 读卡器 Realtek USB2.0-CRW

## 已驱动的设备

* 英特尔核显 HD4000 `ig-platform-id` 注入 `0x10660004` 驱动 [WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen/releases/latest) 亮度可调节 
* 声卡 Conexant CX20590 注入 Layout `12` 驱动 [AppleALC.kext](https://github.com/acidanthera/AppleALC/releases/latest)
* 触摸板键盘 [VoodooPS2Controller.kext](https://github.com/alexandred/VoodooI2C/releases/latest) 触摸板已配置三指，默认为切换Ctrl+方向键. 
* 电池与CPU监控 [VirtualSMC.kext](https://github.com/alexandred/VirtualSMC/release/latests). 
* USB3.0 驱动 [USBInjectAll.kext](https://bitbucket.org/RehabMan/os-x-usb-inject-all/downloads), DSDT加入 usb_7-series-multiplex 实现USB2.0/3.0自动切换
* 网卡内建 [NullEthernet.kext](https://bitbucket.org/RehabMan/os-x-null-ethernet/downloads) 仿冒PCI网卡
* SSD Patch IOAHCIBlockStorage 开启 Trim
* Lenovo EasyCamera 自带驱动
* Elan触摸屏 自带驱动 只能实现单指触屏
* 睡眠唤醒: DSDT 加入 HPET RTC 修复

## 安装前的 BIOS 设定

* 开启 AHCI: Configuration -> SATA Controller Mode

## FAQ

- Q: AppStore 依旧无法登陆 ?  
  A: 请在 系统信息->网络->位置 检查内建网卡是不是en0
如果不是，请把偏好设置->网络中的所有位置都删掉，再删掉/Library/Preferences/SystemConfiguration/NetworkInterfaces.plist，然后重启。最后把之前的位置在添加进来就好了。
参考 https://bitbucket.org/RehabMan/os-x-null-ethernet
- Q: 内存容量如何修改 ?  
  A: 修改 /EFI/CLOVER/config.plist 中的 SMBIOS -> Memory -> Modules -> Size 中的配置，把 4096 改为 8192 即可改为 8G 内存
