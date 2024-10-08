# Hardware Compatibility

This document tracks the current hardware compatibility of Redox.

- [Status](#status)
- [General](#general)
- [Template](#template)
- [Recommended](#recommended)
- [Booting](#booting)
- [Broken](#broken)

## Status

- Broken - The system can't boot.
- Booting - The system boots with some issues.
- Recommended - The system start with all features working.

## General

This section cover things to consider.

- ACPI support is incomplete (some things are hardcoded on the kernel)
- Only USB input devices are supported
- Wi-Fi is not supported
- GPU drivers aren't supported (only VESA and UEFI GOP)
- Automatic operating system discovery on boot loader is not implemented (remember this before installing Redox)

## Template

You will use this template to insert your computer on the table.

```
|  |  |  |  |  |  |  |  |
```

## Recommended

| **Vendor** | **Model** | **Redox Version** | **Image Date** | **Variant** | **CPU Architecture** | **Motherboard Firmware** | **Report** |
|------------|-----------|-------------------|----------------|-------------|----------------------|--------------------------|------------|
| System76 | Galago Pro (galp5) | 0.8.0 | 11-11-2022 | desktop | x86-64 | UEFI | Boots to Orbital |
| System76 | Lemur Pro (lemp9) | 0.8.0 | 11-11-2022 | desktop | x86-64 | UEFI | Boots to Orbital |
| Lenovo | IdeaPad Y510P | 0.8.0 | 11-11-2022 | desktop | x86-64 | BIOS, UEFI | Boots to Orbital |
|  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |

## Booting

| **Vendor** | **Model** | **Redox Version** | **Image Date** | **Variant** | **CPU Architecture** | **Motherboard Firmware** | **Report** |
|------------|-----------|-------------------|----------------|-------------|----------------------|--------------------------|------------|
| System76 | Oryx Pro (oryp10) | 0.8.0 | 11-11-2022 | desktop | x86-64 | UEFI | Boots to Orbital, No touchpad support, though it should be working |
| System76 | Pangolin (pang12) | 0.8.0 | 11-11-2022 | desktop | x86-64 | UEFI | Boots to Orbital, No touchpad support, requires I2C HID |
| Dell | XPS 13 (9350) | 0.8.0 | 11-11-2022 | desktop | x86-64 | BIOS, UEFI | Boots to Orbital, NVMe driver livelocks |
| HP | Dev One | 0.8.0 | 11-11-2022 | desktop | x86-64 | UEFI | Boots to Orbital, No touchpad support, requires I2C HID |
| ASUS | X554L | 0.8.0 | 11-11-2022 | desktop | x86-64 | BIOS | Boots to Orbital, No audio, HDA driver cannot find output pins |
| ASUS | ROG g55vw | 0.8.0 | 11-11-2023 | desktop | x86-64 | BIOS | Boots to Orbital, UEFI panic in SETUP |
| Toshiba | Satellite L500 | 0.8.0 | 11-11-2022 | desktop | x86-64 | BIOS | Boots to Orbital, No ethernet driver, Correct video mode not offered (firmware issue) |
|  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |

## Broken

| **Vendor** | **Model** | **Redox Version** | **Image Date** | **Variant** | **CPU Architecture** | **Motherboard Firmware** | **Report** |
|------------|-----------|-------------------|----------------|-------------|----------------------|--------------------------|------------|
| HP | EliteBook 2570p | 0.8.0 | 23-11-2022 | demo | x86-64 | BIOS (CSM mode?) | Gets to resolution selection, Fails assert in `src/os/bios/mod.rs:77` after selecting resolution |
| BEELINK | U59 | 0.8.0 | 30-05-2024 | server | x86-64 | Unknown | Aborts after panic in xhcid |
| ASUS | PN41 | 0.8.0 | 30-05-2024 | server | x86-64 | Unknown | Aborts after panic in xhcid |
| Lenovo | G570 | 0.8.0 | 11-11-2022 | desktop | x86-64 | BIOS | Bootloader panics in `alloc_zeroed_page_aligned`, Correct video mode not offered (firmware issue) |
|  |  |  |  |  |  |  |  |
|  |  |  |  |  |  |  |  |

## x86-64

### Framework

- **Framework Laptop 16 (AMD Ryzen 7040 Series)**

```
Status - Broken
Redox version - 0.9.0
Variant - demo, server
Image date - 07-09-2024

- Bootloader loaded using UEFI
- Black screen and unresponsive after the bootloader and resolution selection
```

### Custom

If you have a customized computer, put it here.

- **ASUS PRIME B350M-E**

```
Status - Booting
Redox version - 0.9.0
Variant - desktop
Image date - 20-09-2024

- UEFI Firmware: 6203
- Boot: UEFI, Secure Boot Off/OtherOS, USB 2.0 Flash
- PS/2 Keyboard: Partial
- PS/2 Mouse: Broken
```

## i686

Computers with a 32 bits Intel/AMD CPU.

### Dell

- **Dell XPS 13 (9350)**

```
Status - Booting
Redox version - 0.8.0
Variant - desktop
Image date - 11-11-2022

- Booted using BIOS
- Boots to desktop
- NVMe driver livelocks
```

### ASUS

- **ASUS Eee PC 900**

```
Status - Booting
Redox version - 0.8.0
Variant - desktop
Image date - 11-11-2022

- Booted using BIOS
- Correct video mode not offered, this is a firmware issue
- Boots to desktop
- No ethernet driver
```

### Lenovo

- **Lenovo IdeaPad Y510P**

```
Status - Broken
Redox version - 0.8.0
Variant - desktop
Image date - 11-11-2022

- Booted using BIOS
- Panics on phys_to_virt overflow, probably having invalid mappings for 32-bit
```

### Toshiba

- **Toshiba Satellite L500**

```
Status - Broken
Redox version - 0.8.0
Variant - desktop
Image date - 11-11-2022

- Booted using BIOS
- Correct video mode not offered, this is a firmware issue
- Panics on phys_to_virt overflow, probably having invalid mappings for 32-bit
```

### Panasonic

- **Panasonic Toughbook CF-18**

```
Status - Broken
Redox version - 0.8.0
Variant - desktop
Image date - 11-11-2022

- Booted using BIOS
- Hangs after PIT initialization
```

### Custom

If you have a customized computer, put it here.



## ARM64

Computers using a 64 bits ARM CPU.

### Raspberry Pi

- **Raspberry Pi 3 Model B+**

```
Status - Booting
Redox version - 0.8.0
Variant - server
Image date - None

- Booted using Uboot
- Boots to UART serial console
- a bcm2835-sdhci/mmc driver
- pl011 UART
```

### Custom

If you have a customized ARM board, put it here.

