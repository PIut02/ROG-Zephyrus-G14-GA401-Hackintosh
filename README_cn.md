<p align="center">
 <img width="300px" src="https://github.com/PIut02/ROG-Zephyrus-G14-GA401-Hackintosh/assets/39442130/21806232-1546-4bf5-936c-5a5a34e05c76" align="center" alt="ROG-Zephyrus-G14-GA401-Hackintosh(2020-2021)" />
 <h2 align="center">ROG-Zephyrus-G14-GA401-Hackintosh(2020-2021)</h2>
 <p align="center">OpenCore Config for Asus ROG-Zephyrus-G14-GA401(2020-2021) with AMD Ryzen.</p>
  <p align="center">
    <a href="https://github.com/PIut02/ROG-Zephyrus-G14-GA401-Hackintosh/graphs/contributors">
      <img alt="GitHub Contributors" src="https://img.shields.io/github/contributors/PIut02/ROG-Zephyrus-G14-GA401-Hackintosh" />
    </a>
    <a href="https://github.com/PIut02/ROG-Zephyrus-G14-GA401-Hackintosh/issues">
      <img alt="Issues" src="https://img.shields.io/github/issues/PIut02/ROG-Zephyrus-G14-GA401-Hackintosh?color=0088ff" />
    </a>
    <a href="https://github.com/PIut02/ROG-Zephyrus-G14-GA401-Hackintosh/pulls">
      <img alt="GitHub pull requests" src="https://img.shields.io/github/issues-pr/PIut02/ROG-Zephyrus-G14-GA401-Hackintosh?color=0088ff" />
    </a>
  </p>
  <p align="center">
    <a href="https://github.com/PIut02/ROG-Zephyrus-G14-GA401-Hackintosh">查看Demo</a>
    ·
    <a href="https://github.com/PIut02/ROG-Zephyrus-G14-GA401-Hackintosh/issues">报告Bug</a>
    ·
    <a href="https://github.com/PIut02/ROG-Zephyrus-G14-GA401-Hackintosh/issues">提出新特性</a>
  </p>
  <p align="center">
    <a href="README_cn.md">简体中文</a>
    ·
    <a href="README.md">English</a>
  </p>


