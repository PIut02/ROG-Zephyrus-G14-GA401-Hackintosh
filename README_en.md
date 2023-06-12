# ROG-Zephyrus-G14-GA401-Hackintosh(2020-2021)

This English document is mostly translated by ChatGPT.

![1](https://github.com/PIut02/ROG-Zephyrus-G14-GA401IV-Hackintosh/assets/39442130/86b55723-bf91-4830-8dc3-be19ba0f1666)
![1883474518](https://github.com/PIut02/ROG-Zephyrus-G14-GA401IV-Hackintosh/assets/39442130/3023017c-44af-4d54-bba8-355271968e3a)

## Description

- The available versions for this EFI are BigSur/Monterey/Ventura
- The model information has been deleted, please generate and replace it by yourself
- OpenCore version: 0.9.2
- It is recommended to use [UMAF](https://github.com/DavidS95/Smokeless_UMAF/) tool to increase vram, at least 1G is recommended 2G, and enable `Above 4G decoding`
- Due to the NootInc driver team's prohibition on distributing the NootedRed driver, this EFI has removed that driver. Please go to [NootedRed](https://github.com/NootInc/NootedRed) to download and add it manually
- This EFI was made based on the 2020 model, but it should be compatible with the 2021 model
- **This is my first time using Hackintosh, welcome other users to check for errors and provide help**

## Warning

- When installing or updating the system, pay attention to disable the `NootedRed` driver in `config.plist`, otherwise the installation process will get stuck in the progress bar and cannot be installed normally
- When installing or updating the system, please disable the `USBMap` driver in `config.plist` or customize it yourself

## Configuration

| Component                  | Model                 |
| :------------------------- | :-------------------- |
| CPU                        | AMD Ryzen 7 4800HS    |
| Integrated Graphics        | AMD Radeon Vega 7     |
| Graphics Card              | NVIDIA RTX 2060 Max-Q |
| WiFi/Bluetooth             | Intel AX200           |
| Hard Disk                  | WD SN570              |
| Keyboard                   | PS2 controller        |
| Touchpad                   | I2C HID               |
| Audio/3.5mm Headphone Jack | ALC289                |
| Memory                     | DDR4 3200MHz 16G      |

## Overview

### Working

- CPU

  - Energy management is done using [AMD Power Gadget](https://github.com/trulyspinach/SMCAMDProcessor)

- IGPU

  - Hardware acceleration has some issues, waiting for updated driver from [NootedRed](https://github.com/NootInc/NootedRed)

- WiFi/Bluetooth

- Apple ID & iMessages & iCloud

- Touchpad and keyboard

- 1440p 60hz hidpi display

- 3.5mm headphone audio output

- NVME SSD

- Metal acceleration

- Brightness and volume shortcut keys

### Not Working

- Sleep(Only in BigSur)

- Unable to log in to Apple Store/Apple Music account on Mac

- Internal microphone and speakers

- 3.5mm headphone input (but Bluetooth input/output works)

- NVIDIA RTX 2060 MAX-Q

- Third-party browsers cannot use hardware acceleration normally (Edge)

- Keyboard backlight control, Fn shortcut keys (the driver did not work properly)

- If you use Windows first, you must force shutdown and restart to enter Mac OS to make the sound card work in Mac OS.

- VCN (Video/Picture Hardware Encoding and Decoding) still has problems, can be used but not guaranteed, turned off by default, to enable, please add `-nredvcn` to `boot-args`, please move to NootedRed page for the latest progress

### Temperature

By turning off `CPS(core performance boost)`, the temperature can be controlled within a reasonable range, but some performance will be lost. You can turn off `CPS` in BIOS using the UMAF tool, but it will affect the performance of other systems such as windows. It is recommended to turn it off using AMD Power Gadget after each boot into the system, at least for now.

## Know Your EFI

### ACPI

| SSDT          | Function                                                     |
| :------------ | :----------------------------------------------------------- |
| SSDT-PLUG-ALT | Used for MacOS to recognize CPU, must-have                   |
| SSDT-EC       | Fakes a EC for MacOS, must-have                              |
| SSDT-HPET     | Solves IRQ conflicts, must-have                              |
| SSDT-USBX     | USB power management, must-have                              |
| SSDT-XOSI     | ACPI function of MAC and WIN, dual systems must-have.        |
| SSDT-ALS0     | Provided by NootedRed, used for screen brightness adjustment |
| SSDT-PNLF     | Provided by NootedRed, used for screen brightness adjustment |
| SSDT-dGPU-Off | Turn off the discrete graphics card                          |
| SSDT-RMNE     | Used in combination with the built-in Ethernet card in NullEthernet.kext to implement Apple ID login |

### Kexts

| Kext                       | Function                                                     |
| :------------------------- | :----------------------------------------------------------- |
| AMDRyzenCPUPowerManagement | AMD CPU power management                                     |
| AppleALC                   | Audio driver                                                 |
| AppleMCEReporterDisabler   | Disables AppleIntelMCEReporter to avoid errors on AMD CPU devices |
| ECEnabler                  | Battery readings                                             |
| Lilu                       | Must-have                                                    |
| NVMeFix                    | NVMe hard disk power management                              |
| RestrictEvents             | CPU renamer                                                  |
| SMCAMDProcessor            | Subsidiary of AMDRyzenCPUPowerManagement                     |
| SMCBatteryManager          | Battery management                                           |
| SMCLightSensor             | Used for ambient light sensors on laptops                    |
| USBToolBox                 | USB customization                                            |
| USBMap                     | USB customization, not universal, need to customize by yourself |
| VirtualSMC                 | Must-have                                                    |
| NootedRed                  | AMD Integrated Graphics driver                               |
| NullEthernet               | Enables devices without network ports to log in to iCloud on MacOS |
| VoodooI2C                  | Touchpad or touchscreen driver                               |
| VoodooI2CHID               | Touchpad or touchscreen driver                               |
| BrightnessKeys             | Brightness adjustment keys                                   |
| HoRNDIS                    | Supports USB sharing networks for Android devices            |
| AirportItlwm               | Intel network card driver, note that different systems have different kexts |
| IntelBluetoothFirmware     | Bluetooth driver                                             |
| IntelBluetoothInjector     | Bluetooth driver                                             |
| IntelBTPatcher             | Bluetooth driver                                             |
| AmdTscSync                 | CPU frequency synchronization, in conjunction with kernel patches, to control power consumption |

## Credit

https://github.com/NootInc/NootedRed

https://github.com/zabdottler/Lenovo-Yoga-16S-hackintosh

https://github.com/AlphaNecron/Zephyrus-G14-GA401QH-EFI

https://github.com/b00t0x/ROG-Zephyrus-G14-GA402-Hackintosh
