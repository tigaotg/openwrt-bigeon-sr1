# OpenWrt support for Bigeon SR1

OpenWrt 24.10.5 device support for the Bigeon / 智选品珈 SR1 router.

## Hardware

- SoC: MediaTek MT7628AN
- 5 GHz Wi-Fi: MediaTek MT7612EN
- RAM: 128 MB DDR2
- Flash: 16 MB SPI NOR
- Bootloader: Breed
- Ethernet: 5 x 100 Mbps

## Flash layout

| Partition | Offset | Size |
|---|---:|---:|
| u-boot | 0x000000 | 0x30000 |
| hw_panic | 0x030000 | 0x10000 |
| factory | 0x040000 | 0x10000 |
| firmware | 0x050000 | 0xfb0000 |

## Factory data

- 2.4 GHz EEPROM: `factory + 0x0000`
- 5 GHz EEPROM: `factory + 0x8000`
- Ethernet MAC: `factory + 0x28`

## Verified hardware

The following functions were tested on real hardware:

- OpenWrt 24.10.5 boots successfully from flash
- 5 Ethernet ports work and port order is correct
- 2.4 GHz Wi-Fi works
- 5 GHz Wi-Fi works
- DHCP and LuCI work
- Ethernet MAC is read correctly from factory partition
- SYS LED works on GPIO 11
- Reset button works on GPIO 38
- Persistent JFFS2 overlay works after reboot
- SSH and LuCI remain available after reboot

## Files

- `dts/mt7628an_bigeon_sr1.dts` - device tree
- `patches/0001-bigeon-sr1-openwrt-24.10.5.patch` - OpenWrt source changes

## Target

Tested with:

- OpenWrt 24.10.5
- Linux 6.6.119
- Target: `ramips/mt76x8`

## Warning

Do not flash firmware from this repository unless you have confirmed your device hardware matches the Bigeon SR1 described above.

Keep backups of the original flash, especially the factory/EEPROM data and full flash dump.

## LuCI attribution patch

`patches/0002-luci-add-bigeon-sr1-attribution.patch` adds the following attribution to the LuCI Bootstrap footer:

`Bigeon SR1 OpenWrt 适配：微茫世间 · GitHub`

The GitHub link points to:

`https://github.com/tigaotg/openwrt-bigeon-sr1`
