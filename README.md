# Custom Linux Kernel for Raspberry Pi 3

## Description

This custom Linux kernel for the Raspberry Pi 3 includes several patches aimed at enhancing performance, memory management, and specific system features.

## Features
- **Kernel based on 6.6.51**

- **Patch comes from**
  - [Tkg](https://github.com/Frogging-Family/linux-tkg/tree/master/linux-tkg-patches)
  - [ClearLinux](https://github.com/clearlinux-pkgs/linux)
  - [BoreScheduler](https://github.com/firelzrd/bore-scheduler)
  - [XanMod](https://github.com/xanmod/linux-patches/tree/master)
  - [LNRG](https://github.com/smuellerDD/lrng)

- **Build Config**
  - O3
  - Zenify=true
  - Bore=true
  - Tcp_cong=BBR3
  - Tcp_sched=FQ_CODEL
  - LNRG as random generator replacement
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
- **0001-tcp-Add-a-sysctl-to-skip-tcp-collapse-processing-whe.patch**
- **0007-XANMOD-block-mq-deadline-Increase-write-priority-to-.patch**
- **0008-XANMOD-block-mq-deadline-Disable-front_merges-by-def.patch**
- **0009-XANMOD-block-set-rq_affinity-to-force-full-multithre.patch**
- **0012-XANMOD-mm-Raise-max_map_count-default-value.patch**
- **0016-XANMOD-lib-kconfig.debug-disable-default-CONFIG_SYMB.patch**
- **0001-net-tcp_bbr-broaden-app-limited-rate-sample-detectio.patch..0015-tcp-introduce-per-route-feature-RTAX_FEATURE_ECN_LOW.patch**
- **0001-lrng-patches**
