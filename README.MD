# Dell Precision 7820 - OpenCore - Ventura

![OpenCore Version - 0.9.7](https://img.shields.io/badge/OpenCore-0.9.7-30bcd5)
![SMBIOS - MacPro7,1](https://img.shields.io/badge/SMBIOS-MacPro7,1-e0e1e3)
![macOS Version - Ventura 13.6.3](https://img.shields.io/badge/macOS-Ventura_13.6.3-ed690c)
![Updated on - 23 January 2024](https://img.shields.io/badge/Updated_on-23/01/2024-228B22)

****

EFI dir with OpenCore v0.9.7 (`REL-097-2023-12-11`)

This setup has been in daily use (coding etc.) since Nov 2023 and has worked well. I haven't experienced any major issues thus far.

- Sleep works (If you happen to experience issues with sleep, please turn off the Bluetooth and try again)
- WiFi + Bluetooth works (`Intel AX211` I believe)
- FaceTime + iMessage works (*please update the MLB, Serial Number etc. following OC [instructions here](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html). SN & MLB found in the config.plist in this repo are only placeholders (though they are valid and should let you boot), so you MUST change them to avoid issues with iCloud/FaceTime/iMessage*).

**Drivers**
- [**HfsPlus**](https://github.com/acidanthera/OcBinaryData/blob/master/Drivers/HfsPlus.efi)
- [**OpenCanopy**](https://github.com/acidanthera/OpenCorePkg)
- [**OpenRuntime**](https://github.com/acidanthera/OpenCorePkg)


**SSDTs**
- [**SSDT-EC-USBX-DESKTOP**](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-EC-USBX-DESKTOP.aml)
- [**SSDT-PLUG-DRTNIA**](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-PLUG-DRTNIA.aml)
- **SSDT-RTC0** - I actually cannot remember where I got it from. Official Dortania equivalent might be the [SSDT-RTC0-RANGE-HEDT](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-RTC0-RANGE-HEDT.aml).

**Kexts**
- [**AirportItlwm**](https://github.com/OpenIntelWireless/itlwm) - `v2.2.0` - WiFi AX211
- [**AppleALC**](https://github.com/acidanthera/AppleALC) - `v1.8.8` - Sound
- [**BlueToolFixup**](https://github.com/acidanthera/BrcmPatchRAM) - `v2.6.8` - Bluetooth
- [**IntelBluetoothFirmware**](https://github.com/OpenIntelWireless/IntelBluetoothFirmware) - `v2.3.0` - Bluetooth
- [**IntelBTPatcher**](https://github.com/OpenIntelWireless/IntelBluetoothFirmware) - `v2.3.0` - Bluetooth
- [**IntelMausi**](https://github.com/acidanthera/IntelMausi) - `v1.0.7` - NIC
- [**Lilu**](https://github.com/acidanthera/Lilu) - `v1.6.7`
- [**NVMeFix**](https://github.com/acidanthera/NVMeFix) - `v1.1.1` - SSD power management (may not be needed, I left it as it isn't causing any issues)
- [**RadeonSensors**](https://github.com/ChefKissInc/RadeonSensor) - `v0.3.3` - GPU sensors
- [**RestrictEvents**](https://github.com/acidanthera/RestrictEvents) - `v1.1.3` - Fixes RAM warnings
- [**SMCDellSensors**](https://github.com/acidanthera/VirtualSMC) - `v1.3.2` - Allows iStatMenus to see some of the Dell sensors
- [**SMCProcessor** ](https://github.com/acidanthera/VirtualSMC)- `v1.3.2`
- [**SMCRadeonGPU**](https://github.com/ChefKissInc/RadeonSensor) - `v0.3.3` - GPU sensors
- [**SMCSuperIO**](https://github.com/acidanthera/VirtualSMC) - `v1.3.2`
- [**USBMap**](https://github.com/corpnewt/USBMap) - `v1.0` - self-explanatory really, USB map is required since Big Sur 11.3
- [**VirtualSMC**](https://github.com/acidanthera/VirtualSMC) - `v1.3.2`
- [**WhateverGreen**](https://github.com/acidanthera/WhateverGreen) - `v1.6.6` - GPU patches; pretty much essential to enable the proper GPU support without unnecessary faff. You can try applying the [PowerPlay table patches](https://github.com/5T33Z0/OC-Little-Translated/blob/main/11_Graphics/GPU/AMD_Radeon_Tweaks/Polaris_PowerPlay_Tables.md) and remove this kext, but while I did notice a drop in GPU power usage (below 100W) and temps, my secondary display developed a flickering issue and occasional black screen. I decided to live with higher GPU power usage (around 130W most of the time) rather than fight with flickering screens and/or incorrect refresh rates. Your mileage may vary.

****

If you are using a non-Intel WiFi adapter (*chipsets supported by itlwm can be found here: https://openintelwireless.github.io/itlwm/Compat.html*), please remove `AirportItlwm`, `IntelBluetoothFirmware` and `IntelBTPatcher` kexts + update the `config.plist` via the OC config tool of your choice.

[PropertyTree](https://github.com/corpnewt/ProperTree) is what I usually use - remove the unnecessary kexts, open `config.plist` via `File -> Open OR CMD+O`, then `File -> OC Clean Snapshot OR CMD+SHIFT+R`, in newly opened file browser/Finder window, find your `EFI/OC` folder, select/click `OC` and press `Choose`. That should update the `config.plist` and reflect your kext/SSDTs/drivers changes. Then `File -> Save` and reboot.

****

**My specs**
- **CPU**: `Intel Gold 6132`
- **RAM**: `96GB 2400 MHz`
- **GPU**: `SAPPHIRE Nitro+ RX 580 8GB`
- **SSD**: `SABRENT ROCKET NVMe4 1TB`
- **NVME ADAPTER**: `SABRENT M.2 SSD NVMe to PCIe Adapter (Amazon)`
- **DISPLAYS**: `1x LG 27GP95R 4K + 1x Dell P2721Q 4K`
- **WIFI/BLUETOOTH**: `Ubit AX211 PCI-E Adapter (Amazon)`

****

**Thanks to:**
- https://github.com/mach-kernel/Dell7820-macOS - for sharing his version of OC for Catalina. It helped a lot with setting up Ventura.
- https://github.com/acidanthera & https://github.com/dortania - for OpenCore and a bunch of essential kexts and guides.
- https://github.com/zxystd & [OpenIntelWireless Team](https://github.com/OpenIntelWireless) - for making WiFi on hackintosh easy.
- https://github.com/ChefKissInc - for the RadeonSensors.
- https://github.com/corpnewt - for USB Map tool.
