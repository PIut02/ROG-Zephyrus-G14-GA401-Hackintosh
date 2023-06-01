# ROG-Zephyrus-G14-GA401IV-Hackintosh(2020)

[中文](README.md)/[English](README_en.md)

![1](https://github.com/PIut02/ROG-Zephyrus-G14-GA401IV-Hackintosh/assets/39442130/86b55723-bf91-4830-8dc3-be19ba0f1666)

## 说明

- 本EFI仅供Big Sur使用，其他版本未经验证
- 机型信息已删除，请自行生成更换
- OpneCore版本：0.9.2
- 建议使用[UMAF](https://github.com/DavidS95/Smokeless_UMAF/)工具增大显存，最少1G建议2G，并开启`Above 4G decoding`
- **这是我第一次使用Hackintosh，欢迎其他使用者检查错误并提供帮助**

## 警告

- 安装或更新系统时注意在`config.plist`中禁用`NootedRed`驱动，否则安装过程中会卡进度条无法正常安装
- 安装或更新系统时请在`config.plist`中禁用`USBMap`驱动或自行定制

## 配置

| 部件             | 型号                  |
| :--------------- | :-------------------- |
| CPU              | AMD Ryzen 7 4800HS    |
| 核显             | AMD Radeon Vega 7     |
| 独立显卡         | NVIDIA RTX 2060 Max-Q |
| 网卡/蓝牙        | Intel AX200           |
| 硬盘             | WD SN570              |
| 键盘             | PS2 controller        |
| 触摸板           | I2C HID               |
| 音频/3.5耳机接口 | ALC289                |
| 内存             | DDR4 3200MHz 16G      |

## 总览

### 正常工作

- CPU

  - 使用[AMD Power Gadget](https://github.com/trulyspinach/SMCAMDProcessor)进行能源管理

- IGPU

  - 硬件加速存在部分问题，等待[NootedRed](https://github.com/NootInc/NootedRed)驱动更新解决

- WIFI/蓝牙

- Apple ID & iMessages & iCloud

- 触摸板和键盘

- 1440p 60hz hidpi显示

- 3.5mm 耳机声音输出

- NVME SSD

- Metal加速

- 亮度、声音快捷键

### 无法工作

- 睡眠

- 内置麦克风及扬声器

- 3.5mm 耳机输入(但蓝牙输入输出可以工作)

- NVIDIA RTX 2060 MAX-Q

- 第三方浏览器无法正常使用硬件加速(Edge)

- 键盘背光控制、Fn快捷键(驱动没有正常工作)

- 使用Windows后，要使声卡在Mac OS中工作必须要强制关机重启进入Mac OS

- VCN（视频/图片硬件编解码）暂时还有问题，能使用但不确保问题，默认关闭，开启请添加-nredvcn至boot-args，具体请移至NootedRed页面查看最新进展

### 温度

可以通过关闭`CPS(core performence boost)`将温度控制在比较合适的范围，但是会损失一部分性能。可以通过UMAF工具在BIOS中关闭`CPS，但是会影响其他系统比如windows的性能，建议是每次开机进系统后通过AMD Power Gadget关闭，至少目前是只能这样。

## 了解你的EFI

### ACPI

SSDT | 作用
:---------|:---------
SSDT-PLUG-ALT | 用于MacOS识别CPU，必须
SSDT-EC | 欺骗MacOS的假EC，必须
SSDT-HPET | 解决IRQ冲突，必须
SSDT-USBX | USB电源管理，必须
SSDT-XOSI | MAC和WIN的ACPI功能，双系统必须
SSDT-ALS0 | NootedRed提供，用于屏幕亮度调整
SSDT-PNLF | NootedRed提供，用于屏幕亮度调整
SSDT-dGPU-Off | 关闭独显 
SSDT-RMNE | 配合NullEthernet.kext内置网卡实现Apple ID登录 

### Kexts

Kext | 作用
:---------|:---------
AMDRyzenCPUPowerManagement | AMD CPU 电源管理
AppleALC | 音频驱动
AppleMCEReporterDisabler | 关闭AppleIntelMCEReporter，避免在AMD CPU的设备上报错
ECEnabler | 电池读取
Lilu | 必备
NVMeFix | NVMe硬盘电源管理
RestrictEvents | CPU改名
SMCAMDProcessor | AMDRyzenCPUPowerManagement的附属
SMCBatteryManager | 电池管理
SMCLightSensor | 用于笔记本电脑上的环境光传感器 
USBToolBox | USB定制
USBMap | USB定制，不通用需要自行定制 
VirtualSMC | 必备
AsusSMC | 键盘支持 
NootedRed | AMD核显驱动
NullEthernet | 使无网口设备在MacOS可以登录iCloud
VoodooI2C | 触控板或触屏驱动
VoodooI2CHID | 触控板或触屏驱动
BrightnessKeys | 亮度调节按键
HoRNDIS | 支持安卓设备的USB共享网络 
AirportItlwm | 英特尔网卡驱动，注意不同的系统有不同的kext
IntelBluetoothFirmware | 蓝牙驱动
IntelBluetoothInjector | 蓝牙驱动 
IntelBTPatcher | 蓝牙驱动 

## 致谢

https://github.com/NootInc/NootedRed

https://github.com/zabdottler/Lenovo-Yoga-16S-hackintosh

https://github.com/AlphaNecron/Zephyrus-G14-GA401QH-EFI

https://github.com/b00t0x/ROG-Zephyrus-G14-GA402-Hackintosh
