# Custom Linux Kernel for Raspberry Pi 3

## Description

This custom Linux kernel for the Raspberry Pi 3 includes several patches aimed at enhancing performance, memory management, and specific system features. It is based on kernel version 6.6.30, with additional optimizations for improved functionality on the Raspberry Pi 3.

## Features
- **Patch comes from**
  - [Tkg](https://github.com/Frogging-Family/linux-tkg/tree/master/linux-tkg-patches)
  - [ClearLinux](https://github.com/clearlinux-pkgs/linux)
  - [BoreScheduler](https://github.com/firelzrd/bore-scheduler)

- **Build Config**
  - O3
  - Zenify=true
  - Bore=true

- **CPU & Scheduler Optimizations:**
  - **0001-linux6.6.30-bore5.1.11.patch**: .
  - **0003-glitched-eevdf-additions.patch**: Adds experimental changes for the EEVDF scheduler for more efficient CPU time distribution.
  - **0166-sched-fair-remove-upper-limit-on-cpu-number.patch**: Removes the upper limit on CPU number to better scale with multi-core CPUs.

- **Memory Management Enhancements:**
  - **0001-mm-Support-soft-dirty-flag-reset-for-VA-range.patch**: Adds support for resetting the soft-dirty flag for virtual address ranges.
  - **0002-mm-Support-soft-dirty-flag-read-with-reset.patch**: Adds functionality to read and reset the soft-dirty flag.
  - **0161-ACPI-align-slab-buffers-for-improved-memory-performa.patch**: Optimizes memory alignment in ACPI for better performance.

- **File System & Storage:**
  - **0102-increase-the-ext4-default-commit-age.patch**: Increases the default commit age for the ext4 filesystem to improve write performance.
  - **0134-md-raid6-algorithms-scale-test-duration-for-speedier.patch**: Speeds up RAID6 initialization by scaling test duration.
  
- **Locking & Synchronization:**
  - **0121-locking-rwsem-spin-faster.patch**: Speeds up locking mechanisms for faster multi-threaded operations.

- **Networking:**
  - **0167-net-sock-increase-default-number-of-_SK_MEM_PACKETS-.patch**: Increases the default number of socket memory packets to enhance network performance.

- **I/O and Device Initialization:**
  - **0109-initialize-ata-before-graphics.patch**: Ensures ATA devices are initialized before graphics for improved boot stability.
  - **000


## Installation
```sh
sudo apt install bc bison flex libssl-dev make
```
```sh
cd linux

KERNEL=kernel8

make bcmrpi3_defconfig
```
```sh
make -j4 Image.gz modules dtbs
```
```sh
sudo make -j4 modules_install
```
```sh
sudo cp /boot/firmware/$KERNEL.img /boot/firmware/$KERNEL-backup.img

sudo cp arch/arm64/boot/Image.gz /boot/firmware/$KERNEL.img

sudo cp arch/arm64/boot/dts/broadcom/*.dtb /boot/firmware/

sudo cp arch/arm64/boot/dts/overlays/*.dtb* /boot/firmware/overlays/

sudo cp arch/arm64/boot/dts/overlays/README /boot/firmware/overlays/
```

## Applied Patches

- **0001-linux6.6.30-bore5.1.11.patch**  
- **0013-optimize_harder_O3.patch**  
- **0130-itmt2-ADL-fixes.patch**  
- **0161-ACPI-align-slab-buffers-for-improved-memory-performa.patch**  
- **0001-mm-Support-soft-dirty-flag-reset-for-VA-range.patch**  
- **0102-increase-the-ext4-default-commit-age.patch**  
- **0131-add-a-per-cpu-minimum-high-watermark-an-tune-batch-s.patch**  
- **0166-sched-fair-remove-upper-limit-on-cpu-number.patch**  
- **0002-mm-Support-soft-dirty-flag-read-with-reset.patch**  
- **0108-smpboot-reuse-timer-calibration.patch**  
- **0134-md-raid6-algorithms-scale-test-duration-for-speedier.patch**  
- **0167-net-sock-increase-default-number-of-_SK_MEM_PACKETS-.patch**  
- **0003-glitched-eevdf-additions.patch**  
- **0109-initialize-ata-before-graphics.patch**  
- **0135-initcall-only-print-non-zero-initcall-debug-to-speed.patch**  
- **0007-v6.6-fsync1_via_futex_waitv.patch**  
- **0121-locking-rwsem-spin-faster.patch**  
- **0136-crypto-kdf-make-the-module-init-call-a-late-init-cal.patch**
