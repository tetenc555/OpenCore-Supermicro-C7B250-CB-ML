# OpenCore-Supermicro-C7B250-CB-ML

## My Hardware
These are the Hardware component I use. But this OpenCore configuation <strong>should still work</strong> with your MOBO, even if the components are not exactly equal.


| Category  | Component                            |
| --------- | ------------------------------------ |
| CPU       | Intel Core i5 7500             |
| GPU       | Intel UHD Graphics 630 / RX550 2GB Lexa (patched via DP)|
| SSD       | LiteOn NVME SSD 512GB		   |
| Memory    | 2x 4GB DDR4 2400Mhz                    |

## Tahoe Disclamier
Maybe it works with the iGPU? I dont know as mine is headless and i will just wait for a patch for Polaris GPUs. If youre using only the integrated graphics, it should work. USBMap was updated to support Tahoe and FileVault should be functional.


## What's working? :3c

Tested on Sequoia 15.5 !! ||3

- [X] All USB Ports (my front IO doesnt have USB 3! maybe it can require a remap for them to work)
- [X] Audio with all audio outputs showing up
- [X] iServices
- [X] Graphics Acceleration
- [X] IGPU Hardware Acceleration
- [X] Intel 1219-V Ethernet
- [X] Dualboot Windows with OpenCore
- [X] CPU and NVME Power Management
- [X] Proper SMBUS patching
- [X] Native NVRAM
- [X] Sleep and wake!
- [ ] Hibernation (will try to make it work later!)
- [ ] Boot-Chime on Opencore Picker (tried to set it up but it doesnt work yet)

## BIOS Settings!! ^^

Its really easy to install macOS on this system (i was actually quite surprised on how it didnt complain about anything, really), but, to make it work, we need to tweak some settings.

### <strong>Okay but we have a problem ~~ </strong>silly me forgot what i really changed or not... So i made [this folder](https://github.com/tetenc555/OpenCore-Supermicro-C7B250-CB-ML/tree/main/BIOS) with every setting on my bios. I just want to make some notes:

1. If youre using a supported CPU (i3,i5,i7), please enable Integrated Graphics in Advanced->Graphics Configuration->Internal Graphics. Doing this on a unsupported CPU does not make a difference, besides breaking sleep.

2. Also on Graphics configuration, leave Primary Display on PEG! Set DVMT Pre-Allocated to 64mb too!

3. To disable secure boot and csm, first you need to change all PCIe/PCI/PnP Configuration to UEFI! This is also used for the graphics card on macOS, so it is a must thing to do! Also enable "Above 4GB MMIO BIOS assignment"

4. This bios doesnt let me disable VT-D or CFG-Lock, so keep in mind that we need the quirks related to them on our config.plist (already correctly configured)
