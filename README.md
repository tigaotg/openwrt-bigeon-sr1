# OpenWrt support for 智选品珈 SR1

OpenWrt 24.10.5 device support for the Bigeon / 智选品珈 SR1 router.

## Latest firmware

Latest stable release:

**Bigeon SR1 OpenWrt 24.10.5 — first public release based on hardware-verified support**

[Download from GitHub Releases](https://github.com/tigaotg/openwrt-bigeon-sr1/releases/latest)

Current release:

`v24.10.5-sr1-r1`

Available images:

- `openwrt-ramips-mt76x8-bigeon_sr1-initramfs-kernel.bin`
- `openwrt-ramips-mt76x8-bigeon_sr1-squashfs-sysupgrade.bin`

For first-time flashing, it is recommended to boot `initramfs-kernel.bin` from RAM via Breed first, verify the hardware, and only then flash `squashfs-sysupgrade.bin`.

---

## Hardware

- SoC: MediaTek MT7628AN
- 5 GHz Wi-Fi: MediaTek MT7612EN
- RAM: 128 MB DDR2
- Flash: 16 MB SPI NOR
- Bootloader: Breed 1.1
- Ethernet: 5 x 100 Mbps

## Flash layout

| Partition | Offset | Size |
|---|---:|---:|
| u-boot | `0x000000` | `0x30000` |
| hw_panic | `0x030000` | `0x10000` |
| factory | `0x040000` | `0x10000` |
| firmware | `0x050000` | `0xfb0000` |

The firmware partition size is approximately 16064 KiB.

## Factory data

The following Factory data locations were verified on real hardware:

- 2.4 GHz EEPROM: `factory + 0x0000`
- 5 GHz EEPROM: `factory + 0x8000`
- Ethernet MAC: `factory + 0x28`

Do not overwrite Factory / EEPROM data with data from another device.

## Verified hardware

The Bigeon SR1 OpenWrt port has been tested on real hardware.

Verified functions include:

- OpenWrt 24.10.5 boots successfully
- OpenWrt boots successfully after being written to flash
- 5 Ethernet ports work correctly
- Ethernet port order is correct
- 2.4 GHz Wi-Fi works
- 5 GHz Wi-Fi works
- 5 GHz 80 MHz operation works
- 5 GHz 2x2 MIMO works
- DHCP works
- LuCI works
- SSH works
- Ethernet MAC is read correctly from the Factory partition
- 2.4 GHz EEPROM data is read correctly
- 5 GHz EEPROM data is read correctly
- SYS LED works on GPIO 11
- Reset button works on GPIO 38
- Persistent JFFS2 overlay works after reboot
- Wireless settings remain persistent after reboot

## Firmware usage

### initramfs-kernel.bin

File:

`openwrt-ramips-mt76x8-bigeon_sr1-initramfs-kernel.bin`

This image is intended for temporary RAM booting through Breed.

It is recommended for first-time testing because it allows the hardware configuration to be verified before writing OpenWrt to flash.

Recommended checks include:

- Ethernet ports
- LuCI
- 2.4 GHz Wi-Fi
- 5 GHz Wi-Fi
- DHCP
- MAC address
- SYS LED
- Reset button

### squashfs-sysupgrade.bin

File:

`openwrt-ramips-mt76x8-bigeon_sr1-squashfs-sysupgrade.bin`

This image is intended for permanent OpenWrt installation.

It is recommended to test the `initramfs-kernel.bin` image first before flashing this image.

## SHA256

### initramfs-kernel.bin

```text
786c0c0f800e69aa8ed35d303c9c4534b4dabcb782d5f2ffe8cd43a607e52fa6
```

### squashfs-sysupgrade.bin

```text
290b2bc9bcc5519db4d27e0697357f91ded88a821c454558e4eda1293eaac625
```

## Files

- `dts/mt7628an_bigeon_sr1.dts` — device tree
- `patches/0001-bigeon-sr1-openwrt-24.10.5.patch` — OpenWrt device support changes
- `patches/0002-luci-add-bigeon-sr1-attribution.patch` — LuCI Bootstrap attribution patch

## Target

Tested with:

- OpenWrt 24.10.5
- Revision: `r29087-d9c5716d1d`
- Linux: `6.6.119`
- Target: `ramips/mt76x8`
- Board: `bigeon,sr1`

## LuCI attribution

The LuCI Bootstrap attribution patch adds the following footer text:

`Bigeon SR1 OpenWrt 适配：微茫世间 · GitHub`

The GitHub link points to:

[https://github.com/tigaotg/openwrt-bigeon-sr1](https://github.com/tigaotg/openwrt-bigeon-sr1)

The corresponding patch is:

`patches/0002-luci-add-bigeon-sr1-attribution.patch`

## Flashing warning

Do not flash firmware from this project unless you have confirmed that your device hardware matches the Bigeon / 智选品珈 SR1 described here.

Before flashing, it is strongly recommended to keep backups of:

- Full SPI flash
- Factory / EEPROM partition
- Original firmware
- Breed recovery environment

Factory / EEPROM data may contain device-specific information such as Wi-Fi calibration data and MAC addresses.

**Do not overwrite your device's Factory / EEPROM partition with data from another router.**

Incorrectly modifying the bootloader, flash partitions, Factory data, or EEPROM data may cause boot failure, wireless problems, or loss of MAC addresses.

## Recommended flashing procedure

For first-time installation:

1. Boot `initramfs-kernel.bin` from RAM through Breed.
2. Verify Ethernet, LuCI, Wi-Fi, MAC address, SYS LED, and Reset button.
3. Confirm that the hardware matches this project.
4. Flash `squashfs-sysupgrade.bin`.
5. Reboot and verify persistent operation.

## Project status

The Bigeon SR1 OpenWrt port has been tested on real hardware.

The current public release is based on the hardware-verified port and includes the LuCI Bootstrap attribution patch.

The current Release firmware was rebuilt after adding the LuCI attribution patch. The underlying device port and hardware configuration had already been verified on real Bigeon SR1 hardware.

## Author

Bigeon SR1 OpenWrt adaptation:

**微茫世间**

GitHub:

[https://github.com/tigaotg/openwrt-bigeon-sr1](https://github.com/tigaotg/openwrt-bigeon-sr1)
