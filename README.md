# OpenCore-Supermicro-C7B250-CB-ML

## Introduction

## My Hardware
These are the Hardware component I use. But this OpenCore configuation <strong>should still work</strong> with your MOBO, even if the components are not exactly equal.


| Category  | Component                            |
| --------- | ------------------------------------ |
| CPU       | Intel Core Pentium G4560                 |
| GPU       | Intel UHD Graphics 610 (DISABLED VIA BIOS. HEADLESS CONFIGURED FOR OTHER IGPUS) / RX550 2GB Lexa (patched via DP)|
| SSD       | LiteOn NVME SSD 512GB		   |
| Memory    | 2x 4GB DDR4 2400Mhz                    |


## What's working? :3c

- [X] All USB Ports (my front IO doesnt have USB 3! maybe it can require a remap for them to work)
- [X] Audio with all audio outputs showing up
- [X] iServices
- [X] Graphics Acceleration (need to test VDAEncoder when i change my CPU)
- [X] Intel 1219-V Ethernet
- [X] Dualboot Windows with OpenCore
- [X] CPU and NVME Power Management
- [X] Proper SMBUS patching
- [X] Native NVRAM
- [X] Sleep and wake! (If on pentium G4560, disable IGPU in bios! Check BIOS section for more info)
- [ ] Hibernation (will try to make it work later!)

## BIOS Settings!! ^^

Its really easy to install macOS on this system (i was actually quite surprised on how it didnt complain about anything, really), but, to make it work, we need to tweak some settings.

### <strong>Okay but we have a problem ~~ </strong>silly me forgot what i really changed or not... So i made [this folder](https://github.com/tetenc555/OpenCore-Supermicro-C7B250-CB-ML/tree/main/BIOS) with every setting on my bios. I just want to make some notes:

1. If youre using a supported CPU (i3,i5,i7), please enable Integrated Graphics in Advanced->Graphics Configuration->Internal Graphics. Doing this on a unsupported CPU does not make a difference, besides breaking sleep.

2. Also on Graphics configuration, leave Primary Display on PEG! Set DVMT Pre-Allocated to 64mb too!

3. To disable secure boot and csm, first you need to change all PCIe/PCI/PnP Configuration to UEFI! This is also used for the graphics card on macOS, so it is a must thing to do! Also enable "Above 4GB MMIO BIOS assignment"

4. This bios doesnt let me disable VT-D or CFG-Lock, so keep in mind that we need the quirks related to them on our config.plist (already correctly configured)

## If youre using a supported CPU...

Please do this changes on the config.plist! I will upgrade the config here once i get a compatible one.

1. Download HFSPlus.efi and change the legacy driver on the config
2. Delete the data on Kernel -> Emulate -> Cpuid1Data
3. Delete the data on Kernel -> Emulate -> Cpuid1Mask
4. Disable Kernel -> Emulate -> DummyPowerManagement
5. Disable UEFI -> Quirks -> IgnoreInvalidFlexRatio
6. Enable the damn integrated graphics in the BIOS!!!
