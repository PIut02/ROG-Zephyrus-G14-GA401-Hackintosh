ROG-Zephyrus-G14-GA401-Hackintosh Changelog
==================
#### Sep 15, 2024

- Update opencore to 1.0.1.
- Update many kexts to the latest versions.
- Add custom SMCProcessorAMD.kext to read fan readings, but still seems to have issues.
- Due to issues with 4900hs with CPUTscSync.kext, using ForgedInvariant.kext as a replacement.
- Now using boot-args to control the enablement of the bfixup patch, thanks to [htmambo](https://github.com/htmambo).
- Intel wifi is broken on macOS Sequoia, so will not update to Sequoia for now.
- You no longer need to disable NootedRed.kext when installing and updating macOS.
- Update README.md

#### May 26, 2024

- Update SMCRadeonSensors
- Fix typo in README.md
- Update ACPI patch to make it work only on macOS to avoid interference with Windows

#### May 17, 2024

- Update OpenCore to version 1.0.0.
- Add AMFIPass.kext to replace boot-args.
- Update Applealc, AirportItlwm, SMCRadeonSensors, NootedRed.
- Use Apple's native USB map kexts instead of USBToolbox.
- Fix #39, #22
- Add Changelog.md
- Update README.md

#### Mar 20, 2024

- This update only supports 14.4! 
- Update Opencore to 0.9.9 
- Update kext to support macOS 14.4 
- Add back bfixup because nootedred removed vcn support 
- Update README.md

#### Feb 28, 2024
- Update OpenCore to 0.9.8. 
- Update AppleALC, AirportItlwm, IntelBluetoothFirmware. 
- Switch NootedRed and SMCAMDProcessor to fork repositories, thus removing Bfixup and SMCProcessorAMD. 
- Update README.md

#### Jan 6, 2024

- Update OpenCore to version 0.9.7. 
- Use the beta version of AMDRyzenCPUPowerManagement/SMCAMDProcess for temperature control. 
- Add the boot-args "revpatch=auto" for CPU renaming. 
- Implement BFixup for OpenGL issues. 
- Update AppleALC.kext. 
- Update README.md

#### Nov 20, 2023
- Upgrade OpenCore to version 0.9.6. 
- Following the instructions provided by the esteemed NootedRed author in their enlightening discourse ([ChefKissInc/NootedRed#169 (comment)](https://github.com/ChefKissInc/NootedRed/discussions/169#discussioncomment-6976247)), I have eliminated the usage of SMCAMDProcessor in order to attain superior temperature control and performance. Consequently, it is now permissible to discard AMD Power Gadget and employ alternative tools for monitoring temperature and power consumption. 
- Introduce the inclusion of "revpatch=sbvmm" to ensure proper functionality of system update checks on Sonoma. However, it is important to note that this modification may render the ability to modify CPU nomenclature inoperable.
- Update README.md

#### Oct 12, 2023

- Fix dGPU-OFF.aml.
- After fully disabling the dGPU, it was discovered that the Nvidia USB controller was also being disabled, which fixed the abnormal wake-up issue during sleep. Therefore, the GPRW patch can be removed.
- Update README.md

#### Dec 10, 2023

- Add feature: usb tethering by @dakinianaya
- Updated readme files by @dakinianaya

#### Oct 19, 2023

- Fix Bluetooth.
- Add Sonoma support.

#### Sep 24, 2023

- Upgrade OpenCore version.
- Upgrade Kext.
- Update README.md

#### Sep 2, 2023

- Add 2021 model support.

#### Sep 1, 2023

- Fix Built-in microphone.
- Update README.md

#### Aug 20, 2023

- Upgrade OpenCore version.
- Upgrade Kext.
- Update README.md

#### Jul 15, 2023

- Fix sleep.
- Update kext.
- Update README.md

#### Jul 6, 2023

- Fix speaker.

#### Jun 26, 2023

- Fix gpio touchpad.
- Add gpu-sensor kext.

#### Jun 9, 2023

- Add Ventura support.

#### Jun 7, 2023

- Add Monterey support.

#### Jun 1, 2023

- Initialize the repository and upload the files.
