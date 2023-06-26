# Apache NuttX RTOS for Pine64 Star64 64-bit RISC-V SBC (StarFive JH7110)

Read the articles...

-   ["64-bit RISC-V with Apache NuttX Real-Time Operating System"](https://lupyuen.github.io/articles/riscv)

-   ["Rolling to RISC-V"](https://lupyuen.github.io/articles/pinephone2#rolling-to-risc-v)

# Linux Images for Star64

Let's examine the Linux Images for Star64 SBC, to see how U-Boot Bootloader is configured. (We'll boot NuttX later with U-Boot)

According to [Software Releases for Star64](https://wiki.pine64.org/wiki/STAR64#Software_releases), we have...

-   [Yocto Images](https://github.com/Fishwaldo/meta-pine64) at [pine64.my-ho.st](https://pine64.my-ho.st:8443/)

    Let's inspect [star64-image-minimal](https://pine64.my-ho.st:8443/star64-image-minimal-star64-1.2.wic.bz2)

-   [Armbian Images](https://www.armbian.com/star64/)

    Let's inspect [Armbian 23.8 Lunar (Minimal)](https://github.com/armbianro/os/releases/download/23.8.0-trunk.56/Armbian_23.8.0-trunk.56_Star64_lunar_edge_5.15.0_minimal.img.xz)

# Armbian Image for Star64

Let's inspect the Armbian Image for Star64: [Armbian 23.8 Lunar (Minimal)](https://github.com/armbianro/os/releases/download/23.8.0-trunk.56/Armbian_23.8.0-trunk.56_Star64_lunar_edge_5.15.0_minimal.img.xz)

Uncompress the .xz, mount the .img file on Linux / macOS / Windows as an ISO Volume.

The image contains 1 used partition: `armbi_root` (642 MB) that contains the Linux Root Filesystem.

We see the U-Boot Bootloader Configuration at `armbi_root/boot/uEnv.txt`...

```text
fdt_high=0xffffffffffffffff
initrd_high=0xffffffffffffffff

kernel_addr_r=0x44000000
kernel_comp_addr_r=0x90000000
kernel_comp_size=0x10000000

fdt_addr_r=0x48000000
ramdisk_addr_r=0x48100000

# Move distro to first boot to speed up booting
boot_targets=distro mmc1 dhcp 

distro_bootpart=1

# Fix missing bootcmd
bootcmd=run bootcmd_distro
```

# Yocto Image for Star64

Let's inspect the Yocto Image for Star64: [star64-image-minimal](https://pine64.my-ho.st:8443/star64-image-minimal-star64-1.2.wic.bz2)

Uncompress the .bz2, rename as .img. Balena Etcher won't work with .bz2 files!

Write the .img to a microSD Card with Balena Etcher. Insert the microSD Card into a Linux Machine. (Like Pinebook Pro)

We'll see 4 used partitions...

-   spl (2 MB): ???

-   uboot (4 MB): U-Boot Bootloader

-   boot (380 MB): Boot Configuration for U-Boot

-   root (686 MB): Linux Root Filesystem

Plus 2 unused partitions. (Why?)

![Yocto Image for Star64](https://lupyuen.github.io/images/star64-yocto.png)

`boot` partition has 2 files...

```text
$ ls -l /run/media/luppy/boot
total 14808
-rw-r--r-- 1 luppy luppy 15151064 Apr  6  2011 fitImage
-rw-r--r-- 1 luppy luppy     1562 Apr  6  2011 vf2_uEnv.txt
```

`boot/vf2_uEnv.txt` contains the U-Boot Bootloader Configuration...

```text
# This is the sample jh7110_uEnv.txt file for starfive visionfive U-boot
# The current convention (SUBJECT TO CHANGE) is that this file
# will be loaded from the third partition on the
# MMC card.
#devnum=1
partnum=3

# The FIT file to boot from
fitfile=fitImage

# for debugging boot
bootargs_ext=if test ${devnum} = 0; then setenv bootargs "earlyprintk console=tty1 console=ttyS0,115200 rootwait earlycon=sbi root=/dev/mmcblk0p4"; else setenv bootargs "earlyprintk console=tty1 console=ttyS0,115200 rootwait earlycon=sbi root=/dev/mmcblk1p4"; fi;
#bootargs=earlyprintk console=ttyS0,115200 debug rootwait earlycon=sbi root=/dev/mmcblk1p4

# for addr info
fileaddr=0xa0000000
fdtaddr=0x46000000
# boot Linux flat or compressed 'Image' stored at 'kernel_addr_r'
kernel_addr_r=0x40200000
irdaddr=46100000
irdsize=5f00000

# Use the FDT in the FIT image..
setupfdt1=fdt addr ${fdtaddr}; fdt resize;

setupird=setexpr irdend ${irdaddr} + ${irdsize}; fdt set /chosen linux,initrd-start <0x0 0x${irdaddr}>; fdt set /chosen linux,initrd-end <0x0 0x${irdend}>

setupfdt2=fdt set /chosen bootargs "${bootargs}";

bootwait=setenv _delay ${bootdelay}; echo ${_delay}; while test ${_delay} > 0; do sleep 1; setexpr _delay ${_delay} - 1; echo ${_delay}; done

boot2=run bootargs_ext; mmc dev ${devnum}; fatload mmc ${devnum}:${partnum} ${fileaddr} ${fitfile}; bootm start ${fileaddr}; run setupfdt1;run setupird;run setupfdt2; bootm loados ${fileaddr}; run chipa_set_linux; run cpu_vol_set; echo "Booting kernel in"; booti ${kernel_addr_r} ${irdaddr}:${filesize} ${fdtaddr}
```

TODO: Yocto boots from FIT File `fitImage`? Is this a Linux Flat Image?

# TODO