![Screenshot](https://github.com/PIut02/ROG-Zephyrus-G14-GA401-Hackintosh/assets/39442130/11d858f8-de53-4e87-a39c-329be14903ad)

## 说明

- 本仓库可用版本: Sonoma
- 机型信息已删除，请自行生成更换
  - 机型必须使用 `MacbookPro16,3`,`iMac20,1`,`iMacPro1,1`.
- OpenCore版本: 0.9.7
- BIOS设置:
  - 建议使用 [UMAF](https://github.com/DavidS95/Smokeless_UMAF/) 工具中增大显存：操作方法为在 Device Manager > AMD CBS > NBIO Common Options > GFX Configuration 中调整 `IGPU Configuration` 为 `UMA_SPECIFIED` ，然后调整 `UMA Frame buffer Size` 最少 1G 建议 2G
  - 通过开启 `Above 4G decoding` 或者在 boot-args 中添加 `ncpi=0x2000` 参数来避免安装卡住
    使用 [UMAF](https://github.com/DavidS95/Smokeless_UMAF/) 工具在 Device Manager > PCI Subsystem Settings 中开启 `Above 4G decoding`
  - 关闭 `Secure Boot` 和 `Fast Boot`
- 本仓库不包含 `NootedRed` 驱动，请前往 [NootedRed](https://github.com/ChefKissInc/NootedRed) 自行下载添加
- 更新EFI可能需要清除 NVRAM 才能完全生效

> [!Warning]
> 安装或更新系统时注意在 `config.plist` 中禁用 `NootedRed` 驱动，否则安装过程中会卡进度条无法正常安装。
>
> `BFixup.kext` 必须加载在 `NootedRed` 之前，也就是加载顺序需调整为 Lilu > BFixup > NootedRed.

## 配置

| 部件             | 型号(2020/2021)           |
| :--------------- | :------------------------ |
| CPU              | AMD Ryzen 7 4800HS/5800HS |
| 核显             | AMD Radeon Vega 8         |
| 独立显卡         | NVIDIA                    |
| 网卡/蓝牙        | Intel AX200               |
| 硬盘             | WD SN570 SSD              |
| 键盘/触摸板      | IC2 HID                   |
| 音频/3.5耳机接口 | ALC289/285                |

## 总览

### 正常工作

- CPU / IGPU
  - 使用 [AMDPowerGadget](https://github.com/trulyspinach/SMCAMDProcessor) 进行CPU能源管理和温度查看
  - 使用 [RadeonSensor](https://github.com/NootInc/RadeonSensor) 查看GPU温度
- WIFI / 蓝牙
- Apple ID / iMessages / iCloud
- 中断模式触摸板和键盘输入
- 1440p 60hz hidpi显示
- 内置扬声器及3.5mm 耳机声音输出 / 内置麦克风
- 所有USB接口 / NVME SSD
- 亮度、声音快捷键和键盘背光控制
  - 使用 [ROG-HID](https://github.com/black-dragon74/ROG-HID) 控制，要使用该软件需要关闭 `SIP`
- S3睡眠
  - 使用 [UMAF](https://github.com/DavidS95/Smokeless_UMAF/) 工具开启 `S3 Sleep`
  - 可能需要在终端中输入：
    ```
    sudo pmset autopoweroff 0
    sudo pmset powernap 0
    sudo pmset standby 0
    sudo pmset proximitywake 0
    sudo pmset tcpkeepalive 0
    ```

### 无法工作&现存问题

- HDMI音频输出 / 3.5mm 耳机输入
- NVIDIA 显卡
- 部分Fn快捷键
- 使用 Windows 后重启至 macOS 耳机无声，强制关机重启进入 macOS 后正常.
- VCN(视频/图片硬件编解码)暂时还有问题，能使用但不确保问题，默认关闭，开启请添加 `-ChefKissInternal` 至 `boot-args` ，具体请移至 NootedRed 页面查看最新进展.

### 提示

- 可以通过关闭`CPS(core performence boost)`将温度控制在比较合适的范围，但是会损失一部分性能。可以通过 UMAF 工具在 BIOS 中关闭 `CPS` ，但是会影响其他系统比如 Windows 的性能，建议是每次开机进系统后通过 AMDPowerGadget 关闭，至少目前是只能这样。
- `BFixup.kext` 通过降级了 OpenGL 版本来避免让系统冻结，一些应用因此得以正常工作，例如 Chrome ，但同时也会使得部分应用无法工作，如果你遇到问题禁用 `BFixup.kext`.

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
SSDT-NoHybGfx | 关闭独显
SSDT-RMNE | 配合NullEthernet.kext内置网卡实现Apple ID登录

### Kexts

Kext | 作用
:---------|:---------
AirportItlwm | 英特尔网卡驱动，注意不同的系统有不同的kext
AMDRyzenCPUPowerManagement | AMD CPU 电源管理
AppleALC | 音频驱动
AppleMCEReporterDisabler | 关闭AppleIntelMCEReporter，避免在AMD CPU的设备上报错
BFixup | 降级OpenGL版本 
BlueToolFixup | 蓝牙修复补丁 
BrightnessKeys | 亮度调节按键
CPUTscSync | 同步CPU的TSC(Time Stamp Counter)来避免一些问题
ECEnabler | 电池读取
FeatureUnlock | 在不支持的机型解锁功能
HoRNDIS | 支持安卓设备的USB共享网络
IntelBTPatcher | 蓝牙驱动
IntelBluetoothFirmware | 蓝牙驱动
Lilu | 必备
NullEthernet | 使无网口设备在MacOS可以登录iCloud
NVMeFix | NVMe硬盘电源管理
RestrictEvents | 用于阻止导致不同硬件兼容性问题的不需要的进程，并解锁对仅限于其他硬件的某些功能的支持
RadeonSensor | 获取AMD显卡温度信息
SMCAMDProcessor | AMDRyzenCPUPowerManagement的附属
SMCProcessorAMD | 使系统能读取CPU的温度和功耗
SMCBatteryManager | 电池管理
SMCLightSensor | 用于笔记本电脑上的环境光传感器
SMCRadeonGPU.kext | 获取AMD显卡温度信息
USBToolBox | USB定制
USBMap | USB定制
VirtualSMC | 必备
VoodooI2C | 触控板或触屏驱动
VoodooI2CHID | 触控板或触屏驱动

## 致谢

- [Apple](https://www.apple.com) 设计的 macOS 操作系统.
- [ChefKissInc](https://github.com/ChefKissInc/) 编写的 [NootedRed](https://github.com/ChefKissInc/NootedRed) 和 VoodooI2C ，他们的辛勤工作让这个项目成为可能.
- [zabdottler](https://github.com/zabdottler/Lenovo-Yoga-16S-hackintosh), [AlphaNecron](https://github.com/AlphaNecron/Zephyrus-G14-GA401QH-EFI), [b00t0x](https://github.com/b00t0x/ROG-Zephyrus-G14-GA402-Hackintosh) 让我知道这个项目有可能实现.
- [DavidS95](https://github.com/DavidS95/) 编写的 [UMAF](https://github.com/DavidS95/Smokeless_UMAF/)，让我能方便的修改隐藏的BIOS设置.