# ROG-Zephyrus-G14-GA401-Hackintosh(2020-2021)

This English document is mostly translated by ChatGPT.

![1883474518](https://github.com/PIut02/ROG-Zephyrus-G14-GA401IV-Hackintosh/assets/39442130/e32b0e7d-1751-4f90-a6f4-3666a564a4e2)

## Description

- The available versions for this EFI are BigSur/Monterey/Ventura
- The model information has been deleted, please generate and replace it by yourself
- OpenCore version: 0.9.2/0.9.3
- It is recommended to use [UMAF](https://github.com/DavidS95/Smokeless_UMAF/) tool to increase vram, at least 1G is recommended 2G, and enable `Above 4G decoding`
- Due to the NootInc driver team's prohibition on distributing the NootedRed driver, this EFI has removed that driver. Please go to [NootedRed](https://github.com/NootInc/NootedRed) to download and add it manually
- This EFI was made based on the 2020 model, but it should be compatible with the 2021 model
- **This is my first time using Hackintosh, welcome other users to check for errors and provide help**

## Warning

- When installing or updating the system, pay attention to disable the `NootedRed` driver in `config.plist`, otherwise the installation process will get stuck in the progress bar and cannot be installed normally
- When installing or updating the system, please disable the `USBMap` driver in `config.plist` or customize it yourself

## Configuration

| Component       | Model                  |
| :-------------- | :--------------------- |
| CPU             | AMD Ryzen 7 4800HS     |
| Integrated Graphics| AMD Radeon Vega 7   |
| Graphics Card   | NVIDIA RTX 2060 Max-Q  |
| WiFi/Bluetooth  | Intel AX200            |
| Hard Disk       | WD SN570               |
| Keyboard/Touchpad| IC2 HID               |
| Audio/3.5mm Headphone Jack| ALC289       |
| Memory          | DDR4 3200MHz 16G       |

## Overview

### Working

- CPU
  - Use [AMDPowerGadget](https://github.com/trulyspinach/SMCAMDProcessor) for energy management and temperature viewing
- IGPU
  - Hardware acceleration has some issues, waiting for [NootedRed](https://github.com/NootInc/NootedRed) driver update to solve
  - Use [RadeonSensor](https://github.com/NootInc/RadeonSensor) to view temperature
- WiFi/Bluetooth
- Apple ID & iMessages & iCloud
- Interrupt mode touchpad and keyboard
- 1440p 60hz hidpi display
- Built-in speakers and 3.5mm headphone audio output
- All USB ports
- NVME SSD
- Metal acceleration
- Brightness/volume shortcut keys and Keyboard backlight control
  - To use [ROG-HID](https://github.com/black-dragon74/ROG-HID) control, you need to disable SIP (System Integrity Protection) for this software
- S3 Sleep
  - Wake up using the keyboard or power button

### Not Working&Problem

- HDMI audio output
- Built-in microphone and 3.5mm headphone input
- NVIDIA RTX 2060 MAX-Q
- Third-party browsers cannot use hardware acceleration normally (Edge)
- Fn shortcut keys
- After using Windows, restart to macOS with no sound in headphones, force shutdown and restart into macOS normally.
- VCN (Video/Picture Hardware Encoding and Decoding) still has problems, can be used but not guaranteed, turned off by default, to enable, please add `-nredvcn` to `boot-args`, please move to NootedRed page for the latest progress

### Temperature

The temperature can be controlled within a reasonable range by turning off `CPS (core performance boost)`, but some performance will be lost. You can turn off `CPS` in BIOS using the UMAF tool, but it will affect the performance of other systems such as windows. It is recommended to turn it off using AMD Power Gadget after each boot into the system, at least for now.

## Know Your EFI

### ACPI

SSDT | Function
:---------|:---------
SSDT-PLUG-ALT | Used for MacOS to recognize CPU, must-have
SSDT-EC | Fakes an EC for MacOS, must-have
SSDT-HPET | Solves IRQ conflicts, must-have
SSDT-USBX | USB power management, must-have
SSDT-XOSI | ACPI function of MAC and WIN, dual systems must-have.
SSDT-ALS0 | Provided by NootedRed, used for screen brightness adjustment
SSDT-PNLF | Provided by NootedRed, used for screen brightness adjustment
SSDT-dGPU-Off | Turn off the discrete graphics card     
SSDT-RMNE | Used in combination with the built-in Ethernet card in NullEthernet.kext to implement Apple ID login

### Kexts

Kext | Function
:---------|:---------
AirportItlwm | Intel wireless card driver, note that different systems have different kexts
AMDRyzenCPUPowerManagement | AMD CPU power management
AmdTscSync | CPU frequency synchronization, combined with kernel patch to control power consumption 
AppleALC | Audio driver
AppleMCEReporterDisabler | Turn off AppleIntelMCEReporter to avoid errors on AMD CPU devices
BlueToolFixup | Bluetooth repair patch, required for systems 12 and above 
BrightnessKeys | Brightness adjustment keys 
ECEnabler | Battery reading
FeatureUnlock | Unlock features on unsupported models 
HoRNDIS | Support Android device USB shared network 
IntelBTPatcher | Bluetooth driver 
IntelBluetoothInjector | Bluetooth driver 
IntelBluetoothFirmware | Bluetooth driver
Lilu | Essential
NullEthernet | Allows devices without Ethernet ports to log in to iCloud on MacOS
NVMeFix | NVMe hard drive power management
RestrictEvents | CPU rename
RadeonSensor | Get AMD graphics card temperature information 
SMCAMDProcessor | Subsidiary of AMDRyzenCPUPowerManagement
SMCBatteryManager | Battery management
SMCLightSensor | For ambient light sensors on laptops 
SMCRadeonGPU.kext | Get AMD graphics card temperature information 
USBToolBox | USB customization
USBMap | USB customization, not universal and needs to be customized 
VirtualSMC | Essential
VoodooI2C | Touchpad or touch screen driver
VoodooI2CHID | Touchpad or touch screen driver

## Credit

https://github.com/NootInc/NootedRed

https://github.com/NootInc/VoodooI2C

https://github.com/zabdottler/Lenovo-Yoga-16S-hackintosh

https://github.com/AlphaNecron/Zephyrus-G14-GA401QH-EFI

https://github.com/b00t0x/ROG-Zephyrus-G14-GA402-Hackintosh