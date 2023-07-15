# ROG-Zephyrus-G14-GA401-Hackintosh(2020-2021)

[中文](README.md)/[English](README_en.md)

![1883474518](https://github.com/PIut02/ROG-Zephyrus-G14-GA401IV-Hackintosh/assets/39442130/e32b0e7d-1751-4f90-a6f4-3666a564a4e2)

## 说明

- 本EFI可用版本:BigSur/Monterey/Ventura
- 机型信息已删除，请自行生成更换
- OpenCore版本:0.9.2/0.9.3
- 建议使用[UMAF](https://github.com/DavidS95/Smokeless_UMAF/)工具增大显存，最少1G建议2G，并开启`Above 4G decoding`
- 因NootInc驱动团队禁止分发NootedRed驱动，本EFI已移除该驱动，请前往[NootedRed](https://github.com/NootInc/NootedRed)自行下载添加
- 本EFI以2020款制作，但应该兼容2021款
- 更新EFI可能需要清楚NVRAM才能wan'q
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
| 键盘/触摸板      | IC2 HID               |
| 音频/3.5耳机接口 | ALC289                |
| 内存             | DDR4 3200MHz 16G      |

## 总览

### 正常工作

- CPU

  - 使用[AMDPowerGadget](https://github.com/trulyspinach/SMCAMDProcessor)进行能源管理和温度查看
- IGPU

  - 硬件加速存在部分问题，等待[NootedRed](https://github.com/NootInc/NootedRed)驱动更新解决
  - 使用[RadeonSensor](https://github.com/NootInc/RadeonSensor)查看温度
- WIFI/蓝牙
- Apple ID & iMessages & iCloud
- 中断模式触摸板和键盘
- 1440p 60hz hidpi显示
- 内置扬声器及3.5mm 耳机声音输出
- 所有USB接口
- NVME SSD
- Metal加速
- 亮度、声音快捷键和键盘背光控制
  - 使用[ROG-HID](https://github.com/black-dragon74/ROG-HID)控制，要使用该软件需要关闭SIP
- S3睡眠
  - 使用电源键或笔记本开盖唤醒

### 无法工作&现存问题

- HDMI音频输出
- 内置麦克风及3.5mm 耳机输入
- NVIDIA RTX 2060 MAX-Q
- 第三方浏览器无法正常使用硬件加速(Edge)
- 部分Fn快捷键
- 使用Windows后重启至macos耳机无声，强制关机重启进入macos后正常
- VCN（视频/图片硬件编解码）暂时还有问题，能使用但不确保问题，默认关闭，开启请添加`-nredvcn`至`boot-args`，具体请移至NootedRed页面查看最新进展

### 温度

可以通过关闭`CPS(core performence boost)`将温度控制在比较合适的范围，但是会损失一部分性能。可以通过UMAF工具在BIOS中关闭`CPS`，但是会影响其他系统比如windows的性能，建议是每次开机进系统后通过AMD Power Gadget关闭，至少目前是只能这样。

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
AirportItlwm | 英特尔网卡驱动，注意不同的系统有不同的kext
AMDRyzenCPUPowerManagement | AMD CPU 电源管理
AmdTscSync | CPU频率同步，配合内核补丁控制功耗 
AppleALC | 音频驱动
AppleMCEReporterDisabler | 关闭AppleIntelMCEReporter，避免在AMD CPU的设备上报错
BlueToolFixup | 蓝牙修复补丁，12及以上系统需要 
BrightnessKeys | 亮度调节按键 
ECEnabler | 电池读取
FeatureUnlock | 在不支持的机型解锁功能 
HoRNDIS | 支持安卓设备的USB共享网络 
IntelBTPatcher | 蓝牙驱动 
IntelBluetoothInjector | 蓝牙驱动 
IntelBluetoothFirmware | 蓝牙驱动
Lilu | 必备
NullEthernet | 使无网口设备在MacOS可以登录iCloud
NVMeFix | NVMe硬盘电源管理
RestrictEvents | CPU改名
RadeonSensor | 获取AMD显卡温度信息 
SMCAMDProcessor | AMDRyzenCPUPowerManagement的附属
SMCBatteryManager | 电池管理
SMCLightSensor | 用于笔记本电脑上的环境光传感器 
SMCRadeonGPU.kext | 获取AMD显卡温度信息 
USBToolBox | USB定制
USBMap | USB定制，不通用需要自行定制 
VirtualSMC | 必备
VoodooI2C | 触控板或触屏驱动
VoodooI2CHID | 触控板或触屏驱动

## 致谢

https://github.com/NootInc/NootedRed

https://github.com/NootInc/VoodooI2C

https://github.com/zabdottler/Lenovo-Yoga-16S-hackintosh

https://github.com/AlphaNecron/Zephyrus-G14-GA401QH-EFI

https://github.com/b00t0x/ROG-Zephyrus-G14-GA402-Hackintosh
