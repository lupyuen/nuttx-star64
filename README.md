![Pine64 Star64 64-bit RISC-V SBC](https://lupyuen.github.io/images/star64-title.jpg)

# Apache NuttX RTOS for Pine64 Star64 64-bit RISC-V SBC (StarFive JH7110)

[![Daily Build of NuttX for Star64](https://github.com/lupyuen/nuttx-star64/actions/workflows/star64.yml/badge.svg)](https://github.com/lupyuen/nuttx-star64/actions/workflows/star64.yml)

Read the articles...

-   ["RISC-V Star64 JH7110: Poking the Display Controller with U-Boot Bootloader"](https://lupyuen.github.io/articles/display3)

-   ["RISC-V Star64 JH7110: Inside the Display Controller"](https://lupyuen.github.io/articles/display2)

-   ["RTOS on a RISC-V SBC: Star64 JH7110 + Apache NuttX"](https://www.hackster.io/lupyuen/rtos-on-a-risc-v-sbc-star64-jh7110-apache-nuttx-2a7429)

-   ["Star64 JH7110 + NuttX RTOS: Creating the First Release for the RISC-V SBC"](https://lupyuen.github.io/articles/release)

-   ["Star64 JH7110 + NuttX RTOS: RISC-V PLIC Interrupts and Serial I/O"](https://lupyuen.github.io/articles/plic)

-   ["Star64 JH7110 + NuttX RTOS: RISC-V Semihosting and Initial RAM Disk"](https://lupyuen.github.io/articles/semihost)

-   ["Star64 JH7110 + NuttX RTOS: RISC-V Privilege Levels and UART Registers"](https://lupyuen.github.io/articles/privilege)

-   ["Apache NuttX RTOS on RISC-V: Star64 JH7110 SBC"](https://lupyuen.github.io/articles/nuttx2)

-   ["Star64 JH7110 RISC-V SBC: Boot from Network with U-Boot and TFTP"](https://lupyuen.github.io/articles/tftp)

Earlier articles...

-   ["Booting RISC-V Linux on Star64 JH7110 SBC"](https://lupyuen.github.io/articles/linux)

-   ["Inspecting the RISC-V Linux Images for Star64 JH7110 SBC"](https://lupyuen.github.io/articles/star64)

-   ["64-bit RISC-V with Apache NuttX Real-Time Operating System"](https://lupyuen.github.io/articles/riscv)

-   ["Rolling to RISC-V"](https://lupyuen.github.io/articles/pinephone2#rolling-to-risc-v)

Many thanks to CNXSoft for the coverage...

-   ["Star64 RISC-V SBC can now boot Apache NuttX real-time operating system"](https://www.cnx-software.com/2023/08/17/star64-risc-v-sbc-apache-nuttx-real-time-operating-system/)

Let's port Apache NuttX RTOS to [Pine64 Star64](https://wiki.pine64.org/wiki/STAR64) 64-bit RISC-V SBC!

(Based on [StarFive JH7110 SoC](https://doc-en.rvspace.org/Doc_Center/jh7110.html))

Hopefully NuttX will run on Pine64 PineTab-V, which is also based on StarFive JH7110 SoC.

# NuttX Automated Daily Build for Star64

NuttX for Star64 is now built automatically every day via GitHub Actions.

The Daily Releases are available here...

- [nuttx-star64/releases](https://github.com/lupyuen/nuttx-star64/releases)

[nuttx.hash](https://github.com/lupyuen/nuttx-star64/releases/download/nuttx-star64-2023-08-11/nuttx.hash) contains the Commit Hash of the NuttX Kernel and NuttX Apps repos...

```text
NuttX Source: https://github.com/apache/nuttx/tree/fa676f264fa16253213ff665052ba4691e56bf05
NuttX Apps: https://github.com/apache/nuttx-apps/tree/6196e03337a3c677aba0c74e815af16e7075bc71
```

The GitHub Actions Workflow is here...

- [star64.yml](https://github.com/lupyuen/nuttx-star64/blob/main/.github/workflows/star64.yml)

Maybe someday we'll do Daily Automated Testing...

1.  Download the Daily Build to TFTP Server
1.  Power on Star64 with an [IKEA Smart Power Plug via Home Assistant](https://lupyuen.github.io/articles/tftp#whats-next)
1.  Star64 boots the Daily Build over TFTP
1.  Capture the Automated Testing Log and write to the Release Notes

[(Similar to BL602)](https://lupyuen.github.io/articles/auto)

# Linux Images for Star64

Read the article...

-   ["Inspecting the RISC-V Linux Images for Star64 JH7110 SBC"](https://lupyuen.github.io/articles/star64)

Let's examine the Linux Images for Star64 SBC, to see how U-Boot Bootloader is configured. (We'll boot NuttX later with U-Boot)

According to [Software Releases for Star64](https://wiki.pine64.org/wiki/STAR64#Software_releases), we have...

-   [Yocto Images](https://github.com/Fishwaldo/meta-pine64) at [pine64.my-ho.st](https://pine64.my-ho.st:8443/)

    Let's inspect [star64-image-minimal](https://pine64.my-ho.st:8443/star64-image-minimal-star64-1.2.wic.bz2)

-   [Armbian Images](https://www.armbian.com/star64/)

    Let's inspect [Armbian 23.8 Lunar (Minimal)](https://github.com/armbianro/os/releases/download/23.8.0-trunk.56/Armbian_23.8.0-trunk.56_Star64_lunar_edge_5.15.0_minimal.img.xz)

Current state of RISC-V Linux: [Linux on RISC-V (2022)](https://docs.google.com/presentation/d/1A0A6DnGyXR_MPpeg7QunQbv_yePPqid_uRswQe8Sj8M/edit#slide=id.p)

# Armbian Image for Star64

Read the article...

-   ["Inspecting the RISC-V Linux Images for Star64 JH7110 SBC"](https://lupyuen.github.io/articles/star64)

Let's inspect the Armbian Image for Star64: [Armbian 23.8 Lunar (Minimal)](https://github.com/armbianro/os/releases/download/23.8.0-trunk.56/Armbian_23.8.0-trunk.56_Star64_lunar_edge_5.15.0_minimal.img.xz)

Uncompress the .xz, mount the .img file on Linux / macOS / Windows as an ISO Volume.

The image contains 1 used partition: `armbi_root` (612 MB) that contains the Linux Root Filesystem.

Plus one unused partition (4 MB) at the top. (Partition Table)

![Armbian Image for Star64](https://lupyuen.github.io/images/star64-armbian.png)

We see the U-Boot Bootloader Configuration at `armbi_root/boot/extlinux/extlinux.conf`...

```text
label Armbian
  kernel /boot/Image
  initrd /boot/uInitrd
  fdt /boot/dtb/starfive/jh7110-star64-pine64.dtb
  append root=UUID=99f62df4-be35-475c-99ef-2ba3f74fe6b5 console=ttyS0,115200n8 console=tty0 earlycon=sbi rootflags=data=writeback stmmaceth=chain_mode:1 rw rw no_console_suspend consoleblank=0 fsck.fix=yes fsck.repair=yes net.ifnames=0 splash plymouth.ignore-serial-consoles
```

This says that U-Boot will load the Linux Kernel from `armbi_root/boot/Image`

Which is sym-linked to `armbi_root/boot/vmlinuz-5.15.0-starfive2`

_Where in RAM will the Kernel Image be loaded?_

According to [__kernel_addr_r__](https://u-boot.readthedocs.io/en/latest/develop/bootstd.html#environment-variables) from the [__Default U-Boot Settings__](https://github.com/lupyuen/nuttx-star64#u-boot-settings-for-star64), the Linux Kernel will be loaded at RAM Address __`0x4020` `0000`__...

```text
kernel_addr_r=0x40200000
```

[(Source)](https://github.com/lupyuen/nuttx-star64#u-boot-settings-for-star64)

_Everything looks hunky dory?_

Nope the [__Flattened Device Tree (FDT)__](https://u-boot.readthedocs.io/en/latest/develop/devicetree/index.html) is missing!

But the Flattened Device Tree (FDT) is missing! `/boot/dtb/starfive/jh7110-star64-pine64.dtb`

```text
fdt /boot/dtb/starfive/jh7110-star64-pine64.dtb
```

Which means that Armbian will [__fail to boot__](https://github.com/lupyuen/nuttx-star64#boot-armbian-on-star64) on Star64!

```text
Retrieving file: /boot/uInitrd
10911538 bytes read in 466 ms (22.3 MiB/s)
Retrieving file: /boot/Image
22040576 bytes read in 936 ms (22.5 MiB/s)
Retrieving file: /boot/dtb/starfive/jh7110-star64-pine64.dtb
Failed to load '/boot/dtb/starfive/jh7110-star64-pine64.dtb'
```

[(Source)](https://github.com/lupyuen/nuttx-star64#boot-armbian-on-star64)

The missing Device Tree is noted in this [__Pine64 Forum Post__](https://forum.pine64.org/showthread.php?tid=18276&pid=117607#pid117607). So we might need to check back later for the Official Armbian Image, if it's fixed.

[(__balbes150__ suggests that we try this Armbian Image instead)](https://forum.pine64.org/showthread.php?tid=18420&pid=118331#pid118331)


For Reference: Here's the list of __Supported Device Trees__...

```text
→ ls /Volumes/armbi_root/boot/dtb-5.15.0-starfive2/starfive
evb-overlay                      jh7110-evb-usbdevice.dtb
jh7110-evb-can-pdm-pwmdac.dtb    jh7110-evb.dtb
jh7110-evb-dvp-rgb2hdmi.dtb      jh7110-fpga.dtb
jh7110-evb-i2s-ac108.dtb         jh7110-visionfive-v2-A10.dtb
jh7110-evb-pcie-i2s-sd.dtb       jh7110-visionfive-v2-A11.dtb
jh7110-evb-spi-uart2.dtb         jh7110-visionfive-v2-ac108.dtb
jh7110-evb-uart1-rgb2hdmi.dtb    jh7110-visionfive-v2-wm8960.dtb
jh7110-evb-uart4-emmc-spdif.dtb  jh7110-visionfive-v2.dtb
jh7110-evb-uart5-pwm-i2c-tdm.dtb vf2-overlay
```

And here are the other files in __/boot__...

```text
→ ls -l /Volumes/armbi_root/boot
total 94416
lrwxrwxrwx       24 Image -> vmlinuz-5.15.0-starfive2
-rw-r--r--  4276712 System.map-5.15.0-starfive2
-rw-r--r--     1536 armbian_first_run.txt.template
-rw-r--r--    38518 boot.bmp
-rw-r--r--   144938 config-5.15.0-starfive2
lrwxrwxrwx       20 dtb -> dtb-5.15.0-starfive2
drwxr-xr-x        0 dtb-5.15.0-starfive2
drwxrwxr-x        0 extlinux
lrwxrwxrwx       27 initrd.img -> initrd.img-5.15.0-starfive2
-rw-r--r-- 10911474 initrd.img-5.15.0-starfive2
lrwxrwxrwx       27 initrd.img.old -> initrd.img-5.15.0-starfive2
-rw-rw-r--      341 uEnv.txt
lrwxrwxrwx       24 uInitrd -> uInitrd-5.15.0-starfive2
-rw-r--r-- 10911538 uInitrd-5.15.0-starfive2
lrwxrwxrwx       24 vmlinuz -> vmlinuz-5.15.0-starfive2
-rw-r--r-- 22040576 vmlinuz-5.15.0-starfive2
lrwxrwxrwx       24 vmlinuz.old -> vmlinuz-5.15.0-starfive2
```

TODO: Explain `boot/uInitrd` RAM Disk

# Yocto Image for Star64

Read the article...

-   ["Inspecting the RISC-V Linux Images for Star64 JH7110 SBC"](https://lupyuen.github.io/articles/star64)

Let's inspect the Yocto Image for Star64: [star64-image-minimal](https://pine64.my-ho.st:8443/star64-image-minimal-star64-1.2.wic.bz2)

Uncompress the .bz2, rename as .img. Balena Etcher won't work with .bz2 files!

Write the .img to a microSD Card with Balena Etcher. Insert the microSD Card into a Linux Machine. (Like Pinebook Pro)

We see 4 used partitions...

-   spl (2 MB): [Secondary Program Loader](https://u-boot.readthedocs.io/en/latest/board/starfive/visionfive2.html#flashing)

-   uboot (4 MB): [U-Boot Bootloader](https://u-boot.readthedocs.io/en/latest/board/starfive/visionfive2.html#flashing)

-   boot (380 MB): U-Boot Configuration and Linux Kernel Image

-   root (686 MB): Linux Root Filesystem

Plus one unused partition (2 MB) at the top. (Partition Table)

![Yocto Image for Star64](https://lupyuen.github.io/images/star64-yocto.png)

`boot` partition has 2 files...

```text
$ ls -l /run/media/$USER/boot
total 14808
-rw-r--r-- 1 15151064 Apr  6  2011 fitImage
-rw-r--r-- 1     1562 Apr  6  2011 vf2_uEnv.txt
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

[`kernel_addr_r`](https://u-boot.readthedocs.io/en/latest/develop/bootstd.html#environment-variables) says that Linux Kernel will be loaded at `0x4020` `0000`...

```text
# boot Linux flat or compressed 'Image' stored at 'kernel_addr_r'
kernel_addr_r=0x40200000
```

Yocto boots from the [Flat Image Tree (FIT)](https://u-boot.readthedocs.io/en/latest/usage/fit/index.html#): `boot/fitImage`

Yocto's `root/boot` looks different from Armbian...

```text
$ ls -l /run/media/$USER/root/boot
total 24376
lrwxrwxrwx 1       17 Mar  9  2018 fitImage -> fitImage-5.15.107
-rw-r--r-- 1  9807808 Mar  9  2018 fitImage-5.15.107
-rw-r--r-- 1 15151064 Mar  9  2018 fitImage-initramfs-5.15.107
```

# Boot NuttX with U-Boot Bootloader

Read the article...

-   ["Inspecting the RISC-V Linux Images for Star64 JH7110 SBC"](https://lupyuen.github.io/articles/star64)

_Will we boot NuttX with Armbian or Yocto settings?_

Armbian looks simpler, since it uses a plain Linux Kernel Image File `Image`. (Instead of Yocto's complicated Flat Image Tree)

Hence we'll overwrite Armbian's `armbi_root/boot/Image` by the NuttX Kernel Image.

We'll compile NuttX Kernel to boot at `0x4020` `0000`.

NuttX Kernel will begin with a RISC-V Linux Header. (See next section)

We'll use a Temporary File for the Flattened Device Tree (FDT) since it's missing from Armbian.

# Inside the Armbian Kernel Image

Read the article...

-   ["Inspecting the RISC-V Linux Images for Star64 JH7110 SBC"](https://lupyuen.github.io/articles/star64)

_What's inside the Armbian Linux Kernel Image?_

Let's look inside `armbi_root/boot/vmlinuz-5.15.0-starfive2`...

![Armbian Kernel Image](https://lupyuen.github.io/images/star64-kernel.png)

See the "RISCV" at `0x30`? That's the Magic Number for the RISC-V Linux Image Header!

-   ["Boot image header in RISC-V Linux"](https://www.kernel.org/doc/html/latest/riscv/boot-image-header.html)

```text
u32 code0;                /* Executable code */
u32 code1;                /* Executable code */
u64 text_offset;          /* Image load offset, little endian */
u64 image_size;           /* Effective Image size, little endian */
u64 flags;                /* kernel flags, little endian */
u32 version;              /* Version of this header */
u32 res1 = 0;             /* Reserved */
u64 res2 = 0;             /* Reserved */
u64 magic = 0x5643534952; /* Magic number, little endian, "RISCV" */
u32 magic2 = 0x05435352;  /* Magic number 2, little endian, "RSC\x05" */
u32 res3;                 /* Reserved for PE COFF offset */
```

This is how we decode the RISC-V Linux Header...

-   [__"Decode the RISC-V Linux Header"__](https://lupyuen.github.io/articles/star64#appendix-decode-the-risc-v-linux-header)

Let's decompile the Kernel Image...

TODO: Explain MZ and the funny RISC-V instruction at the top

# Decompile Armbian Kernel Image with Ghidra

Read the article...

-   ["Inspecting the RISC-V Linux Images for Star64 JH7110 SBC"](https://lupyuen.github.io/articles/star64)

We decompile the Armbian Linux Kernel Image with [Ghidra](https://github.com/NationalSecurityAgency/ghidra).

In Ghidra, create a New Project. Click File > Import File.

Select `armbi_root/boot/vmlinuz-5.15.0-starfive2` and enter these Import Options...

-   Format: Raw Binary

-   Language: RISCV > RV64GC (RISCV:LE:64:RV64GC:gcc)

    [(StarFive JH7110 has 4 × RV64GC U74 Application Cores)](https://doc-en.rvspace.org/JH7110/Datasheet/JH7110_DS/c_u74_quad_core.html)

-   Options > Base Address: 0x44000000

    (Based on the U-Boot Configuration from above)

![Load the Armbian Linux Kernel Image into Ghidra](https://lupyuen.github.io/images/star64-ghidra.png)

![Load the Armbian Linux Kernel Image into Ghidra](https://lupyuen.github.io/images/star64-ghidra2.png)

Double-click `vmlinuz-5.15.0-starfive2`, analyse the file with the Default Options.

Ghidra displays the Decompiled Linux Kernel...

![Disassembled Linux Kernel in Ghidra](https://lupyuen.github.io/images/star64-ghidra3.png)

At Address `0x4400` `0002` we see a Jump to `FUN_440010c8`...

```text
// Load -13 into Register S4
li  s4,-0xd

// Jump to Actual Boot Code
j   FUN_440010c8
```

Double-click `FUN_440010c8` to see the Linux Boot Code...

![Linux Boot Code in Ghidra](https://lupyuen.github.io/images/star64-ghidra4.png)

TODO: Explain MZ and the funny RISC-V instruction at the top

TODO: Where is the source file?

TODO: Any interesting CSR Instructions?

# Serial Console on Star64

Read the article...

-   ["Booting RISC-V Linux on Star64 JH7110 SBC"](https://lupyuen.github.io/articles/linux)

To access the Serial Console, we connect a [USB Serial Adapter](https://pine64.com/product/serial-console-woodpecker-edition/) to Star64...

![Star64 JH7110 RISC-V SBC with Woodpecker USB Serial Adapter](https://lupyuen.github.io/images/linux-title.jpg)

According to [Star64 Schematic](https://files.pine64.org/doc/star64/Star64_Schematic_V1.1_20230504.pdf), UART0 TX and RX (GPIO 5 and 6) are connected to the Pi GPIO Header (Pins 8 and 10).

Thus we connect these pins...

| Star64 GPIO Header | [USB Serial Adapter](https://pine64.com/product/serial-console-woodpecker-edition/) | Wire Colour |
|:----:|:----:|:----|
| Pin 6 (GND) | GND | Brown
| Pin 8 (TX) | RX | Red
| Pin 10 (RX) | TX | Orange

Set the Voltage Jumper to 3V3. (Instead of 5V)

![Pine64 Woodpecker Serial Adapter](https://lupyuen.github.io/images/star64-uart3.jpg)

On our computer, connect to the USB Serial Port at 115.2 kbps...

```bash
screen /dev/ttyUSB0 115200
```

Power up Star64. The DIP Switches for GPIO 0 and 1 default to Low and Low, so Star64 should boot from Flash Memory, which has the U-Boot Bootloader inside.

[(DIP Switch Labels are inverted: __"ON"__ actually means __"Low"__)](https://wiki.pine64.org/wiki/STAR64#Prototype_Bringup_Notes)

![DIP Switches for GPIO 0 and 1 are set to Low and Low](https://lupyuen.github.io/images/star64-uart2.jpg)

We'll see this U-Boot Bootloader Log...

TODO: Explain [OpenSBI](https://www.thegoodpenguin.co.uk/blog/an-overview-of-opensbi/)

# Star64 U-Boot Bootloader Log

Read the article...

-   ["Booting RISC-V Linux on Star64 JH7110 SBC"](https://lupyuen.github.io/articles/linux)

Here's the log for U-Boot Bootloader on Star64 (without microSD Card)...

![U-Boot Bootloader Log](https://lupyuen.github.io/images/star64-opensbi.jpg)

```text
U-Boot SPL 2021.10 (Jan 19 2023 - 04:09:41 +0800)
DDR version: dc2e84f0.
Trying to boot from SPI

OpenSBI v1.2
   ____                    _____ ____ _____
  / __ \                  / ____|  _ \_   _|
 | |  | |_ __   ___ _ __ | (___ | |_) || |
 | |  | | '_ \ / _ \ '_ \ \___ \|  _ < | |
 | |__| | |_) |  __/ | | |____) | |_) || |_
  \____/| .__/ \___|_| |_|_____/|____/_____|
        | |
        |_|

Platform Name             : StarFive VisionFive V2
Platform Features         : medeleg
Platform HART Count       : 5
Platform IPI Device       : aclint-mswi
Platform Timer Device     : aclint-mtimer @ 4000000Hz
Platform Console Device   : uart8250
Platform HSM Device       : jh7110-hsm
Platform PMU Device       : ---
Platform Reboot Device    : pm-reset
Platform Shutdown Device  : pm-reset
Firmware Base             : 0x40000000
Firmware Size             : 288 KB
Runtime SBI Version       : 1.0

Domain0 Name              : root
Domain0 Boot HART         : 1
Domain0 HARTs             : 0*,1*,2*,3*,4*
Domain0 Region00          : 0x0000000002000000-0x000000000200ffff (I)
Domain0 Region01          : 0x0000000040000000-0x000000004007ffff ()
Domain0 Region02          : 0x0000000000000000-0xffffffffffffffff (R,W,X)
Domain0 Next Address      : 0x0000000040200000
Domain0 Next Arg1         : 0x0000000042200000
Domain0 Next Mode         : S-mode
Domain0 SysReset          : yes

Boot HART ID              : 1
Boot HART Domain          : root
Boot HART Priv Version    : v1.11
Boot HART Base ISA        : rv64imafdcbx
Boot HART ISA Extensions  : none
Boot HART PMP Count       : 8
Boot HART PMP Granularity : 4096
Boot HART PMP Address Bits: 34
Boot HART MHPM Count      : 2
Boot HART MIDELEG         : 0x0000000000000222
Boot HART MEDELEG         : 0x000000000000b109


U-Boot 2021.10 (Jan 19 2023 - 04:09:41 +0800), Build: jenkins-github_visionfive2-6

CPU:   rv64imacu
Model: StarFive VisionFive V2
DRAM:  8 GiB
MMC:   sdio0@16010000: 0, sdio1@16020000: 1
Loading Environment from SPIFlash... SF: Detected gd25lq128 with page size 256 Bytes, erase size 4 KiB, total 16 MiB
*** Warning - bad CRC, using default environment

StarFive EEPROM format v2

--------EEPROM INFO--------
Vendor : PINE64
Product full SN: STAR64V1-2310-D008E000-00000003
data version: 0x2
PCB revision: 0xc1
BOM revision: A
Ethernet MAC0 address: 6c:cf:39:00:75:5d
Ethernet MAC1 address: 6c:cf:39:00:75:5e
--------EEPROM INFO--------

In:    serial@10000000
Out:   serial@10000000
Err:   serial@10000000
Model: StarFive VisionFive V2
Net:   eth0: ethernet@16030000, eth1: ethernet@16040000
Card did not respond to voltage select! : -110
Card did not respond to voltage select! : -110
bootmode flash device 0
Card did not respond to voltage select! : -110
Hit any key to stop autoboot:  2  1  0 
Card did not respond to voltage select! : -110
Couldn't find partition mmc 0:3
Can't set block device
Importing environment from mmc0 ...
## Warning: Input data exceeds 1048576 bytes - truncated
## Info: input data size = 1048578 = 0x100002
Card did not respond to voltage select! : -110
Couldn't find partition mmc 1:2
Can't set block device
## Warning: defaulting to text format
## Error: "boot2" not defined
Card did not respond to voltage select! : -110
ethernet@16030000 Waiting for PHY auto negotiation to complete......... TIMEOUT !
phy_startup() failed: -110FAILED: -110ethernet@16040000 Waiting for PHY auto negotiation to complete......... TIMEOUT !
phy_startup() failed: -110FAILED: -110ethernet@16030000 Waiting for PHY auto negotiation to complete......... TIMEOUT !
phy_startup() failed: -110FAILED: -110ethernet@16040000 Waiting for PHY auto negotiation to complete......... TIMEOUT !
phy_startup() failed: -110FAILED: -110StarFive # 
StarFive # 
```

Which is OK because we haven't inserted a microSD Card.

## U-Boot Commands for Star64

Here are the U-Boot Commands...

```text
StarFive # help
?         - alias for 'help'
base      - print or set address offset
bdinfo    - print Board Info structure
blkcache  - block cache diagnostics and control
boot      - boot default, i.e., run 'bootcmd'
bootd     - boot default, i.e., run 'bootcmd'
bootefi   - Boots an EFI payload from memory
bootelf   - Boot from an ELF image in memory
booti     - boot Linux kernel 'Image' format from memory
bootm     - boot application image from memory
bootp     - boot image via network using BOOTP/TFTP protocol
bootvx    - Boot vxWorks from an ELF image
cmp       - memory compare
config    - print .config
coninfo   - print console devices and information
cp        - memory copy
cpu       - display information about CPUs
crc32     - checksum calculation
dhcp      - boot image via network using DHCP/TFTP protocol
dm        - Driver model low level access
echo      - echo args to console
editenv   - edit environment variable
eeprom    - EEPROM sub-system
efidebug  - Configure UEFI environment
env       - environment handling commands
erase     - erase FLASH memory
eraseenv  - erase environment variables from persistent storage
exit      - exit script
ext2load  - load binary file from a Ext2 filesystem
ext2ls    - list files in a directory (default /)
ext4load  - load binary file from a Ext4 filesystem
ext4ls    - list files in a directory (default /)
ext4size  - determine a file's size
ext4write - create a file in the root directory
false     - do nothing, unsuccessfully
fatinfo   - print information about filesystem
fatload   - load binary file from a dos filesystem
fatls     - list files in a directory (default /)
fatmkdir  - create a directory
fatrm     - delete a file
fatsize   - determine a file's size
fatwrite  - write file into a dos filesystem
fdt       - flattened device tree utility commands
flinfo    - print FLASH memory information
fstype    - Look up a filesystem type
fstypes   - List supported filesystem types
fsuuid    - Look up a filesystem UUID
go        - start application at address 'addr'
gpio      - query and control gpio pins
gpt       - GUID Partition Table
gzwrite   - unzip and write memory to block device
help      - print command description/usage
i2c       - I2C sub-system
iminfo    - print header information for application image
imxtract  - extract a part of a multi-image
itest     - return true/false on integer compare
ln        - Create a symbolic link
load      - load binary file from a filesystem
loadb     - load binary file over serial line (kermit mode)
loads     - load S-Record file over serial line
loadx     - load binary file over serial line (xmodem mode)
loady     - load binary file over serial line (ymodem mode)
log       - log system
loop      - infinite loop on address range
ls        - list files in a directory (default /)
lzmadec   - lzma uncompress a memory region
mac       - display and program the system ID and MAC addresses in EEPROM
md        - memory display
misc      - Access miscellaneous devices with MISC uclass driver APIs
mm        - memory modify (auto-incrementing address)
mmc       - MMC sub system
mmcinfo   - display MMC info
mw        - memory write (fill)
net       - NET sub-system
nfs       - boot image via network using NFS protocol
nm        - memory modify (constant address)
panic     - Panic with optional message
part      - disk partition related commands
ping      - send ICMP ECHO_REQUEST to network host
pinmux    - show pin-controller muxing
printenv  - print environment variables
protect   - enable or disable FLASH write protection
random    - fill memory with random pattern
reset     - Perform RESET of the CPU
run       - run commands in an environment variable
save      - save file to a filesystem
saveenv   - save environment variables to persistent storage
setenv    - set environment variables
setexpr   - set environment variable as the result of eval expression
sf        - SPI flash sub-system
showvar   - print local hushshell variables
size      - determine a file's size
sleep     - delay execution for some time
source    - run script from memory
sysboot   - command to get and boot from syslinux files
test      - minimal test like /bin/sh
tftpboot  - boot image via network using TFTP protocol
tftpput   - TFTP put command, for uploading files to a server
true      - do nothing, successfully
unlz4     - lz4 uncompress a memory region
unzip     - unzip a memory region
version   - print monitor, compiler and linker version
```

## U-Boot Settings for Star64

Here are the U-Boot Settings...

```text
StarFive # printenv
baudrate=115200
boot_a_script=load ${devtype} ${devnum}:${distro_bootpart} ${scriptaddr} ${prefix}${script}; source ${scriptaddr}
boot_efi_binary=load ${devtype} ${devnum}:${distro_bootpart} ${kernel_addr_r} efi/boot/bootriscv64.efi; if fdt addr ${fdt_addr_r}; then bootefi ${kernel_addr_r} ${fdt_addr_r};else bootefi ${kernel_addr_r} ${fdtcontroladdr};fi
boot_efi_bootmgr=if fdt addr ${fdt_addr_r}; then bootefi bootmgr ${fdt_addr_r};else bootefi bootmgr;fi
boot_extlinux=sysboot ${devtype} ${devnum}:${distro_bootpart} any ${scriptaddr} ${prefix}${boot_syslinux_conf}
boot_prefixes=/ /boot/
boot_script_dhcp=boot.scr.uimg
boot_scripts=boot.scr.uimg boot.scr
boot_syslinux_conf=extlinux/extlinux.conf
boot_targets=mmc0 dhcp 
bootargs=console=ttyS0,115200  debug rootwait  earlycon=sbi
bootcmd=run load_vf2_env;run importbootenv;run load_distro_uenv;run boot2;run distro_bootcmd
bootcmd_dhcp=devtype=dhcp; if dhcp ${scriptaddr} ${boot_script_dhcp}; then source ${scriptaddr}; fi;setenv efi_fdtfile ${fdtfile}; setenv efi_old_vci ${bootp_vci};setenv efi_old_arch ${bootp_arch};setenv bootp_vci PXEClient:Arch:00027:UNDI:003000;setenv bootp_arch 0x1b;if dhcp ${kernel_addr_r}; then tftpboot ${fdt_addr_r} dtb/${efi_fdtfile};if fdt addr ${fdt_addr_r}; then bootefi ${kernel_addr_r} ${fdt_addr_r}; else bootefi ${kernel_addr_r} ${fdtcontroladdr};fi;fi;setenv bootp_vci ${efi_old_vci};setenv bootp_arch ${efi_old_arch};setenv efi_fdtfile;setenv efi_old_arch;setenv efi_old_vci;
bootcmd_distro=run fdt_loaddtb; run fdt_sizecheck; run set_fdt_distro; sysboot mmc ${fatbootpart} fat c0000000 ${bootdir}/${boot_syslinux_conf}; 
bootcmd_mmc0=devnum=0; run mmc_boot
bootdelay=2
bootdir=/boot
bootenv=uEnv.txt
bootmode=flash
bootpart=0:3
chip_vision=UNKOWN
chipa_gmac_set=fdt set /soc/ethernet@16030000/ethernet-phy@0 tx_inverted_10 <0x0>;fdt set /soc/ethernet@16030000/ethernet-phy@0 tx_inverted_100 <0x0>;fdt set /soc/ethernet@16030000/ethernet-phy@0 tx_inverted_1000 <0x0>;fdt set /soc/ethernet@16030000/ethernet-phy@0 tx_delay_sel <0x9>;fdt set /soc/ethernet@16040000/ethernet-phy@1 tx_inverted_10 <0x0>;fdt set /soc/ethernet@16040000/ethernet-phy@1 tx_inverted_100 <0x0>;fdt set /soc/ethernet@16040000/ethernet-phy@1 tx_inverted_1000 <0x0>;fdt set /soc/ethernet@16040000/ethernet-phy@1 tx_delay_sel <0x9> 
chipa_set=if test ${chip_vision} = A; then run chipa_gmac_set;fi; 
chipa_set_linux=fdt addr ${fdt_addr_r};run visionfive2_mem_set;run chipa_set;
chipa_set_linux_force=fdt addr ${fdt_addr_r};run visionfive2_mem_set;run chipa_gmac_set; 
chipa_set_uboot=fdt addr ${uboot_fdt_addr};run chipa_set;
chipa_set_uboot_force=fdt addr ${uboot_fdt_addr};run chipa_gmac_set; 
devnum=0
distro_bootcmd=for target in ${boot_targets}; do run bootcmd_${target}; done
distroloadaddr=0xb0000000
efi_dtb_prefixes=/ /dtb/ /dtb/current/
eth0addr=6c:cf:39:00:75:5d
eth1addr=6c:cf:39:00:75:5e
ethact=ethernet@16030000
ethaddr=6c:cf:39:00:75:5d
ext4bootenv=ext4load mmc ${bootpart} ${loadaddr} ${bootdir}/${bootenv}
fatbootpart=1:2
fdt_addr_r=0x46000000
fdt_high=0xffffffffffffffff
fdt_loaddtb=fatload mmc ${fatbootpart} ${fdt_addr_r} ${bootdir}/dtbs/${fdtfile}; fdt addr ${fdt_addr_r}; 
fdt_sizecheck=fatsize mmc ${fatbootpart} ${bootdir}/dtbs/${fdtfile}; 
fdtaddr=fffc6aa0
fdtcontroladdr=fffc6aa0
fdtfile=starfive/starfive_visionfive2.dtb
importbootenv=echo Importing environment from mmc${devnum} ...; env import -t ${loadaddr} ${filesize}
initrd_high=0xffffffffffffffff
ipaddr=192.168.120.230
kernel_addr_r=0x40200000
load_distro_uenv=fatload mmc ${fatbootpart} ${distroloadaddr} ${bootdir}/${bootenv}; env import ${distroloadaddr} 17c; 
load_efi_dtb=load ${devtype} ${devnum}:${distro_bootpart} ${fdt_addr_r} ${prefix}${efi_fdtfile}
load_vf2_env=fatload mmc ${bootpart} ${loadaddr} ${testenv}
loadaddr=0xa0000000
loadbootenv=fatload mmc ${bootpart} ${loadaddr} ${bootenv}
memory_addr=40000000
memory_size=200000000
mmc_boot=if mmc dev ${devnum}; then devtype=mmc; run scan_dev_for_boot_part; fi
mmcbootenv=run scan_mmc_dev; setenv bootpart ${devnum}:${mmcpart}; if mmc rescan; then run loadbootenv && run importbootenv; run ext4bootenv && run importbootenv; if test -n $uenvcmd; then echo Running uenvcmd ...; run uenvcmd; fi; fi
mmcpart=3
netmask=255.255.255.0
partitions=name=loader1,start=17K,size=1M,type=${type_guid_gpt_loader1};name=loader2,size=4MB,type=${type_guid_gpt_loader2};name=system,size=-,bootable,type=${type_guid_gpt_system};
preboot=run chipa_set_uboot;run mmcbootenv
pxefile_addr_r=0x45900000
ramdisk_addr_r=0x46100000
scan_dev_for_boot=echo Scanning ${devtype} ${devnum}:${distro_bootpart}...; for prefix in ${boot_prefixes}; do run scan_dev_for_extlinux; run scan_dev_for_scripts; done;run scan_dev_for_efi;
scan_dev_for_boot_part=part list ${devtype} ${devnum} -bootable devplist; env exists devplist || setenv devplist 1; for distro_bootpart in ${devplist}; do if fstype ${devtype} ${devnum}:${distro_bootpart} bootfstype; then run scan_dev_for_boot; fi; done; setenv devplist
scan_dev_for_efi=setenv efi_fdtfile ${fdtfile}; for prefix in ${efi_dtb_prefixes}; do if test -e ${devtype} ${devnum}:${distro_bootpart} ${prefix}${efi_fdtfile}; then run load_efi_dtb; fi;done;run boot_efi_bootmgr;if test -e ${devtype} ${devnum}:${distro_bootpart} efi/boot/bootriscv64.efi; then echo Found EFI removable media binary efi/boot/bootriscv64.efi; run boot_efi_binary; echo EFI LOAD FAILED: continuing...; fi; setenv efi_fdtfile
scan_dev_for_extlinux=if test -e ${devtype} ${devnum}:${distro_bootpart} ${prefix}${boot_syslinux_conf}; then echo Found ${prefix}${boot_syslinux_conf}; run boot_extlinux; echo SCRIPT FAILED: continuing...; fi
scan_dev_for_scripts=for script in ${boot_scripts}; do if test -e ${devtype} ${devnum}:${distro_bootpart} ${prefix}${script}; then echo Found U-Boot script ${prefix}${script}; run boot_a_script; echo SCRIPT FAILED: continuing...; fi; done
scan_mmc_dev=if test ${bootmode} = flash; then if mmc dev ${devnum}; then echo found device ${devnum};else setenv devnum 0;mmc dev 0;fi; fi; echo bootmode ${bootmode} device ${devnum};
scan_sf_for_scripts=${devtype} read ${scriptaddr} ${script_offset_f} ${script_size_f}; source ${scriptaddr}; echo SCRIPT FAILED: continuing...
script_offset_f=0x1fff000
script_size_f=0x1000
scriptaddr=0x43900000
serial#=STAR64V1-2310-D008E000-00000003
set_fdt_distro=if test ${chip_vision} = A; then if test ${memory_size} = 200000000; then run chipa_gmac_set;run visionfive2_mem_set;fatwrite mmc ${fatbootpart} ${fdt_addr_r} ${bootdir}/dtbs/${fdtfile} ${filesize};else run chipa_gmac_set;run visionfive2_mem_set;fatwrite mmc ${fatbootpart} ${fdt_addr_r} ${bootdir}/dtbs/${fdtfile} ${filesize};fi;else run visionfive2_mem_set;fatwrite mmc ${fatbootpart} ${fdt_addr_r} ${bootdir}/dtbs/${fdtfile} ${filesize};fi; 
sf_boot=if sf probe ${busnum}; then devtype=sf; run scan_sf_for_scripts; fi
stderr=serial@10000000
stdin=serial@10000000
stdout=serial@10000000
testenv=vf2_uEnv.txt
type_guid_gpt_loader1=5B193300-FC78-40CD-8002-E86C45580B47
type_guid_gpt_loader2=2E54B353-1271-4842-806F-E436D6AF6985
type_guid_gpt_system=0FC63DAF-8483-4772-8E79-3D69D8477DE4
uboot_fdt_addr=0xfffc6aa0
ver=U-Boot 2021.10 (Jan 19 2023 - 04:09:41 +0800)
visionfive2_mem_set=fdt memory ${memory_addr} ${memory_size};

Environment size: 7246/65532 bytes
StarFive # 
```

# Boot Armbian on Star64

Read the article...

-   ["Booting RISC-V Linux on Star64 JH7110 SBC"](https://lupyuen.github.io/articles/linux)

Let's boot Armbian on Star64!

We download the Armbian Image for Star64: [Armbian 23.8 Lunar (Minimal)](https://github.com/armbianro/os/releases/download/23.8.0-trunk.56/Armbian_23.8.0-trunk.56_Star64_lunar_edge_5.15.0_minimal.img.xz)

Uncompress the .xz, write the .img to a microSD Card with Balena Etcher.

Here's what happens when we boot the microSD Card on Star64...

-   [Armbian Boot Log](https://gist.github.com/lupyuen/d73ace627318375fe20e90e4950f9c50)

Armbian fails to boot...

```text
Found /boot/extlinux/extlinux.conf
Retrieving file: /boot/extlinux/extlinux.conf
383 bytes read in 7 ms (52.7 KiB/s)
1:[6CArmbian
Retrieving file: /boot/uInitrd
10911538 bytes read in 466 ms (22.3 MiB/s)
Retrieving file: /boot/Image
22040576 bytes read in 936 ms (22.5 MiB/s)
append: root=UUID=99f62df4-be35-475c-99ef-2ba3f74fe6b5 console=ttyS0,115200n8 console=tty0 earlycon=sbi rootflags=data=writeback stmmaceth=chain_mode:1 rw rw no_console_suspend consoleblank=0 fsck.fix=yes fsck.repair=yes net.ifnames=0 splash plymouth.ignore-serial-consoles
Retrieving file: /boot/dtb/starfive/jh7110-star64-pine64.dtb
Failed to load '/boot/dtb/starfive/jh7110-star64-pine64.dtb'
Skipping Armbian for failure retrieving FDT
```

The Flattened Device Tree (FDT) is missing! `/boot/dtb/starfive/jh7110-star64-pine64.dtb`

```text
→ ls /Volumes/armbi_root/boot/dtb-5.15.0-starfive2/starfive
evb-overlay                      jh7110-evb-usbdevice.dtb
jh7110-evb-can-pdm-pwmdac.dtb    jh7110-evb.dtb
jh7110-evb-dvp-rgb2hdmi.dtb      jh7110-fpga.dtb
jh7110-evb-i2s-ac108.dtb         jh7110-visionfive-v2-A10.dtb
jh7110-evb-pcie-i2s-sd.dtb       jh7110-visionfive-v2-A11.dtb
jh7110-evb-spi-uart2.dtb         jh7110-visionfive-v2-ac108.dtb
jh7110-evb-uart1-rgb2hdmi.dtb    jh7110-visionfive-v2-wm8960.dtb
jh7110-evb-uart4-emmc-spdif.dtb  jh7110-visionfive-v2.dtb
jh7110-evb-uart5-pwm-i2c-tdm.dtb vf2-overlay
```

The missing Device Tree is noted in this [__Pine64 Forum Post__](https://forum.pine64.org/showthread.php?tid=18276&pid=117607#pid117607). So we might need to check back later for the Official Armbian Image, if it's fixed.

[(__balbes150__ suggests that we try this Armbian Image instead)](https://forum.pine64.org/showthread.php?tid=18420&pid=118331#pid118331)

# Boot Yocto on Star64

Read the article...

-   ["Booting RISC-V Linux on Star64 JH7110 SBC"](https://lupyuen.github.io/articles/linux)

Now we boot Yocto on Star64.

We download the Yocto Minimal Image for Star64: [star64-image-minimal](https://pine64.my-ho.st:8443/star64-image-minimal-star64-1.2.wic.bz2)

Uncompress the .bz2, rename as .img. Balena Etcher won't work with .bz2 files!

Write the .img to a microSD Card with Balena Etcher.

Here's what happens when we boot the microSD Card on Star64...

-   [Yocto Boot Log](https://gist.github.com/lupyuen/b23edf50cecbee13e5aab3c0bae6c528)

Usernames and Passwords are...
-   root / pine64
-   pine64 / pine64

[(Source)](https://github.com/Fishwaldo/meta-pine64#usernames)

Yep the Yocto Minimal Image boots OK on Star64!

# Boot Yocto Plasma on Star64

Read the article...

-   ["Booting RISC-V Linux on Star64 JH7110 SBC"](https://lupyuen.github.io/articles/linux)

Finally we boot Yocto Plasma on Star64.

We download the Yocto Plasma Image for Star64: [star64-image-plasma](https://pine64.my-ho.st:8443/star64-image-plasma-star64-1.2.wic.bz2)

Uncompress the .bz2, rename as .img. Balena Etcher won't work with .bz2 files!

Write the .img to a microSD Card with Balena Etcher.

When we boot the microSD Card on Star64, the Plasma Desktop Environment runs OK on a HDMI Display! (Pic below)

Usernames and Passwords are...
-   root / pine64
-   pine64 / pine64

[(Source)](https://github.com/Fishwaldo/meta-pine64#usernames)

![Yocto Plasma on Star64](https://lupyuen.github.io/images/star64-plasma.jpg)

# NuttX prints to QEMU Console

Read the article...

-   ["Apache NuttX RTOS on RISC-V: Star64 JH7110 SBC"](https://lupyuen.github.io/articles/nuttx2)

Our NuttX Kernel will print to Star64 Serial Console for debugging. Before that, let's write some RISC-V Assembly Code to print to the QEMU Console!

Earlier we ran NuttX on QEMU Emulator for 64-bit RISC-V...

-   ["64-bit RISC-V with Apache NuttX Real-Time Operating System"](https://lupyuen.github.io/articles/riscv)

QEMU emulates a 16550 UART Port. (Similar to Star64 / JH7110)

_What's the Base Address of QEMU's UART Port?_

According to the NuttX Configuration for QEMU: [nsh64/defconfig](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64/boards/risc-v/qemu-rv/rv-virt/configs/nsh64/defconfig#L10-L16)

```text
CONFIG_16550_ADDRWIDTH=0
CONFIG_16550_UART0=y
CONFIG_16550_UART0_BASE=0x10000000
CONFIG_16550_UART0_CLOCK=3686400
CONFIG_16550_UART0_IRQ=37
CONFIG_16550_UART0_SERIAL_CONSOLE=y
CONFIG_16550_UART=y
```

Base Address of QEMU's UART Port is `0x1000` `0000`. (Same as Star64 / JH7110 yay!)

_How to print to the 16550 UART Port?_

Let's check the 16550 UART Driver in NuttX. From [uart_16550.c](https://github.com/apache/nuttx/blob/master/drivers/serial/uart_16550.c#L1539-L1553):

```c
/****************************************************************************
 * Name: u16550_send
 *
 * Description:
 *   This method will send one byte on the UART
 *
 ****************************************************************************/

static void u16550_send(struct uart_dev_s *dev, int ch)
{
  FAR struct u16550_s *priv = (FAR struct u16550_s *)dev->priv;
  u16550_serialout(priv, UART_THR_OFFSET, (uart_datawidth_t)ch);
}
```

[(u16550_serialout is defined here)](https://github.com/apache/nuttx/blob/master/drivers/serial/uart_16550.c#L610-L624)

To print a character, the driver writes to the UART Base Address (`0x1000` `0000`) at Offset UART_THR_OFFSET.

And we discover that [UART_THR_OFFSET](https://github.com/apache/nuttx/blob/dc69b108b8e0547ecf6990207526c27aceaf1e2e/include/nuttx/serial/uart_16550.h#L172-L200) is 0:

```c
#define UART_THR_INCR          0 /* (DLAB =0) Transmit Holding Register */
#define UART_THR_OFFSET        (CONFIG_16550_REGINCR*UART_THR_INCR)
```

So we can transmit to UART Port by simply writing to `0x1000` `0000`. How convenient!

_How to print to the QEMU Console?_

Let's do the printing in RISC-V Assembly Code, so that we can debug the NuttX Boot Code.

From [qemu_rv_head.S](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64/arch/risc-v/src/qemu-rv/qemu_rv_head.S#L71-L93):

```text
  /* Load UART Base Address to Register t0 */
  li  t0, 0x10000000

  /* Load `1` to Register t1 */
  li  t1, 0x31
  /* Store byte from Register t1 to UART Base Address, Offset 0 */
  sb  t1, 0(t0)

  /* Load `2` to Register t1 */
  li  t1, 0x32
  /* Store byte from Register t1 to UART Base Address, Offset 0 */
  sb  t1, 0(t0)

  /* Load `3` to Register t1 */
  li  t1, 0x33
  /* Store byte from Register t1 to UART Base Address, Offset 0 */
  sb  t1, 0(t0)
```

This prints "123" to the QEMU Console. Here's the output:

```text
+ qemu-system-riscv64 \
  -semihosting \
  -M virt,aclint=on \
  -cpu rv64 \
  -smp 8 \
  -bios none \
  -kernel nuttx \
  -nographic

123123123123123123112323
NuttShell (NSH) NuttX-12.0.3
nsh> 
```

Which is correct because QEMU is running with 8 CPUs. Yay!

![NuttX prints to QEMU Console](https://lupyuen.github.io/images/riscv-print.png)

[Cody AI Assistant](https://about.sourcegraph.com/cody) explains our RISC-V Assembly Code...

![Cody AI Assistant explains our RISC-V Assembly Code](https://lupyuen.github.io/images/riscv-cody1.png)

And offers to optimise our RISC-V Assembly Code...

![Cody AI Assistant optimises our RISC-V Assembly Code](https://lupyuen.github.io/images/riscv-cody2.png)

But the output is incorrect ;-)

```text
+ qemu-system-riscv64 -semihosting -M virt,aclint=on -cpu rv64 -smp 8 -bios none -kernel nuttx -nographic
11111111
NuttShell (NSH) NuttX-12.0.3
nsh> 
```

The correct output is `123123123123123123112323`. (Because of the 8 CPUs)

# UART Base Address for Star64

Read the article...

-   ["Apache NuttX RTOS on RISC-V: Star64 JH7110 SBC"](https://lupyuen.github.io/articles/nuttx2)

We'll take the UART Assembly Code from the previous section and run on Star64 / JH7110. (So we can troubleshoot the NuttX Boot Code)

_Does Star64 / JH7110 use a 16550 UART Controller like QEMU?_

According to the [JH7110 UART Developing Guide](https://doc-en.rvspace.org/VisionFive2/DG_UART/JH7110_SDK/function_layer.html), Star64 / JH7110 uses the 8250 UART Controller...

Which is [compatible with QEMU's 16550 UART Controller](https://en.wikipedia.org/wiki/16550_UART). So our UART Assembly Code for QEMU will run on Star64!

_What's the UART Base Address for Star64 / JH7110?_

Based on [JH7110 System Memory Map](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/system_memory_map.html), UART0 is at `0x1000` `0000`.

Also from the [JH7110 UART Device Tree](https://doc-en.rvspace.org/VisionFive2/DG_UART/JH7110_SDK/general_uart_controller.html): UART Register Base Address is `0x1000` `0000` with range `0x10000`.

[(JH7110 UART Datasheet)](https://doc-en.rvspace.org/JH7110/Datasheet/JH7110_DS/uart.html)

_Isn't that the same UART Base Address as QEMU?_

Let's check the UART Base Address in NuttX for QEMU. From [nsh64/defconfig](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64/boards/risc-v/qemu-rv/rv-virt/configs/nsh64/defconfig#L10-L16):

```text
CONFIG_16550_ADDRWIDTH=0
CONFIG_16550_UART0=y
CONFIG_16550_UART0_BASE=0x10000000
CONFIG_16550_UART0_CLOCK=3686400
CONFIG_16550_UART0_IRQ=37
CONFIG_16550_UART0_SERIAL_CONSOLE=y
CONFIG_16550_UART=y
```

NuttX UART Base Address is `0x1000` `0000`. The exact same UART Base Address for QEMU AND Star64!

So no changes needed, our UART Assembly Code will run on QEMU AND Star64 yay!

# RISC-V Linux Kernel Header

Read the article...

-   ["Apache NuttX RTOS on RISC-V: Star64 JH7110 SBC"](https://lupyuen.github.io/articles/nuttx2)

For U-Boot Bootloader to boot NuttX, we need to embed the RISC-V Linux Kernel Header...

-   [__"Inside the Kernel Image"__](https://lupyuen.github.io/articles/star64#inside-the-kernel-image)

This is how we decode the RISC-V Linux Header...

-   [__"Decode the RISC-V Linux Header"__](https://lupyuen.github.io/articles/star64#appendix-decode-the-risc-v-linux-header)

We copy the Arm64 Linux Header from [arm64_head.S](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64/arch/arm64/src/common/arm64_head.S#L79-L118)...

And tweak for RISC-V Linux Header, like this: [qemu_rv_head.S](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64/arch/risc-v/src/qemu-rv/qemu_rv_head.S#L42-L75):

```text
__start:
  /* Begin Test */

  /* DO NOT MODIFY. Image Header expected by Linux bootloaders.
   *
   * This `li` instruction has no meaningful effect except that
   * its opcode forms the magic "MZ" signature of a PE/COFF file
   * that is required for UEFI applications.
   *
   * Some bootloaders check the magic "MZ" to see if the image is a valid
   * Linux image. But modifying the bootLoader is unnecessary unless we
   * need to do a customized secure boot. So we just put "MZ" in the
   * header to make the bootloader happy.
   */

  c.li    s4, -13              /* Magic Signature "MZ" (2 bytes) */
  j       real_start           /* Jump to Kernel Start (2 bytes) */
  .long   0                    /* Executable Code padded to 8 bytes */
  .quad   0x200000             /* Image load offset from start of RAM */
  /* TODO: _e_initstack - __start */
  .quad   171644               /* Effective size of kernel image, little-endian */
  .quad   0x0                  /* Kernel flags, little-endian */
  .long   0x2                  /* Version of this header */
  .long   0                    /* Reserved */
  .quad   0                    /* Reserved */
  .ascii  "RISCV\x00\x00\x00"  /* Magic number, "RISCV" (8 bytes) */
  .ascii  "RSC\x05"            /* Magic number 2, "RSC\x05" (4 bytes) */
  .long   0                    /* Reserved for PE COFF offset */

real_start:

  /* Load UART Base Address to Register t0 */
  li  t0, 0x10000000
```

Note that Image Load Offset must be `0x20` `0000`!

```text
  .quad   0x200000             /* Image load offset from start of RAM */
```

That's because our kernel starts at `0x4020` `0000`

Here's the assembled output...

```text
0000000040200000 <__start>:
  li      s4, -0xd             /* Magic Signature "MZ" (2 bytes) */
    40200000:  5a4d                  li  s4,-13
  j       real_start           /* Jump to Kernel Start (2 bytes) */
    40200002:  a83d                  j  40200040 <real_start>
    40200004:  0000                  unimp
    40200006:  0000                  unimp
    40200008:  0000                  unimp
    4020000a:  0020                  addi  s0,sp,8
    4020000c:  0000                  unimp
    4020000e:  0000                  unimp
    40200010:  9e7c                  0x9e7c
    40200012:  0002                  c.slli64  zero
  ...
    40200020:  0002                  c.slli64  zero
  ...
    4020002e:  0000                  unimp
    40200030:  4952                  lw  s2,20(sp)
    40200032:  00564353            fadd.s  ft6,fa2,ft5,rmm
    40200036:  0000                  unimp
    40200038:  5352                  lw  t1,52(sp)
    4020003a:  00000543            fmadd.s  fa0,ft0,ft0,ft0,rne
  ...

0000000040200040 <real_start>:
```

Check that the lengths and offsets match the RISC-V Linux Header Format...

-   [__"Decode the RISC-V Linux Header"__](https://lupyuen.github.io/articles/star64#appendix-decode-the-risc-v-linux-header)

And our RISC-V Boot Code tested OK with QEMU.

# Set Start Address of NuttX Kernel

Read the article...

-   ["Apache NuttX RTOS on RISC-V: Star64 JH7110 SBC"](https://lupyuen.github.io/articles/nuttx2)

Earlier we saw that Star64's U-Boot Bootloader will load Linux Kernels into RAM at Address `0x4020` `0000`...

- ["Armbian Image for Star64"](https://lupyuen.github.io/articles/star64#armbian-image-for-star64)

- ["Yocto Image for Star64"](https://lupyuen.github.io/articles/star64#yocto-image-for-star64)

To boot NuttX on Star64, let's set the Start Address of the NuttX Kernel to `0x4020` `0000`.

From [nsh64/defconfig](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64/boards/risc-v/qemu-rv/rv-virt/configs/nsh64/defconfig#L56-L57):

```text
CONFIG_RAM_SIZE=33554432
CONFIG_RAM_START=0x80000000
```

We changed the above NuttX Build Config to `0x40200000`

We also updated the Linker Script: [ld.script](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64/boards/risc-v/qemu-rv/rv-virt/scripts/ld.script#L21-L26)

```text
SECTIONS
{
  /* Previously 0x80000000 */
  . = 0x40200000;
  .text :
```

Remember to change this if building for NuttX Kernel Mode: [ld-kernel64.script](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64/boards/risc-v/qemu-rv/rv-virt/scripts/ld-kernel64.script#L21-L51):

```text
MEMORY
{
    /* Previously 0x80000000 */
    kflash (rx) : ORIGIN = 0x40200000, LENGTH = 2048K   /* w/ cache */
    /* Previously 0x80200000 */
    ksram (rwx) : ORIGIN = 0x40400000, LENGTH = 2048K   /* w/ cache */
    /* Previously 0x80400000 */
    pgram (rwx) : ORIGIN = 0x40600000, LENGTH = 4096K   /* w/ cache */
}
...
SECTIONS
{
  /* Previously 0x80000000 */
  . = 0x40200000;
  .text :
```

Which should match [knsh64/defconfig](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64/boards/risc-v/qemu-rv/rv-virt/configs/knsh64/defconfig):

```text
CONFIG_ARCH_PGPOOL_PBASE=0x40600000
CONFIG_ARCH_PGPOOL_VBASE=0x40600000
// TODO: Fix CONFIG_RAM_SIZE
CONFIG_RAM_SIZE=1048576
CONFIG_RAM_START=0x40200000
```

RISC-V Disassembly of NuttX Kernel shows that the Start Address is correct...

```text
0000000040200000 <__start>:
  li      s4, -0xd             /* Magic Signature "MZ" (2 bytes) */
    40200000:  5a4d                  li  s4,-13
  j       real_start           /* Jump to Kernel Start (2 bytes) */
    40200002:  a83d                  j  40200040 <real_start>
```

We're ready to boot NuttX on Star64!

# Boot NuttX on Star64

Read the article...

-   ["Apache NuttX RTOS on RISC-V: Star64 JH7110 SBC"](https://lupyuen.github.io/articles/nuttx2)

Let's boot NuttX on Star64! We compile [NuttX for 64-bit RISC-V QEMU](https://lupyuen.github.io/articles/riscv#appendix-build-apache-nuttx-rtos-for-64-bit-risc-v-qemu) with these tweaks...

- ["NuttX prints to QEMU Console"](https://github.com/lupyuen/nuttx-star64#nuttx-prints-to-qemu-console)

- ["UART Base Address for Star64"](https://github.com/lupyuen/nuttx-star64#uart-base-address-for-star64)

- ["RISC-V Linux Kernel Header"](https://github.com/lupyuen/nuttx-star64#risc-v-linux-kernel-header)

- ["Set Start Address of NuttX Kernel"](https://github.com/lupyuen/nuttx-star64#set-start-address-of-nuttx-kernel)

For the microSD Image, we pick this [__Armbian Image for Star64__](https://www.armbian.com/star64/)...

-   [__Armbian 23.8 Lunar for Star64 (Minimal)__](https://github.com/armbianro/os/releases/download/23.8.0-trunk.56/Armbian_23.8.0-trunk.56_Star64_lunar_edge_5.15.0_minimal.img.xz)

Write the Armbian Image to a microSD Card with Balena Etcher.

We fix the [Missing Device Tree](https://lupyuen.github.io/articles/star64#armbian-image-for-star64)...

```bash
## Fix the Missing Device Tree
sudo chmod go+w /run/media/$USER/armbi_root/boot
sudo chmod go+w /run/media/$USER/armbi_root/boot/dtb/starfive
cp \
  /run/media/$USER/armbi_root/boot/dtb/starfive/jh7110-visionfive-v2.dtb \
  /run/media/$USER/armbi_root/boot/dtb/starfive/jh7110-star64-pine64.dtb
```

Then we delete the sym-link `/boot/Image` and copy the NuttX Binary Image `nuttx.bin` to `/boot/Image`...

```bash
## We assume that `nuttx` contains the NuttX ELF Image.
## Export the NuttX Binary Image to `nuttx.bin`
riscv64-unknown-elf-objcopy \
  -O binary \
  nuttx \
  nuttx.bin

## Delete Armbian Kernel `/boot/Image`
rm /run/media/$USER/armbi_root/boot/Image

## Copy `nuttx.bin` to Armbian Kernel `/boot/Image`
cp nuttx.bin /run/media/$USER/armbi_root/boot/Image
```

Insert the microSD Card into Star64 and power up.

NuttX boots with `123` yay! [(Which is printed by our Boot Code)](https://github.com/lupyuen/nuttx-star64#nuttx-prints-to-qemu-console)

```text
Starting kernel ...
clk u5_dw_i2c_clk_core already disabled
clk u5_dw_i2c_clk_apb already disabled
123
Unhandled exception: Illegal instruction
```

![Boot NuttX on Star64](https://lupyuen.github.io/images/star64-nuttx.png)

Here's the complete log...

```text
Retrieving file: /boot/extlinux/extlinux.conf
383 bytes read in 7 ms (52.7 KiB/s)
1:[6CArmbian
Retrieving file: /boot/uInitrd
10911538 bytes read in 466 ms (22.3 MiB/s)
Retrieving file: /boot/Image
163201 bytes read in 14 ms (11.1 MiB/s)
append: root=UUID=99f62df4-be35-475c-99ef-2ba3f74fe6b5 console=ttyS0,115200n8 console=tty0 earlycon=sbi rootflags=data=writeback stmmaceth=chain_mode:1 rw rw no_console_suspend consoleblank=0 fsck.fix=yes fsck.repair=yes net.ifnames=0 splash plymouth.ignore-serial-consoles
Retrieving file: /boot/dtb/starfive/jh7110-star64-pine64.dtb
50235 bytes read in 14 ms (3.4 MiB/s)
## Loading init Ramdisk from Legacy Image at 46100000 ...
   Image Name:   uInitrd
   Image Type:   RISC-V Linux RAMDisk Image (gzip compressed)
   Data Size:    10911474 Bytes = 10.4 MiB
   Load Address: 00000000
   Entry Point:  00000000
   Verifying Checksum ... OK
## Flattened Device Tree blob at 46000000
   Booting using the fdt blob at 0x46000000
   Using Device Tree in place at 0000000046000000, end 000000004600f43a

Starting kernel ...

clk u5_dw_i2c_clk_core already disabled
clk u5_dw_i2c_clk_apb already disabled
123Unhandled exception: Illegal instruction
EPC: 000000004020005c RA: 00000000fff471c6 TVAL: 00000000f1402573
EPC: ffffffff804ba05c RA: 00000000402011c6 reloc adjusted

SP:  00000000ff733630 GP:  00000000ff735e00 TP:  0000000000000001
T0:  0000000010000000 T1:  0000000000000033 T2:  7869662e6b637366
S0:  0000000000000400 S1:  00000000ffff1428 A0:  0000000000000001
A1:  0000000046000000 A2:  0000000000000600 A3:  0000000000004000
A4:  0000000000000000 A5:  0000000040200000 A6:  00000000fffd5708
A7:  0000000000000000 S2:  00000000fff47194 S3:  0000000000000003
S4:  fffffffffffffff3 S5:  00000000fffdbb50 S6:  0000000000000000
S7:  0000000000000000 S8:  00000000fff47194 S9:  0000000000000002
S10: 0000000000000000 S11: 0000000000000000 T3:  0000000000000023
T4:  000000004600b5cc T5:  000000000000ff00 T6:  000000004600b5cc

Code: 0313 0320 8023 0062 0313 0330 8023 0062 (2573 f140)


resetting ...
reset not supported yet
### ERROR ### Please RESET the board ###
```

Why does NuttX crash at `4020005c`? See the next section...

![Cody AI Assistant tries to explain our RISC-V Exception](https://lupyuen.github.io/images/star64-exception.jpg)

_[Cody AI Assistant](https://about.sourcegraph.com/cody) tries to explain our RISC-V Exception_

# NuttX Fails To Get Hart ID

Read the article...

-   ["Apache NuttX RTOS on RISC-V: Star64 JH7110 SBC"](https://lupyuen.github.io/articles/nuttx2)

Earlier we saw NuttX crashing when booting on Star64...

```text
Starting kernel ...
clk u5_dw_i2c_clk_core already disabled
clk u5_dw_i2c_clk_apb already disabled
123
Unhandled exception: Illegal instruction
EPC: 000000004020005c RA: 00000000fff471c6 TVAL: 00000000f1402573
```

_Why did NuttX crash at `4020005c`?_

Here's our RISC-V Boot Code...

From [qemu_rv_head.S](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/ed09c34532ee7c51ac2da816cd6cf0adcce336e6/arch/risc-v/src/qemu-rv/qemu_rv_head.S#L92-L103):

```text
nuttx/arch/risc-v/src/chip/qemu_rv_head.S:95
  /* Load mhartid (cpuid) */
  csrr a0, mhartid
    4020005c:  f1402573  csrr a0, mhartid
```

NuttX tries loads the CPU ID or Hardware Thread "Hart" ID from the RISC-V Control and Status Register (CSR). [(Explained here)](https://lupyuen.github.io/articles/riscv#get-cpu-id)

But it fails! Because we don't have sufficient privilege to access the Hart ID...

# RISC-V Privilege Levels

Read the article...

-   ["Apache NuttX RTOS on RISC-V: Star64 JH7110 SBC"](https://lupyuen.github.io/articles/nuttx2)

RISC-V runs at 3 Privilege Levels...

- M: Machine Mode (Most powerful)

- S: Supervisor Mode (Less powerful)

- U: User Mode (Least powerful)

NuttX runs at Supervisor Mode, which [doesn't allow access to Machine-Mode CSR Registers](https://five-embeddev.com/riscv-isa-manual/latest/machine.html).  (Including [Hart ID](https://five-embeddev.com/riscv-isa-manual/latest/machine.html#hart-id-register-mhartid))

(The `m` in `mhartid` signifies that it's a Machine-Mode Register)

![RISC-V Privilege Levels](https://lupyuen.github.io/images/nuttx2-privilege.jpg)

_What runs in Machine Mode?_

[OpenSBI](https://www.thegoodpenguin.co.uk/blog/an-overview-of-opensbi/) (Supervisor Binary Interface) is the first thing that boots on Star64. It runs at Machine Mode and starts the U-Boot Bootloader.

[(See the RISC-V SBI Spec)](https://github.com/riscv-non-isa/riscv-sbi-doc/blob/master/riscv-sbi.pdf)

_What about U-Boot Bootloader?_

U-Boot Bootloader runs in Supervisor Mode. And starts NuttX, also in Supervisor Mode.

So OpenSBI is the only thing that runs in Machine Mode. And can access the Machine-Level Registers.

_QEMU doesn't have this problem?_

Because QEMU runs everything in (super-powerful) __Machine Mode__!

![NuttX QEMU runs in Machine Mode](https://lupyuen.github.io/images/nuttx2-privilege2.jpg)

NuttX needs to fetch the Hart ID with a different recipe...

# Downgrade NuttX to Supervisor Mode

Read the article...

-   ["Apache NuttX RTOS on RISC-V: Star64 JH7110 SBC"](https://lupyuen.github.io/articles/nuttx2)

_How to get the Hart ID from OpenSBI?_

Let's refer to the Linux Boot Code: [linux/arch/riscv/kernel/head.S](https://github.com/torvalds/linux/blob/master/arch/riscv/kernel/head.S)

(Tip: `CONFIG_RISCV_M_MODE` is False and `CONFIG_EFI` is True)

From [linux/blob/master/arch/riscv/kernel/head.S](https://github.com/torvalds/linux/blob/master/arch/riscv/kernel/head.S#L292-L295):

```c
/* Save hart ID and DTB physical address */
mv s0, a0
mv s1, a1
```

Here we see that U-Boot [(or OpenSBI)](https://github.com/riscv-non-isa/riscv-sbi-doc/blob/master/riscv-sbi.adoc#function-hart-start-fid-0) will pass 2 arguments when it starts our kernel...

- Register A0: Hart ID

- Register A1: RAM Address of Device Tree

So we'll simply read the Hart ID from Register A0. (And ignore A1)

We'll remove `csrr a0, mhartid`.

_What are the actual values of Registers A0 and A1?_

Thanks to our [earlier Crash Dump](https://github.com/lupyuen/nuttx-star64#boot-nuttx-on-star64), we know the actual values of A0 and A1!

```text
SP:  00000000ff733630 GP:  00000000ff735e00 TP:  0000000000000001
T0:  0000000010000000 T1:  0000000000000033 T2:  7869662e6b637366
S0:  0000000000000400 S1:  00000000ffff1428 A0:  0000000000000001
A1:  0000000046000000 A2:  0000000000000600 A3:  0000000000004000
```

This says that...

- Hart ID is 1 (Register A0)

- RAM Address of Device Tree is `0x4600` `0000` (Register A1)

Yep looks correct! But we'll subtract 1 from Register A0 because NuttX expects Hart ID to start with 0.

_What about other CSR Instructions in our NuttX Boot Code?_

We change the Machine-Level `m` Registers to Supervisor-Level `s` Registers.

To Disable Interrupts: Change `mie` to [`sie`](https://five-embeddev.com/riscv-isa-manual/latest/supervisor.html#supervisor-interrupt-registers-sip-and-sie)

```text
/* Disable all interrupts (i.e. timer, external) in mie */
csrw  mie, zero
```

[(Source)](https://lupyuen.github.io/articles/riscv#disable-interrupts)

To Load Interrupt Vector Table: Change `mtvec` to [`stvec`](https://five-embeddev.com/riscv-isa-manual/latest/supervisor.html#supervisor-trap-vector-base-address-register-stvec)

```text
/* Load address of Interrupt Vector Table */
csrw  mtvec, t0
```

[(Source)](https://lupyuen.github.io/articles/riscv#load-interrupt-vector)

_The Linux Boot Code looks confusing. What are CSR_IE and CSR_IP?_

```text
/* Mask all interrupts */
csrw CSR_IE, zero
csrw CSR_IP, zero
```

[(Source)](https://github.com/torvalds/linux/blob/master/arch/riscv/kernel/head.S#L195-L200)

That's because the Linux Boot Code will work for Machine Level AND Supervisor Level! Here's how `CSR_IE` and `CSR_IP` are mapped to the `m` and `s` CSR Registers...

(Remember: `CONFIG_RISCV_M_MODE` is false for NuttX)

```text
#ifdef CONFIG_RISCV_M_MODE
  /* Use Machine-Level CSR Registers */
  # define CSR_IE    CSR_MIE
  # define CSR_IP    CSR_MIP
  ...
#else
  /* Use Supervisor-Level CSR Registers */
  # define CSR_IE    CSR_SIE
  # define CSR_IP    CSR_SIP
  ...
#endif /* !CONFIG_RISCV_M_MODE */
```

[(Source)](https://github.com/torvalds/linux/blob/master/arch/riscv/include/asm/csr.h#L391-L444)

Let's fix the Boot Code...

# Fix the NuttX Boot Code

Read the article...

-   ["Apache NuttX RTOS on RISC-V: Star64 JH7110 SBC"](https://lupyuen.github.io/articles/nuttx2)

From the previous section, we identified these fixes for the NuttX Boot Code...

1.  Remove `csrr a0, mhartid` because OpenSBI will pass Hart ID in Register A0. Subtract 1 from Register A0 because NuttX expects Hart ID to start with 0.

1.  To Disable Interrupts: Change `mie` to [`sie`](https://five-embeddev.com/riscv-isa-manual/latest/supervisor.html#supervisor-interrupt-registers-sip-and-sie)

1.  To Load Interrupt Vector Table: Change `mtvec` to [`stvec`](https://five-embeddev.com/riscv-isa-manual/latest/supervisor.html#supervisor-trap-vector-base-address-register-stvec)

Here's the updated Boot Code, and our analysis: [qemu_rv_head.S](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64/arch/risc-v/src/qemu-rv/qemu_rv_head.S)

```text
real_start:
  ...
  /* Load mhartid (cpuid) */
  /* Previously: csrr a0, mhartid */

  /* We assume that OpenSBI has passed Hart ID (value 1) in Register a0. */
  /* But NuttX expects Hart ID to start at 0, so we subtract 1. */
  addi a0, a0, -1

  /* Print the Hart ID */
  addi t1, a0, 0x30
  /* Store byte from Register t1 to UART Base Address, Offset 0 */
  sb   t1, 0(t0)
```

__If Hart ID is 0:__

- Set Stack Pointer to the Idle Thread Stack

```text
  /* Set stack pointer to the idle thread stack */
  bnez a0, 1f
  la   sp, QEMU_RV_IDLESTACK_TOP
  j    2f
```

__If Hart ID is 1, 2, 3, ...__

- Validate the Hart ID (Must be less than number of CPUs)
- Compute the Stack Base Address based on `g_cpu_basestack` and Hart ID
- Set the Stack Pointer to the computed Stack Base Address

```text
1:
  /* Load the number of CPUs that the kernel supports */
#ifdef CONFIG_SMP
  li   t1, CONFIG_SMP_NCPUS
#else
  li   t1, 1
#endif

  /* If a0 (mhartid) >= t1 (the number of CPUs), stop here */
  blt  a0, t1, 3f
  csrw sie, zero
  /* Previously: csrw mie, zero */
  wfi

3:
  /* To get g_cpu_basestack[mhartid], must get g_cpu_basestack first */
  la   t0, g_cpu_basestack

  /* Offset = pointer width * hart id */
#ifdef CONFIG_ARCH_RV32
  slli t1, a0, 2
#else
  slli t1, a0, 3
#endif
  add  t0, t0, t1

  /* Load idle stack base to sp */
  REGLOAD sp, 0(t0)

  /*
   * sp (stack top) = sp + idle stack size - XCPTCONTEXT_SIZE
   *
   * Note: Reserve some space used by up_initial_state since we are already
   * running and using the per CPU idle stack.
   */
  li   t0, STACK_ALIGN_UP(CONFIG_IDLETHREAD_STACKSIZE - XCPTCONTEXT_SIZE)
  add  sp, sp, t0
```

__For All Hart IDs:__

- Disable Interrupts
- Load the Interrupt Vector Table
- Jump to `qemu_rv_start`

```
2:
  /* Disable all interrupts (i.e. timer, external) in mie */
  csrw  sie, zero
  /* Previously: csrw  mie, zero */

  /* Don't load the Interrupt Vector Table, use OpenSBI for crash logging */
  /* la   t0, __trap_vec */
  /* csrw stvec, t0 */
  /* Previously: csrw mtvec, t0 */

  /* Jump to qemu_rv_start */
  jal  x1, qemu_rv_start

  /* We shouldn't return from _start */
```

Note that we don't load the Interrupt Vector Table, because we'll use OpenSBI for crash logging. (Like when we hit M-Mode Instructions)

_What happens when we run this?_

Hart ID is now 0, which is correct...

```text
Starting kernel ...
clk u5_dw_i2c_clk_core already disabled
clk u5_dw_i2c_clk_apb already disabled
123067
```

But `qemu_rv_start` hangs. Why?

```text
  /* Print `7` */
  li  t0, 0x10000000
  li  t1, 0x37
  sb  t1, 0(t0)

  /* Jump to qemu_rv_start */
  jal  x1, qemu_rv_start
```

Let's trace `qemu_rv_start`...

# Boot from Network with U-Boot and TFTP

Read the article...

-   ["Star64 JH7110 RISC-V SBC: Boot from Network with U-Boot and TFTP"](https://lupyuen.github.io/articles/tftp)

We really should configure U-Boot Bootloader to load the Kernel Image over the network via [TFTP over UDP](https://en.wikipedia.org/wiki/Trivial_File_Transfer_Protocol). Because testing NuttX by swapping microSD Card is getting so tiresome.

Here's how...

![Boot from Network with U-Boot and TFTP](https://lupyuen.github.io/images/tftp-flow.jpg)

## Setup TFTP Server

First we set up a TFTP Server with [`tftpd`](https://crates.io/crates/tftpd)...

```bash
cargo install tftpd
mkdir $HOME/tftproot
sudo tftpd -i 0.0.0.0 -p 69 -d "$HOME/tftproot"
## `sudo` because port 69 is a privileged low port
```

([`tftp_server`](https://crates.io/crates/tftp_server) won't work, it only supports localhost)

We should see...

```text
Running TFTP Server on 0.0.0.0:69 in $HOME/tftproot
Sending a.txt to 127.0.0.1:57125
Sent a.txt to 127.0.0.1:57125
Sending a.txt to 192.168.x.x:33499
Sent a.txt to 192.168.x.x:33499
```

Let's test the TFTP Server...

```bash
echo Test123 >$HOME/tftproot/a.txt
curl -v tftp://127.0.0.1/a.txt
curl -v tftp://192.168.x.x/a.txt
```

(`localhost` won't work because of IPv6, I think)

We should see...

```text
$ curl -v tftp://192.168.x.x/a.txt
*   Trying 192.168.x.x:69...
* getpeername() failed with errno 107: Transport endpoint is not connected
* Connected to 192.168.x.x () port 69 (#0)
* getpeername() failed with errno 107: Transport endpoint is not connected
* set timeouts for state 0; Total  300000, retry 6 maxtry 50
* got option=(tsize) value=(8)
* tsize parsed from OACK (8)
* got option=(blksize) value=(512)
* blksize parsed from OACK (512) requested (512)
* got option=(timeout) value=(6)
* Connected for receive
* set timeouts for state 1; Total  0, retry 72 maxtry 50
Test123
* Closing connection 0
```

If it fails...

```text
$ curl -v tftp://192.168.x.x/a.txt
*   Trying 192.168.x.x:69...
* getpeername() failed with errno 107: Transport endpoint is not connected
* Connected to 192.168.x.x () port 69 (#0)
* getpeername() failed with errno 107: Transport endpoint is not connected
* set timeouts for state 0; Total  300000, retry 6 maxtry 50
```

In the olden days we would actually do this...

```text
$ tftp 127.0.0.1
tftp> get a.txt
Received 8 bytes in 0.0 seconds
tftp> quit
```

Just like FTP!

## Copy NuttX Image to TFTP Server

Next we copy the NuttX Image and Device Tree to the TFTP Folder...

```bash
## Copy the Device Tree from Armbian microSD
cp \
  /run/media/$USER/armbi_root/boot/dtb/starfive/jh7110-visionfive-v2.dtb \
  jh7110-star64-pine64.dtb

## Copy NuttX Binary Image and Device Tree to TFTP Folder
## `nuttx.bin` comes from here:
## https://github.com/lupyuen2/wip-pinephone-nuttx/releases/tag/star64-0.0.1
cp nuttx.bin $HOME/tftproot/Image
cp jh7110-star64-pine64.dtb $HOME/tftproot

## Test NuttX Binary Image and Device Tree over TFTP
curl -v tftp://192.168.x.x/Image
curl -v tftp://192.168.x.x/jh7110-star64-pine64.dtb

## We should see...
## Warning: Binary output can mess up your terminal. Use "--output -" to tell 
## Warning: curl to output it to your terminal anyway, or consider "--output 
## Warning: <FILE>" to save to a file.
```

## Test U-Boot with TFTP

Now we boot Star64 JH7110 SBC and test the TFTP Commands.

Connect Star64 SBC to the Ethernet wired network and power up.

Star64 fails to boot over the network (because we don't have a [BOOTP Server](https://en.wikipedia.org/wiki/Bootstrap_Protocol) or DHCP+TFTP Combo Server), but that's OK...

```text
ethernet@16030000 Waiting for PHY auto negotiation to complete....... done
BOOTP broadcast 1
*** Unhandled DHCP Option in OFFER/ACK: 43
*** Unhandled DHCP Option in OFFER/ACK: 43
DHCP client bound to address 192.168.x.x (351 ms)
Using ethernet@16030000 device
TFTP from server 192.168.x.x; our IP address is 192.168.x.x
Filename 'boot.scr.uimg'.
Load address: 0x43900000
Loading: *
TFTP server died; starting again
BOOTP broadcast 1
*** Unhandled DHCP Option in OFFER/ACK: 43
*** Unhandled DHCP Option in OFFER/ACK: 43
DHCP client bound to address 192.168.x.x (576 ms)
Using ethernet@16030000 device
TFTP from server 192.168.x.x; our IP address is 192.168.x.x
Filename 'boot.scr.uimg'.
Load address: 0x40200000
Loading: *
TFTP server died; starting again
StarFive #
```

[(Source)](https://github.com/lupyuen/nuttx-star64#u-boot-bootloader-log-for-tftp)

Run these commands...

```bash
## Set the TFTP Server IP
setenv tftp_server 192.168.x.x

## Load the NuttX Image from TFTP Server
## kernel_addr_r=0x40200000
## tftp_server=192.168.x.x
tftpboot ${kernel_addr_r} ${tftp_server}:Image

## Load the Device Tree from TFTP Server
## fdt_addr_r=0x46000000
## tftp_server=192.168.x.x
tftpboot ${fdt_addr_r} ${tftp_server}:jh7110-star64-pine64.dtb

## Set the RAM Address of Device Tree
## fdt_addr_r=0x46000000
fdt addr ${fdt_addr_r}

## Boot the NuttX Image with the Device Tree
## kernel_addr_r=0x40200000
## fdt_addr_r=0x46000000
booti ${kernel_addr_r} - ${fdt_addr_r}
```

[(Inspired by this article)](https://community.arm.com/oss-platforms/w/docs/495/tftp-remote-network-kernel-using-u-boot)

We should see...

```text
StarFive # setenv tftp_server 192.168.x.x

StarFive # tftpboot ${kernel_addr_r} ${tftp_server}:Image
Using ethernet@16030000 device
TFTP from server 192.168.x.x; our IP address is 192.168.x.x
Filename 'Image'.
Load address: 0x40200000
Loading: #############################################################T ####
#################################################################
#############
221.7 KiB/s
done
Bytes transferred = 2097832 (2002a8 hex)

StarFive # tftpboot ${fdt_addr_r} ${tftp_server}:jh7110-star64-pine64.dtb
Using ethernet@16030000 device
TFTP from server 192.168.x.x; our IP address is 192.168.x.x
Filename 'jh7110-star64-pine64.dtb'.
Load address: 0x46000000
Loading: ####
374 KiB/s
done
Bytes transferred = 50235 (c43b hex)

StarFive # fdt addr ${fdt_addr_r}

StarFive # booti ${kernel_addr_r} - ${fdt_addr_r}
## Flattened Device Tree blob at 46000000
   Booting using the fdt blob at 0x46000000
   Using Device Tree in place at 0000000046000000, end 000000004600f43a

Starting kernel ...

clk u5_dw_i2c_clk_core already disabled
clk u5_dw_i2c_clk_apb already disabled
123067DFAGHBC
```

[(Source)](https://github.com/lupyuen/nuttx-star64#u-boot-bootloader-log-for-tftp)

## Configure U-Boot for TFTP

Let's configure U-Boot so that it will boot from TFTP every time we power up!

```bash
## Remember the TFTP Server IP
setenv tftp_server 192.168.x.x
## Check that it's correct
printenv tftp_server
## Save it for future reboots
saveenv

## Add the Boot Command for TFTP
setenv bootcmd_tftp 'if tftpboot ${kernel_addr_r} ${tftp_server}:Image ; then if tftpboot ${fdt_addr_r} ${tftp_server}:jh7110-star64-pine64.dtb ; then if fdt addr ${fdt_addr_r} ; then booti ${kernel_addr_r} - ${fdt_addr_r} ; fi ; fi ; fi'
## Check that it's correct
printenv bootcmd_tftp
## Save it for future reboots
saveenv

## Test the Boot Command for TFTP
run bootcmd_tftp

## Remember the Original Boot Targets
setenv orig_boot_targets "$boot_targets"
## Should show `mmc0 dhcp`
printenv boot_targets
## Save it for future reboots
saveenv

## Add TFTP to the Boot Targets
setenv boot_targets "$boot_targets tftp"
## Should show `mmc0 dhcp  tftp`
printenv boot_targets
## Save it for future reboots
saveenv
```

`bootcmd_tftp` expands to...

```bash
## Load the NuttX Image from TFTP Server
## kernel_addr_r=0x40200000
## tftp_server=192.168.x.x
if tftpboot ${kernel_addr_r} ${tftp_server}:Image ;
then

  ## Load the Device Tree from TFTP Server
  ## fdt_addr_r=0x46000000
  if tftpboot ${fdt_addr_r} ${tftp_server}:jh7110-star64-pine64.dtb ;
  then

    ## Set the RAM Address of Device Tree
    ## fdt_addr_r=0x46000000
    if fdt addr ${fdt_addr_r} ;
    then

      ## Boot the NuttX Image with the Device Tree
      ## kernel_addr_r=0x40200000
      ## fdt_addr_r=0x46000000
      booti ${kernel_addr_r} - ${fdt_addr_r} ;
    fi ;
  fi ;
fi
```

[(From here)](https://community.arm.com/oss-platforms/w/docs/495/tftp-remote-network-kernel-using-u-boot) This is a persistent change, i.e. the device will boot via TFTP on every power up. To revert back to the default boot behaviour:

```bash
## Restore the Boot Targets
setenv boot_targets "$orig_boot_targets"
## Should show `mmc0 dhcp`
printenv boot_targets
## Save it for future reboots
saveenv
```

With Network Boot running, we're now ready for __Automated Testing of Apache NuttX RTOS__ on Star64 SBC!

Though we might need a __Smart Power Plug__ to power-cycle our SBC: [__IKEA TRÅDFRI__](https://www.ikea.com/sg/en/p/tradfri-control-outlet-kit-smart-10364797/) and [__DIRIGERA__](https://www.ikea.com/sg/en/p/dirigera-hub-for-smart-products-white-smart-50503409/) via [__Home Assistant API__](https://gist.github.com/lupyuen/01cff0d4ca225984ca8fd0d999d7c76d) (pic below)

![Home Assistant controls Google Home (and potentially Smart Plugs)](https://lupyuen.github.io/images/tftp-home.png)

## U-Boot Commands for Network Boot

_How does it work?_

`bootcmd` is now...

```text
bootcmd=run load_vf2_env;run importbootenv;run load_distro_uenv;run boot2;run distro_bootcmd

load_vf2_env=fatload mmc ${bootpart} ${loadaddr} ${testenv}

importbootenv=echo Importing environment from mmc${devnum} ...; env import -t ${loadaddr} ${filesize}

load_distro_uenv=fatload mmc ${fatbootpart} ${distroloadaddr} ${bootdir}/${bootenv}; env import ${distroloadaddr} 17c; 

boot2 not defined, comes from `boot/vf2_uEnv.txt`
```

`bootcmd` calls `distro_bootcmd`, which runs `bootcmd_mmc0` and `bootcmd_dhcp`...

```text
distro_bootcmd=for target in ${boot_targets}; do run bootcmd_${target}; done

boot_targets=mmc0 dhcp 

bootcmd_mmc0=devnum=0; run mmc_boot

bootcmd_distro=run fdt_loaddtb; run fdt_sizecheck; run set_fdt_distro; sysboot mmc ${fatbootpart} fat c0000000 ${bootdir}/${boot_syslinux_conf}; 
```

`bootcmd_dhcp` is...

```text
bootcmd_dhcp=devtype=dhcp; if dhcp ${scriptaddr} ${boot_script_dhcp}; then source ${scriptaddr}; fi;setenv efi_fdtfile ${fdtfile}; setenv efi_old_vci ${bootp_vci};setenv efi_old_arch ${bootp_arch};setenv bootp_vci PXEClient:Arch:00027:UNDI:003000;setenv bootp_arch 0x1b;if dhcp ${kernel_addr_r}; then tftpboot ${fdt_addr_r} dtb/${efi_fdtfile};if fdt addr ${fdt_addr_r}; then bootefi ${kernel_addr_r} ${fdt_addr_r}; else bootefi ${kernel_addr_r} ${fdtcontroladdr};fi;fi;setenv bootp_vci ${efi_old_vci};setenv bootp_arch ${efi_old_arch};setenv efi_fdtfile;setenv efi_old_arch;setenv efi_old_vci;
```

Which expands to...

```bash
devtype=dhcp

## Load the Boot Script from DHCP+TFTP Server
## scriptaddr=0x43900000
## boot_script_dhcp=boot.scr.uimg
if dhcp ${scriptaddr} ${boot_script_dhcp}
then
  source ${scriptaddr}
fi

## Set the EFI Variables
## fdtfile=starfive/starfive_visionfive2.dtb
setenv efi_fdtfile ${fdtfile}
setenv efi_old_vci ${bootp_vci}
setenv efi_old_arch ${bootp_arch}
setenv bootp_vci PXEClient:Arch:00027:UNDI:003000
setenv bootp_arch 0x1b

## Load the Kernel Image from DHCP+TFTP Server...
## kernel_addr_r=0x40200000
if dhcp ${kernel_addr_r}
then

  ## Load the Device Tree from the DHCP+TFTP Server
  ## fdt_addr_r=0x46000000
  ## efi_fdtfile=starfive/starfive_visionfive2.dtb
  tftpboot ${fdt_addr_r} dtb/${efi_fdtfile}

  ## Set the RAM Address of Device Tree
  ## fdt_addr_r=0x46000000
  if fdt addr ${fdt_addr_r}
  then

    ## Boot the EFI Kernel Image
    ## fdt_addr_r=0x46000000
    bootefi ${kernel_addr_r} ${fdt_addr_r}
  else

    ## Boot the EFI Kernel Image
    ## fdtcontroladdr=fffc6aa0
    bootefi ${kernel_addr_r} ${fdtcontroladdr}
  fi
fi

## Unset the EFI Variables
setenv bootp_vci ${efi_old_vci}
setenv bootp_arch ${efi_old_arch}
setenv efi_fdtfile
setenv efi_old_arch
setenv efi_old_vci
```

`dhcp` command is...

```text
dhcp - boot image via network using DHCP/TFTP protocol

Usage:
dhcp [loadAddress] [[hostIPaddr:]bootfilename]
```

(Assume [DHCP/TFTP](https://www.emcraft.com/som/using-dhcp) is not used)

`tftpboot` command is...

```text
tftpboot - boot image via network using TFTP protocol

Usage:
tftpboot [loadAddress] [[hostIPaddr:]bootfilename]
```

`fdt` command is...

```text
fdt - flattened device tree utility commands

Usage:
fdt addr [-c]  <addr> [<length>]   - Set the [control] fdt location to <addr>
fdt apply <addr>                    - Apply overlay to the DT
fdt move   <fdt> <newaddr> <length> - Copy the fdt to <addr> and make it active
fdt resize [<extrasize>]            - Resize fdt to size + padding to 4k addr + some optional <extrasize> if needed
fdt print  <path> [<prop>]          - Recursive print starting at <path>
fdt list   <path> [<prop>]          - Print one level starting at <path>
fdt get value <var> <path> <prop>   - Get <property> and store in <var>
fdt get name <var> <path> <index>   - Get name of node <index> and store in <var>
fdt get addr <var> <path> <prop>    - Get start address of <property> and store in <var>
fdt get size <var> <path> [<prop>]  - Get size of [<property>] or num nodes and store in <var>
fdt set    <path> <prop> [<val>]    - Set <property> [to <val>]
fdt mknode <path> <node>            - Create a new node after <path>
fdt rm     <path> [<prop>]          - Delete the node or <property>
fdt header [get <var> <member>]     - Display header info
                                      get - get header member <member> and store it in <var>
fdt bootcpu <id>                    - Set boot cpuid
fdt memory <addr> <size>            - Add/Update memory node
fdt rsvmem print                    - Show current mem reserves
fdt rsvmem add <addr> <size>        - Add a mem reserve
fdt rsvmem delete <index>           - Delete a mem reserves
fdt chosen [<start> <end>]          - Add/update the /chosen branch in the tree
                                        <start>/<end> - initrd start/end addr
NOTE: Dereference aliases by omitting the leading '/', e.g. fdt print ethernet0.
```

`booti` command is...

```text
booti - boot Linux kernel 'Image' format from memory

Usage:
booti [addr [initrd[:size]] [fdt]]
    - boot Linux flat or compressed 'Image' stored at 'addr'
        The argument 'initrd' is optional and specifies the address
        of an initrd in memory. The optional parameter ':size' allows
        specifying the size of a RAW initrd.
        Currently only booting from gz, bz2, lzma and lz4 compression
        types are supported. In order to boot from any of these compressed
        images, user have to set kernel_comp_addr_r and kernel_comp_size environment
        variables beforehand.
        Since booting a Linux kernel requires a flat device-tree, a
        third argument providing the address of the device-tree blob
        is required. To boot a kernel with a device-tree blob but
        without an initrd image, use a '-' for the initrd argument.
```

`bootefi` command is...

```text
bootefi - Boots an EFI payload from memory

Usage:
bootefi <image address> [fdt address]
  - boot EFI payload stored at address <image address>.
    If specified, the device tree located at <fdt address> gets
    exposed as EFI configuration table.
bootefi bootmgr [fdt address]
  - load and boot EFI payload based on BootOrder/BootXXXX variables.

    If specified, the device tree located at <fdt address> gets
    exposed as EFI configuration table.
```

Doesn't work for NuttX...

```text
StarFive # bootefi ${kernel_addr_r} ${fdt_addr_r}
Card did not respond to voltage select! : -110
Card did not respond to voltage select! : -110
No EFI system partition
No UEFI binary known at 0x40200000
```

[`autoload`](https://u-boot.readthedocs.io/en/latest/usage/environment.html) setting is...

```text
autoload:
if set to “no” (any string beginning with ‘n’), “bootp” and “dhcp” will just load perform a lookup of the configuration from the BOOTP server, but not try to load any image.
```

# Hang in Enter Critical Section

Read the article...

-   ["Star64 JH7110 + NuttX RTOS: RISC-V Privilege Levels and UART Registers"](https://lupyuen.github.io/articles/privilege)

NuttX on Star64 JH7110 hangs when entering Critical Section...

From [uart_16550.c](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64/drivers/serial/uart_16550.c#L1713-L1737):

```c
int up_putc(int ch)
{
  FAR struct u16550_s *priv = (FAR struct u16550_s *)CONSOLE_DEV.priv;
  irqstate_t flags;

  /* All interrupts must be disabled to prevent re-entrancy and to prevent
   * interrupts from firing in the serial driver code.
   */

  //// This will hang!
  flags = enter_critical_section();
  ...
  u16550_putc(priv, ch);
  leave_critical_section(flags);
  return ch;
}
```

Which assembles to...

```text
int up_putc(int ch)
{
  ...
up_irq_save():
nuttx/include/arch/irq.h:675
  __asm__ __volatile__
    40204598:  47a1                  li  a5,8
    4020459a:  3007b7f3            csrrc  a5,mstatus,a5
up_putc():
nuttx/drivers/serial/uart_16550.c:1726
  flags = enter_critical_section();
```

But `mstatus` is not accessible at Supervisor Level! Let's trace this.

[`enter_critical_section`](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64/include/nuttx/irq.h#L156-L191) calls [`up_irq_save`](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64/arch/risc-v/include/irq.h#L660-L689)...

```c
// Disable interrupts and return the previous value of the mstatus register
static inline irqstate_t up_irq_save(void)
{
  irqstate_t flags;

  /* Read mstatus & clear machine interrupt enable (MIE) in mstatus */

  __asm__ __volatile__
    (
      "csrrc %0, " __XSTR(CSR_STATUS) ", %1\n"
      : "=r" (flags)
      : "r"(STATUS_IE)
      : "memory"
    );

  /* Return the previous mstatus value so that it can be restored with
   * up_irq_restore().
   */

  return flags;
}
```

`CSR_STATUS` is defined in [mode.h](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64/arch/risc-v/include/mode.h#L35-L103):

```c
#ifdef CONFIG_ARCH_USE_S_MODE
#  define CSR_STATUS        sstatus          /* Global status register */
#else
#  define CSR_STATUS        mstatus          /* Global status register */
#endif
```

So we need to set [CONFIG_ARCH_USE_S_MODE](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64/arch/risc-v/Kconfig#L278-L296).

Which is defined in Kernel Mode: [`rv-virt:knsh64`](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64/boards/risc-v/qemu-rv/rv-virt/configs/knsh64/defconfig). So we change Build Config to...

```bash
tools/configure.sh rv-virt:knsh64
```

And we bypassed Machine Mode Initialisation during startup...

From [qemu_rv_start.c](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64a/arch/risc-v/src/qemu-rv/qemu_rv_start.c#L166-L231)

```c
void qemu_rv_start(int mhartid)
{
  // Clear BSS
  DEBUGASSERT(mhartid == 0);
  if (0 == mhartid) { qemu_rv_clear_bss(); }

  // Bypass to S-Mode Init
  qemu_rv_start_s(mhartid);

  // Skip M-Mode Init
  // TODO: What about `satp`, `stvec`, `pmpaddr0`, `pmpcfg0`?
  ...
}
```

grep for `csr` in `nuttx.S` shows that no more M-Mode Registers are used.

Now Critical Section is OK yay!

```text
Starting kernel ...
clk u5_dw_i2c_clk_core already disabled
clk u5_dw_i2c_clk_apb already disabled
123067DFAGHBCIcd
```

- [See the __Build Steps__](https://github.com/lupyuen2/wip-pinephone-nuttx/releases/tag/star64-0.0.1)

- [See the __Modified Files__](https://github.com/lupyuen2/wip-pinephone-nuttx/pull/31/files)

- [See the __Build Outputs__](https://github.com/lupyuen2/wip-pinephone-nuttx/releases/tag/star64-0.0.1)

_What about `satp`, `stvec`, `pmpaddr0`, `pmpcfg0`?_

We'll handle them in a while.

Sometimes we see this...

```text
Starting kernel ...
clk u5_dw_i2c_clk_core already disabled
clk u5_dw_i2c_clk_apb already disabled
123067DFAGHBCUnhandled exception: Store/AMO access fault
EPC: 0000000040200628 RA: 00000000402004ba TVAL: ffffff8000008000
EPC: ffffffff804ba628 RA: ffffffff804ba4ba reloc adjusted

SP:  0000000040406a30 GP:  00000000ff735e00 TP:  0000000000000001
T0:  0000000010000000 T1:  0000000000000037 T2:  ffffffffffffffff
S0:  0000000040400000 S1:  0000000000000200 A0:  0000000000000003
A1:  0000080000008000 A2:  0000000010100000 A3:  0000000040400000
A4:  0000000000000026 A5:  0000000000000000 A6:  00000000101000e7
A7:  0000000000000000 S2:  0000080000008000 S3:  0000000040600000
S4:  0000000040400000 S5:  0000000000000000 S6:  0000000000000026
S7:  00fffffffffff000 S8:  0000000040404000 S9:  0000000000001000
S10: 0000000040400ab0 S11: 0000000000200000 T3:  0000000000000023
T4:  000000004600f43a T5:  000000004600d000 T6:  000000004600cfff

Code: 879b 0277 d7b3 00f6 f793 1ff7 078e 95be (b023 0105)
```

Which fails at...

```text
nuttx/arch/risc-v/src/common/riscv_mmu.c:101
  lntable[index] = (paddr | mmuflags);
    40200620:  1ff7f793            andi  a5,a5,511
    40200624:  078e                  slli  a5,a5,0x3
    40200626:  95be                  add  a1,a1,a5
    40200628:  0105b023            sd  a6,0(a1)  /* Fails Here */
mmu_invalidate_tlb_by_vaddr():
nuttx/arch/risc-v/src/common/riscv_mmu.h:237
  __asm__ __volatile__
    4020062c:  12d00073            sfence.vma  zero,a3
    40200630:  8082                  ret
```

TODO: Trace this Store/AMO Access Fault

# Hang in UART Transmit

Read the article...

-   ["Star64 JH7110 + NuttX RTOS: RISC-V Privilege Levels and UART Registers"](https://lupyuen.github.io/articles/privilege)

When printing to UART Port, the UART Transmit hangs while waiting for UART Transmit Ready...

From [uart_16550.c](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64/drivers/serial/uart_16550.c#L1638-L1642)

```c
static void u16550_putc(FAR struct u16550_s *priv, int ch)
{
  //// This will hang!
  while ((u16550_serialin(priv, UART_LSR_OFFSET) & UART_LSR_THRE) == 0);
  u16550_serialout(priv, UART_THR_OFFSET, (uart_datawidth_t)ch);
}
```

Where [`u16550_serialin`](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64a/drivers/serial/uart_16550.c#L596-L611) is defined as...

```c
*((FAR volatile uart_datawidth_t *)priv->uartbase + offset);
```

And [`UART_THR_OFFSET`](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64a/include/nuttx/serial/uart_16550.h#L197) is...

```c
#define UART_LSR_OFFSET        (CONFIG_16550_REGINCR*UART_LSR_INCR)
```

`CONFIG_16550_REGINCR` is 1...

```text
→ grep 16550 .config
CONFIG_16550_REGINCR=1
CONFIG_16550_REGWIDTH=8
CONFIG_16550_ADDRWIDTH=0
```

As defined according to the Default Config for 16550: [Kconfig-16550](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64a/drivers/serial/Kconfig-16550#L501-L520):

```text
config 16550_REGINCR
  int "Address increment between 16550 registers"
  default 1
  ---help---
    The address increment between 16550 registers.  Options are 1, 2, or 4.
    Default: 1

config 16550_REGWIDTH
  int "Bit width of 16550 registers"
  default 8
  ---help---
    The bit width of registers.  Options are 8, 16, or 32. Default: 8

config 16550_ADDRWIDTH
  int "Address width of 16550 registers"
  default 8
  ---help---
    The bit width of registers.  Options are 0, 8, 16, or 32.
    Default: 8
    Note: 0 means auto detect address size (uintptr_t)
```

_But is CONFIG_16550_REGINCR correct for Star64 JH7110?_

Let's check the official Linux Driver. According to [JH7110 Linux Device Tree](https://doc-en.rvspace.org/VisionFive2/DG_UART/JH7110_SDK/general_uart_controller.html)...

```text
reg = <0x0 0x10000000 0x0 0xl0000>;
reg-io-width = <4>;
reg-shift = <2>;
```

`reg-shift` is 2.

And from the Linux 8250 Driver: [8250_dw.c](https://github.com/torvalds/linux/blob/master/drivers/tty/serial/8250/8250_dw.c#L159-L169)

```text
static void dw8250_serial_out(struct uart_port *p, int offset, int value)
{
  struct dw8250_data *d = to_dw8250_data(p->private_data);

  writeb(value, p->membase + (offset << p->regshift));

  if (offset == UART_LCR && !d->uart_16550_compatible)
    dw8250_check_lcr(p, value);
}
```

We see that the UART Offset is shifted by 2 (`regshift`). Which means we multiply the UART Offset by 4.

Thus `CONFIG_16550_REGINCR` should be 4, not 1!

_How to fix CONFIG_16550_REGINCR?_

We fix the NuttX Configuration: Device Drivers > Serial Driver Support > 16550 UART Chip support > Address increment between 16550 registers

And change it from 1 to 4: [knsh64/defconfig](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64a/boards/risc-v/qemu-rv/rv-virt/configs/knsh64/defconfig#L11)

```text
CONFIG_16550_REGINCR=4
```

Now UART Transmit doesn't hang yay!

```text
Starting kernel ...
clk u5_dw_i2c_clk_core already disabled
clk u5_dw_i2c_clk_apb already disabled
123067DFm45DTpAqGaclbHm45DTpBqm45DTpCqI
```

NuttX now hangs somewhere in `nx_start`

Let's log the NuttX Scheduler...

# Enable Scheduler Logging

Scheduler Logging in NuttX seems to have changed recently. To enable Scheduler Logging...

- `make menuconfig`

- Disable this setting: Device Drivers > System Logging > Prepend timestamp to syslog message

- Enable these settings: Build Setup > Debug Options > Scheduler Debug Features > Scheduler Error, Warnings and Info Output

- Also enable: Build Setup > Debug Options > Binary Loader Debug Features > Binary Loader Error, Warnings and Info Output

After enabling Scheduler Logging and Binary Loader Logging, we see...

```text
123067DFAGaclbHBCqemu_rv_kernel_mappings: map I/O regions
qemu_rv_kernel_mappings: map kernel text
qemu_rv_kernel_mappings: map kernel data
qemu_rv_kernel_mappings: connect the L1 and L2 page tables
qemu_rv_kernel_mappings: map the page pool
qemu_rv_mm_init: mmu_enable: satp=1077956608
Inx_start: Entry
elf_initialize: Registering ELF
uart_register: Registering /dev/console
uart_register: Registering /dev/ttyS0
work_start_lowpri: Starting low-priority kernel worker thread(s)
nx_start_application: Starting init task: /system/bin/init
load_absmodule: Loading /system/bin/init
elf_loadbinary: Loading file: /system/bin/init
elf_init: filename: /system/bin/init loadinfo: 0x404069e8
```

_What is `/system/bin/init`?_

We'll find out in a while...

[Compare with QEMU Kernel Mode Run Log](https://gist.github.com/lupyuen/6888376da6561bdc060c2459dffdef01)

[See the QEMU Kernel Mode Build Log](https://gist.github.com/lupyuen/dce0cdbbf4a4bdf9c79e617b3fe1b679)

# Initialise RISC-V Supervisor Mode

Read the article...

-   ["Star64 JH7110 + NuttX RTOS: RISC-V Privilege Levels and UART Registers"](https://lupyuen.github.io/articles/privilege)

Earlier we bypassed the Machine Mode and Supervisor Mode Initialisation during NuttX startup...

From [qemu_rv_start.c](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64a/arch/risc-v/src/qemu-rv/qemu_rv_start.c#L166-L231)

```c
void qemu_rv_start(int mhartid)
{
  // Clear BSS
  DEBUGASSERT(mhartid == 0);
  if (0 == mhartid) { qemu_rv_clear_bss(); }

  // Bypass to S-Mode Init
  qemu_rv_start_s(mhartid);

  // Skip M-Mode Init
  // TODO: What about `satp`, `stvec`, `pmpaddr0`, `pmpcfg0`?
  ...
}
```

Now we restore the Supervisor Mode Initialisation, commenting out the Machine Mode Initialisation...

From [qemu_rv_start.c](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64a/arch/risc-v/src/qemu-rv/qemu_rv_start.c#L165-L233):

```c
void qemu_rv_start(int mhartid)
{
  DEBUGASSERT(mhartid == 0); //

  /* NOTE: still in M-mode */

  if (0 == mhartid)
    {
      qemu_rv_clear_bss();

      /* Initialize the per CPU areas */

      riscv_percpu_add_hart(mhartid);
    }

  /* Disable MMU and enable PMP */

  WRITE_CSR(satp, 0x0);
  //WRITE_CSR(pmpaddr0, 0x3fffffffffffffull);
  //WRITE_CSR(pmpcfg0, 0xf);

  /* Set exception and interrupt delegation for S-mode */

  //WRITE_CSR(medeleg, 0xffff);
  //WRITE_CSR(mideleg, 0xffff);

  /* Allow to write satp from S-mode */

  //CLEAR_CSR(mstatus, MSTATUS_TVM);

  /* Set mstatus to S-mode and enable SUM */

  //CLEAR_CSR(mstatus, ~MSTATUS_MPP_MASK);
  //SET_CSR(mstatus, MSTATUS_MPPS | SSTATUS_SUM);

  /* Set the trap vector for S-mode */

  WRITE_CSR(stvec, (uintptr_t)__trap_vec);

  /* Set the trap vector for M-mode */

  //WRITE_CSR(mtvec, (uintptr_t)__trap_vec_m);

  if (0 == mhartid)
    {
      /* Only the primary CPU needs to initialize mtimer
       * before entering to S-mode
       */

      // TODO
      //up_mtimer_initialize();
    }

  /* Set mepc to the entry */

  //WRITE_CSR(mepc, (uintptr_t)qemu_rv_start_s);

  /* Set a0 to mhartid explicitly and enter to S-mode */

  //asm volatile (
  //    "mv a0, %0 \n"
  //    "mret \n"
  //    :: "r" (mhartid)
  //);

  // Jump to S-Mode Init ourselves
  qemu_rv_start_s(mhartid); //
}
```

TODO: Port [__up_mtimer_initialize__](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64a/arch/risc-v/src/qemu-rv/qemu_rv_timerisr.c#L151-L210) to Star64

Now NuttX boots further!

```text
123067DFHBCqemu_rv_kernel_mappings: map I/O regions
qemu_rv_kernel_mappings: map kernel text
qemu_rv_kernel_mappings: map kernel data
qemu_rv_kernel_mappings: connect the L1 and L2 page tables
qemu_rv_kernel_mappings: map the page pool
qemu_rv_mm_init: mmu_enable: satp=1077956608
Inx_start: Entry
elf_initialize: Registering ELF
uart_register: Registering /dev/console
uart_register: Registering /dev/ttyS0
work_start_lowpri: Starting low-priority kernel worker thread(s)
nx_start_application: Starting init task: /system/bin/init
load_absmodule: Loading /system/bin/init
elf_loadbinary: Loading file: /system/bin/init
elf_init: filename: /system/bin/init loadinfo: 0x404069e8
riscv_exception: EXCEPTION: Breakpoint. MCAUSE: 0000000000000003, EPC: 0000000040200434, MTVAL: 0000000000000000
riscv_exception: PANIC!!! Exception = 0000000000000003
_assert: Current Version: NuttX  12.0.3 2261b80-dirty Jul 15 2023 20:38:57 risc-v
_assert: Assertion failed panic: at file: common/riscv_exception.c:85 task: Idle Task 0x40200ce6
up_dump_register: EPC: 0000000040200434
up_dump_register: A0: 0000000000000001 A1: 0000000040406778 A2: 0000000000000000 A3: 0000000000000001
up_dump_register: A4: 0000000000000000 A5: 00000000404067e0 A6: 0000000000000074 A7: fffffffffffffff8
up_dump_register: T0: 0000000000000030 T1: 0000000000000007 T2: 0000000000000020 T3: 0000000040406aa0
up_dump_register: T4: 0000000040406a98 T5: 00000000000001ff T6: 000000000000002d
up_dump_register: S0: 0000000000000000 S1: 0000000040406968 S2: 0000000040408720 S3: 0000000000000000
up_dump_register: S4: 0000000000000000 S5: 0000000000000000 S6: 0000000000000000 S7: 0000000000000000
up_dump_register: S8: 00000000fff47194 S9: 0000000000000000 S10: 0000000000000000 S11: 0000000000000000
up_dump_register: SP: 0000000040406760 FP: 0000000000000000 TP: 0000000000000001 RA: 0000000040213e24
dump_stack: User Stack:
dump_stack:   base: 0x40406030
dump_stack:   size: 00003024
dump_stack:     sp: 0x40406760
stack_dump: 0x40406760: 00000000 00000000 40213e6a 00000000 fff47194 00000000 404067d0 00000000
stack_dump: 0x40406780: 00000001 00000000 00000010 00000000 00000000 00000000 40213ffc 00000000
stack_dump: 0x404067a0: 40408720 00000000 40406968 00000000 00000000 00000000 4020c7ec 00000000
stack_dump: 0x404067c0: 00000800 00000000 40219f30 00000000 612f2e2e 2f737070 2f6e6962 74696e69
stack_dump: 0x404067e0: 00000a00 00000000 00000000 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x40406800: fff47194 00000000 00000000 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x40406820: 00000000 00000000 00000000 00000000 40219f28 00000000 404069e8 00000000
stack_dump: 0x40406840: 40219f28 00000000 40212bde 00000000 40227776 00000000 40406870 00000000
stack_dump: 0x40406860: 00000000 00000000 fffffffc ffffffff 40219f28 00000000 404069e8 00000000
stack_dump: 0x40406880: 40400170 00000000 40204fea 00000000 0000006c 00000000 404069e8 00000000
stack_dump: 0x404068a0: 40400170 00000000 402050ae 00000000 40406908 00000000 40208f66 00000000
stack_dump: 0x404068c0: 40406908 00000000 4020c8c6 00000000 40219f28 00000000 404086d0 00000000
stack_dump: 0x404068e0: ffffffda ffffffff 40215be6 00000000 40406968 00000000 00000001 00000000
stack_dump: 0x40406900: 40400b28 00000000 40219f30 00000000 404086d0 00000000 40407e30 00000000
stack_dump: 0x40406920: 40407370 00000000 40219f30 00000000 00000000 00000000 40219f01 00000000
stack_dump: 0x40406940: 404069e8 00000000 404069e8 00000000 40219f28 00000000 4020dfdc 00000000
stack_dump: 0x40406960: 40219f28 00000000 40205ede 00000000 fff47194 00000000 404069b0 00000000
stack_dump: 0x40406980: 00000000 00000000 40205efe 00000000 00000000 00000000 404069b0 00000000
stack_dump: 0x404069a0: 40408830 00000000 4020d88c 00000000 40226bc0 00000000 40219f28 00000000
stack_dump: 0x404069c0: 40408830 00000000 00000000 00000000 40219f28 00000000 4020d894 00000000
stack_dump: 0x404069e0: 40406a18 00000000 00000000 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x40406a00: 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x40406a20: 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x40406a40: 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x40406a60: 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x40406a80: 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x40406aa0: 402277d0 00000000 40219f28 00000000 40408830 00000000 404001f8 00000000
stack_dump: 0x40406ac0: fffffffe ffffffff 4020eb36 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x40406ae0: 40406b60 00000000 40406b68 00000000 40219f28 00000000 40408830 00000000
stack_dump: 0x40406b00: 00000c00 00000000 4020d38a 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x40406b20: 00000000 00000000 fffda848 00000000 fffffff3 ffffffff 40400b18 00000000
stack_dump: 0x40406b40: 4040177c 00000000 00000064 00000000 00000c00 00000000 40200ff4 00000000
stack_dump: 0x40406b60: 00000000 00000000 40016400 00000000 00000000 00000000 00000c00 00000000
stack_dump: 0x40406b80: 4040177c 00000000 40401780 00000000 40400b28 00000000 40200ee6 00000000
stack_dump: 0x40406ba0: 40600000 00000000 00400000 00000000 00000026 00000000 00000003 00000000
stack_dump: 0x40406bc0: fff47194 00000000 ffff1428 00000000 10000000 00000000 40200514 00000000
stack_dump: 0x40406be0: 00000400 00000000 40200552 00000000 40000000 00000000 402000de 00000000
dump_tasks:    PID GROUP PRI POLICY   TYPE    NPX STATE   EVENT      SIGMASK          STACKBASE  STACKSIZE      USED   FILLED    COMMAND
dump_tasks:   ----   --- --- -------- ------- --- ------- ---------- -------- 0x404002b0      2048      1160    56.6%    irq
dump_task:       0     0   0 FIFO     Kthread N-- Running            0000000000000000 0x40406030      3024      1448    47.8%    Idle Task
dump_task:       1     1 100 RR       Kthread --- Waiting Unlock     0000000000000000 0x4040a060      1952       264    13.5%    lpwork 0x404013e0
```

But NuttX crashes. Let's find out why...

# QEMU Semihosting in NuttX

Read the article...

-   ["Star64 JH7110 + NuttX RTOS: RISC-V Semihosting and Initial RAM Disk"](https://lupyuen.github.io/articles/semihost)

NuttX crashes while booting on Star64 JH7110 SBC. From the Crash Dump above, [`mcause`](https://five-embeddev.com/riscv-isa-manual/latest/machine.html#sec:mcause) is 3: "Machine Software Interrupt".

Exception Program Counter `0x4020` `0434` is in RISC-V Semihosting `smh_call`...

```text
0000000040200430 <smh_call>:
smh_call():
nuttx/arch/risc-v/src/common/riscv_semihost.S:37
  .global smh_call
  .type smh_call @function

smh_call:

  slli zero, zero, 0x1f
    40200430:  01f01013            slli  zero,zero,0x1f
nuttx/arch/risc-v/src/common/riscv_semihost.S:38
  ebreak
    //// Crashes here (Trigger semihosting breakpoint)
    40200434:  00100073            ebreak
nuttx/arch/risc-v/src/common/riscv_semihost.S:39
  srai zero, zero, 0x7
    40200438:  40705013            srai  zero,zero,0x7
nuttx/arch/risc-v/src/common/riscv_semihost.S:40
  ret
    4020043c:  00008067            ret
    40200440:  0000                  unimp
```

When we log `smh_call`...

```text
host_call: nbr=0x1, parm=0x40406778, size=24
```

[host_call](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64a/arch/risc-v/src/common/riscv_hostfs.c#L35-L73) says that the Semihosting Call is for HOST_OPEN. (Open a file)

So NuttX crashes on Star64 because it's trying to read `/system/bin/init` via Semihosting!

(See next section)

Let's disable Semihosting and replace by Initial RAM Disk and ROMFS.

(See https://github.com/apache/nuttx/issues/9501)

![QEMU reads the Apps Filesystem over Semihosting](https://lupyuen.github.io/images/semihost-qemu.jpg)

Here's the Crash Dump after we disabled Semihosting...

```text
123067DFHBCqemu_rv_kernel_mappings: map I/O regions
qemu_rv_kernel_mappings: map kernel text
qemu_rv_kernel_mappings: map kernel data
qemu_rv_kernel_mappings: connect the L1 and L2 page tables
qemu_rv_kernel_mappings: map the page pool
qemu_rv_mm_init: mmu_enable: satp=1077956608
Inx_start: Entry
elf_initialize: Registering ELF
uart_register: Registering /dev/console
uart_register: Registering /dev/ttyS0
work_start_lowpri: Starting low-priority kernel worker thread(s)
nx_start_application: Starting init task: /system/bin/init
load_absmodule: Loading /system/bin/init
elf_loadbinary: Loading file: /system/bin/init
elf_init: filename: /system/bin/init loadinfo: 0x404069e8
host_call: nbr=0x1, parm=0x40406788, size=24
_assert: Current Version: NuttX  12.0.3 6ed2880-dirty Jul 15 2023 21:00:59 risc-v
_assert: Assertion failed panic: at file: common/riscv_hostfs.c:58 task: Idle Task 0x40200cd0
up_dump_register: EPC: 000000004020f590
up_dump_register: A0: 0000000040401630 A1: 000000000000003a A2: 0000000040219ee8 A3: 0000000000000000
up_dump_register: A4: 000000000000000a A5: 0000000000000000 A6: 0000000000000009 A7: 0000000000000068
up_dump_register: T0: 0000000000000030 T1: 0000000000000009 T2: 0000000000000020 T3: 000000000000002a
up_dump_register: T4: 000000000000002e T5: 00000000000001ff T6: 000000000000002d
up_dump_register: S0: 0000000000000000 S1: 0000000040400b28 S2: 0000000040401768 S3: 0000000040219ee8
up_dump_register: S4: 0000000040229b10 S5: 000000000000003a S6: 0000000000000000 S7: 0000000000000000
up_dump_register: S8: 00000000fff47194 S9: 0000000000000000 S10: 0000000000000000 S11: 0000000000000000
up_dump_register: SP: 0000000040406650 FP: 0000000000000000 TP: 0000000000000001 RA: 000000004020f590
dump_stack: User Stack:
dump_stack:   base: 0x40406030
dump_stack:   size: 00003024
dump_stack:     sp: 0x40406650
stack_dump: 0x40406640: 40406650 00000000 4020f688 00000000 00000000 00000000 40212bc8 00000000
stack_dump: 0x40406660: deadbeef deadbeef 40406680 00000000 deadbeef deadbeef 7474754e 00000058
stack_dump: 0x40406680: 404066b8 00000000 00000001 00000000 40406788 00000000 40205cc0 00000000
stack_dump: 0x404066a0: 00000074 00000000 fffffff8 2e323100 00332e30 00000000 40229ae8 00000000
stack_dump: 0x404066c0: 65366708 38383264 69642d30 20797472 206c754a 32203531 20333230 303a3132
stack_dump: 0x404066e0: 39353a30 00000000 0000000a 00000000 00000000 73697200 00762d63 00000000
stack_dump: 0x40406700: ffff9fef ffffffff 40406740 00000000 fff47194 00000000 00000000 00000000
stack_dump: 0x40406720: 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x40406740: 40408720 00000000 40406968 00000000 00000000 00000000 40204e80 00000000
stack_dump: 0x40406760: 00000074 00000000 40213e3c 00000000 fff47194 00000000 40213e64 00000000
stack_dump: 0x40406780: 00000000 00000000 404067d0 00000000 00000001 00000000 00000010 00000000
stack_dump: 0x404067a0: 40408720 00000000 40213f7e 00000000 00000000 00000000 4020c7d6 00000000
stack_dump: 0x404067c0: 00000800 00000000 40219e70 00000000 612f2e2e 2f737070 2f6e6962 74696e69
stack_dump: 0x404067e0: 00000a00 00000000 00000000 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x40406800: fff47194 00000000 00000000 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x40406820: 00000000 00000000 00000000 00000000 40219e68 00000000 404069e8 00000000
stack_dump: 0x40406840: 40219e68 00000000 40212bc8 00000000 402276b6 00000000 40406870 00000000
stack_dump: 0x40406860: 00000000 00000000 fffffffc ffffffff 40219e68 00000000 404069e8 00000000
stack_dump: 0x40406880: 40400170 00000000 40204fd4 00000000 0000006c 00000000 404069e8 00000000
stack_dump: 0x404068a0: 40400170 00000000 40205098 00000000 40406908 00000000 40208f50 00000000
stack_dump: 0x404068c0: 40406908 00000000 4020c8b0 00000000 40219e68 00000000 404086d0 00000000
stack_dump: 0x404068e0: ffffffda ffffffff 40215b2a 00000000 40406968 00000000 00000001 00000000
stack_dump: 0x40406900: 40400b28 00000000 40219e70 00000000 404086d0 00000000 40407e30 00000000
stack_dump: 0x40406920: 40407370 00000000 40219e70 00000000 00000000 00000000 40219e01 00000000
stack_dump: 0x40406940: 404069e8 00000000 404069e8 00000000 40219e68 00000000 4020dfc6 00000000
stack_dump: 0x40406960: 40219e68 00000000 40205ec8 00000000 fff47194 00000000 404069b0 00000000
stack_dump: 0x40406980: 00000000 00000000 40205ee8 00000000 00000000 00000000 404069b0 00000000
stack_dump: 0x404069a0: 40408830 00000000 4020d876 00000000 40226b00 00000000 40219e68 00000000
stack_dump: 0x404069c0: 40408830 00000000 00000000 00000000 40219e68 00000000 4020d87e 00000000
stack_dump: 0x404069e0: 40406a18 00000000 00000000 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x40406a00: 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x40406a20: 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x40406a40: 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x40406a60: 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x40406a80: 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x40406aa0: 40227710 00000000 40219e68 00000000 40408830 00000000 404001f8 00000000
stack_dump: 0x40406ac0: fffffffe ffffffff 4020eb20 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x40406ae0: 40406b60 00000000 40406b68 00000000 40219e68 00000000 40408830 00000000
stack_dump: 0x40406b00: 00000c00 00000000 4020d374 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x40406b20: 00000000 00000000 fffda848 00000000 fffffff3 ffffffff 40400b18 00000000
stack_dump: 0x40406b40: 4040177c 00000000 00000064 00000000 00000c00 00000000 40200fde 00000000
stack_dump: 0x40406b60: 00000000 00000000 40016400 00000000 00000000 00000000 00000c00 00000000
stack_dump: 0x40406b80: 4040177c 00000000 40401780 00000000 40400b28 00000000 40200ed0 00000000
stack_dump: 0x40406ba0: 40600000 00000000 00400000 00000000 00000026 00000000 00000003 00000000
stack_dump: 0x40406bc0: fff47194 00000000 ffff1428 00000000 10000000 00000000 402004fe 00000000
stack_dump: 0x40406be0: 00000400 00000000 4020053c 00000000 00000000 00000000 402000de 00000000
dump_tasks:    PID GROUP PRI POLICY   TYPE    NPX STATE   EVENT      SIGMASK          STACKBASE  STACKSIZE      USED   FILLED    COMMAND
dump_tasks:   ----   --- --- -------- ------- --- ------- ---------- -------- 0x404002b0      2048         0     0.0%    irq
dump_task:       0     0   0 FIFO     Kthread N-- Running            0000000000000000 0x40406030      3024      2248    74.3%    Idle Task
dump_task:       1     1 100 RR       Kthread --- Waiting Unlock     0000000000000000 0x4040a060      1952       264    13.5%    lpwork 0x404013e0
```

# NuttX Apps Filesystem

Read the article...

-   ["Star64 JH7110 + NuttX RTOS: RISC-V Semihosting and Initial RAM Disk"](https://lupyuen.github.io/articles/semihost)

_Where is `/system/bin/init`? Why is it loaded by NuttX over Semihosting?_

`/system/bin/init` is needed for starting the NuttX Shell (and NuttX Apps) on Star64 JH7110 SBC.

We see it in the NuttX Build Configuration...

```text
→ grep INIT .config
CONFIG_INIT_FILE=y
CONFIG_INIT_ARGS=""
CONFIG_INIT_STACKSIZE=3072
CONFIG_INIT_PRIORITY=100
CONFIG_INIT_FILEPATH="/system/bin/init"
CONFIG_INIT_MOUNT=y
CONFIG_INIT_MOUNT_SOURCE=""
CONFIG_INIT_MOUNT_TARGET="/system"
CONFIG_INIT_MOUNT_FSTYPE="hostfs"
CONFIG_INIT_MOUNT_FLAGS=0x1
CONFIG_INIT_MOUNT_DATA="fs=../apps"
CONFIG_PATH_INITIAL="/system/bin"
CONFIG_NSH_ARCHINIT=y
```

Which says that `../apps` is mounted as `/system`, via Semihosting HostFS.

That's how `/system/bin/init` gets loaded over Semihosting...

```
→ ls ../apps/bin       
getprime hello    init     sh
```

![QEMU reads the Apps Filesystem over Semihosting](https://lupyuen.github.io/images/semihost-qemu.jpg)

We traced the Semihosting Calls in QEMU Kernel Mode, here's what we observed...

[QEMU Kernel Mode Run Log](https://gist.github.com/lupyuen/6888376da6561bdc060c2459dffdef01)

```text
nx_start_application: Starting init task: /system/bin/init
load_absmodule: Loading /system/bin/init
elf_loadbinary: Loading file: /system/bin/init
elf_init: filename: /system/bin/init loadinfo: 0x802069e8
hostfs_open: relpath=bin/init, oflags=0x1, mode=0x1b6
...
NuttShell (NSH) NuttX-12.2.1-RC0
nsh> nx_start: CPU0: Beginning Idle Loop

nsh> 
nsh> uname -a
posix_spawn: pid=0xc0202978 path=uname file_actions=0xc0202980 attr=0xc0202988 argv=0xc0202a28
hostfs_stat: relpath=bin/uname
host_call: nbr=0x1, parm=0x80208fe0, size=24
exec_spawn: ERROR: Failed to load program 'uname': -2
nxposix_spawn_exec: ERROR: exec failed: 2
NuttX 12.2.1-RC0 cafbbb1 Jul 15 2023 16:55:00 risc-v rv-virt
nsh> 
nsh> ls /
posix_spawn: pid=0xc0202978 path=ls file_actions=0xc0202980 attr=0xc0202988 argv=0xc0202a28
hostfs_stat: relpath=bin/ls
host_call: nbr=0x1, parm=0x80208fe0, size=24
exec_spawn: ERROR: Failed to load program 'ls': -2
nxposix_spawn_exec: ERROR: exec failed: 2
/:
 dev/
 proc/
 system/
nsh> 
nsh> ls /system
posix_spawn: pid=0xc0202978 path=ls file_actions=0xc0202980 attr=0xc0202988 argv=0xc0202a28
hostfs_stat: relpath=bin/ls
host_call: nbr=0x1, parm=0x80208fe0, size=24
exec_spawn: ERROR: Failed to load program 'ls': -2
nxposix_spawn_exec: ERROR: exec failed: 2
hostfs_stat: relpath=
host_call: nbr=0x1, parm=0x80209180, size=24
host_call: nbr=0xc, parm=0x80209180, size=8
host_call: nbr=0x2, parm=0x80209190, size=8
 /system
nsh> 
nsh> ls /system/bin
posix_spawn: pid=0xc0202978 path=ls file_actions=0xc0202980 attr=0xc0202988 argv=0xc0202a28
hostfs_stat: relpath=bin/ls
host_call: nbr=0x1, parm=0x80208fe0, size=24
exec_spawn: ERROR: Failed to load program 'ls': -2
nxposix_spawn_exec: ERROR: exec failed: 2
hostfs_stat: relpath=bin
host_call: nbr=0x1, parm=0x80209180, size=24
host_call: nbr=0xc, parm=0x80209180, size=8
host_call: nbr=0x2, parm=0x80209190, size=8
 /system/bin
nsh> 
nsh> ls /system/bin/init
posix_spawn: pid=0xc0202978 path=ls file_actions=0xc0202980 attr=0xc0202988 argv=0xc0202a28
hostfs_stat: relpath=bin/ls
host_call: nbr=0x1, parm=0x80208fe0, size=24
exec_spawn: ERROR: Failed to load program 'ls': -2
nxposix_spawn_exec: ERROR: exec failed: 2
hostfs_stat: relpath=bin/init
host_call: nbr=0x1, parm=0x80209180, size=24
host_call: nbr=0xc, parm=0x80209180, size=8
host_call: nbr=0x2, parm=0x80209190, size=8
 /system/bin/init
```

Semihosting won't work on Star64 SBC. Let's replace this with Initial RAM Disk and ROMFS...

(See https://github.com/apache/nuttx/issues/9501)

# Initial RAM Disk for LiteX Arty-A7

Read the article...

-   ["Star64 JH7110 + NuttX RTOS: RISC-V Semihosting and Initial RAM Disk"](https://lupyuen.github.io/articles/semihost)

Let's modify NuttX for QEMU to mount the Apps Filesystem from an Initial RAM Disk (instead of Semihosting).

(So later we can replicate this on Star64 JH7110 SBC)

First we look at the Initial RAM Disk for LiteX Arty-A7...

[(About NuttX RAM Disks and ROM Disks)](https://cwiki.apache.org/confluence/plugins/servlet/mobile?contentId=139629548#content/view/139629548)

To generate the RAM Disk, we run this command: [VexRISCV_SMP Core](https://nuttx.apache.org/docs/latest/platforms/risc-v/litex/cores/vexriscv_smp/index.html)

```bash
cd nuttx
genromfs -f romfs.img -d ../apps/bin -V "NuttXBootVol"
```

[(About `genromfs`)](https://www.systutorials.com/docs/linux/man/8-genromfs/)

LiteX Memory Map says where the RAM Disk is loaded...

```text
"romfs.img":   "0x40C00000",
"nuttx.bin":   "0x40000000",
"opensbi.bin": "0x40f00000"
```

This is the LiteX Build Configuration for mounting the RAM Disk: [knsh/defconfig](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64/boards/risc-v/litex/arty_a7/configs/knsh/defconfig#L34)

```bash
CONFIG_BOARDCTL_ROMDISK=y
CONFIG_BOARD_LATE_INITIALIZE=y
CONFIG_BUILD_KERNEL=y
CONFIG_FS_ROMFS=y
CONFIG_INIT_FILEPATH="/system/bin/init"
CONFIG_INIT_MOUNT=y
CONFIG_INIT_MOUNT_FLAGS=0x1
CONFIG_INIT_MOUNT_TARGET="/system/bin"
CONFIG_LITEX_APPLICATION_RAMDISK=y
CONFIG_NSH_FILE_APPS=y
CONFIG_NSH_READLINE=y
CONFIG_PATH_INITIAL="/system/bin"
CONFIG_RAM_SIZE=4194304
CONFIG_RAM_START=0x40400000
CONFIG_RAW_BINARY=y
CONFIG_SYSTEM_NSH_PROGNAME="init"
CONFIG_TESTING_GETPRIME=y
```

According to [NSH Start-Up Script](https://nuttx.apache.org/docs/latest/applications/nsh/nsh.html#nsh-start-up-script):

```text
CONFIG_DISABLE_MOUNTPOINT not set
CONFIG_FS_ROMFS enabled
```

The RAM Disk is mounted at LiteX Startup: [litex_appinit.c](https://github.com/apache/nuttx/blob/master/boards/risc-v/litex/arty_a7/src/litex_appinit.c#L76-L103)

```c
void board_late_initialize(void)
{
  #ifdef CONFIG_LITEX_APPLICATION_RAMDISK
  litex_mount_ramdisk();
  #endif

  litex_bringup();
}
```

`litex_bringup` mounts the RAM Disk at startup: [litex_ramdisk.c](https://github.com/apache/nuttx/blob/master/boards/risc-v/litex/arty_a7/src/litex_ramdisk.c#L41-L98)

```c
#ifndef CONFIG_BUILD_KERNEL
#error "Ramdisk usage is intended to be used with kernel build only"
#endif

#define SECTORSIZE   512
#define NSECTORS(b)  (((b) + SECTORSIZE - 1) / SECTORSIZE)
#define RAMDISK_DEVICE_MINOR 0

// Mount a ramdisk defined in the ld-kernel.script to /dev/ramX.
// The ramdisk is intended to contain a romfs with applications which can
// be spawned at runtime.
int litex_mount_ramdisk(void)
{
  int ret;
  struct boardioc_romdisk_s desc;

  desc.minor    = RAMDISK_DEVICE_MINOR;
  desc.nsectors = NSECTORS((ssize_t)__ramdisk_size);
  desc.sectsize = SECTORSIZE;
  desc.image    = __ramdisk_start;

  ret = boardctl(BOARDIOC_ROMDISK, (uintptr_t)&desc);
  if (ret < 0)
    {
      syslog(LOG_ERR, "Ramdisk register failed: %s\n", strerror(errno));
      syslog(LOG_ERR, "Ramdisk mountpoint /dev/ram%d\n",
                                          RAMDISK_DEVICE_MINOR);
      syslog(LOG_ERR, "Ramdisk length %u, origin %x\n",
                                          (ssize_t)__ramdisk_size,
                                          (uintptr_t)__ramdisk_start);
    }

  return ret;
}
```

`__ramdisk_start` is defined in [board_memorymap.h](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64b/boards/risc-v/litex/arty_a7/include/board_memorymap.h#L58-L91):

```c
/* RAMDisk */
#define RAMDISK_START     (uintptr_t)__ramdisk_start
#define RAMDISK_SIZE      (uintptr_t)__ramdisk_size

/* ramdisk (RW) */
extern uint8_t          __ramdisk_start[];
extern uint8_t          __ramdisk_size[];
```

And [ld-kernel.script](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64b/boards/risc-v/litex/arty_a7/scripts/ld-kernel.script#L20-L49):

```text
MEMORY
{
  kflash (rx)   : ORIGIN = 0x40000000, LENGTH = 4096K   /* w/ cache */
  ksram (rwx)   : ORIGIN = 0x40400000, LENGTH = 4096K   /* w/ cache */
  pgram (rwx)   : ORIGIN = 0x40800000, LENGTH = 4096K   /* w/ cache */
  ramdisk (rwx) : ORIGIN = 0x40C00000, LENGTH = 4096K   /* w/ cache */
}
...
/* Page heap */
__pgheap_start = ORIGIN(pgram);
__pgheap_size = LENGTH(pgram) + LENGTH(ramdisk);

/* Application ramdisk */
__ramdisk_start = ORIGIN(ramdisk);
__ramdisk_size = LENGTH(ramdisk);
__ramdisk_end  = ORIGIN(ramdisk) + LENGTH(ramdisk);
```

Note that `__pgheap_size` needs to include `ramdisk`.

Let's do the same to NuttX for QEMU...

# Modify NuttX QEMU to Load Initial RAM Disk

Read the article...

-   ["Star64 JH7110 + NuttX RTOS: RISC-V Semihosting and Initial RAM Disk"](https://lupyuen.github.io/articles/semihost)

Now we can modify NuttX for QEMU to mount the Apps Filesystem from an Initial RAM Disk instead of Semihosting.

(So later we can replicate this on Star64 JH7110 SBC)

![NuttX for QEMU will mount the Apps Filesystem from an Initial RAM Disk](https://lupyuen.github.io/images/semihost-qemu2.jpg)

We follow the steps from LiteX Arty-A7 (from the previous section)...

We build NuttX QEMU in Kernel Mode: [Build Steps](https://github.com/lupyuen2/wip-pinephone-nuttx/tree/master/boards/risc-v/qemu-rv/rv-virt)

```bash
## Build NuttX QEMU Kernel Mode
./tools/configure.sh rv-virt:knsh64 
make V=1 -j7

## Build Apps Filesystem
make export V=1
pushd ../apps
./tools/mkimport.sh -z -x ../nuttx/nuttx-export-*.tar.gz
make import V=1
popd
```

We generate the Initial RAM Disk `initrd`...

```bash
cd nuttx
genromfs -f initrd -d ../apps/bin -V "NuttXBootVol"
```

[(About `genromfs`)](https://www.systutorials.com/docs/linux/man/8-genromfs/)

Initial RAM Disk `initrd` is 7.9 MB...

```text
→ ls -l initrd
-rw-r--r--  1 7902208 Jul 21 13:41 initrd
```

This is how we load the Initial RAM Disk on QEMU: [‘virt’ Generic Virtual Platform (virt)](https://www.qemu.org/docs/master/system/riscv/virt.html#running-linux-kernel)

```bash
qemu-system-riscv64 \
  -semihosting \
  -M virt,aclint=on \
  -cpu rv64 \
  -smp 8 \
  -bios none \
  -kernel nuttx \
  -initrd initrd \
  -nographic
```

_What is the RAM Address of the Initial RAM Disk in QEMU?_

Initial RAM Disk is loaded by QEMU at `0x8400` `0000`...

- ["RAM Disk Address for RISC-V QEMU"](https://github.com/lupyuen/nuttx-star64#ram-disk-address-for-risc-v-qemu)

Below are the files that we changed in NuttX for QEMU to load the Initial RAM Disk (instead of Semihosting)...

- [Modified Files for QEMU with Initial RAM Disk](https://github.com/lupyuen2/wip-pinephone-nuttx/pull/33/files)

We configured QEMU to mount the RAM Disk as ROMFS (instead of Semihosting): [knsh64/defconfig](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/ramdisk/boards/risc-v/qemu-rv/rv-virt/configs/knsh64/defconfig)

```bash
CONFIG_BOARDCTL_ROMDISK=y
CONFIG_BOARD_LATE_INITIALIZE=y
CONFIG_FS_ROMFS=y
CONFIG_INIT_FILEPATH="/system/bin/init"
CONFIG_INIT_MOUNT=y
CONFIG_INIT_MOUNT_FLAGS=0x1
CONFIG_INIT_MOUNT_TARGET="/system/bin"

## We removed these...
## CONFIG_FS_HOSTFS=y
## CONFIG_RISCV_SEMIHOSTING_HOSTFS=y
```

We defined the RAM Disk Memory in the Linker Script: [ld-kernel64.script](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/ramdisk/boards/risc-v/qemu-rv/rv-virt/scripts/ld-kernel64.script#L20-L54)

```text
MEMORY
{
  ...
  /* Added RAM Disk */
  ramdisk (rwx) : ORIGIN = 0x80800000, LENGTH = 16M   /* w/ cache */

  /* This won't work, crashes with a Memory Mgmt Fault...
     ramdisk (rwx) : ORIGIN = 0x84000000, LENGTH = 16M */   /* w/ cache */
}

/* Added RAM Disk */
/* Page heap */

__pgheap_start = ORIGIN(pgram);
__pgheap_size = LENGTH(pgram) + LENGTH(ramdisk);
/* Previously: __pgheap_size = LENGTH(pgram); */

/* Added RAM Disk */
/* Application ramdisk */

__ramdisk_start = ORIGIN(ramdisk);
__ramdisk_size = LENGTH(ramdisk);
__ramdisk_end  = ORIGIN(ramdisk) + LENGTH(ramdisk);
```

(We increased RAM Disk Memory from 4 MB to 16 MB because our RAM Disk is now bigger)

At Startup, we mount the RAM Disk: [qemu_rv_appinit.c](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/ramdisk/boards/risc-v/qemu-rv/rv-virt/src/qemu_rv_appinit.c#L83C1-L179C2)

```c
// Called at NuttX Startup
void board_late_initialize(void) {
  // Mount the RAM Disk
  mount_ramdisk();

  /* Perform board-specific initialization */
#ifdef CONFIG_NSH_ARCHINIT
  mount(NULL, "/proc", "procfs", 0, NULL);
#endif
}

// Mount the RAM Disk
int mount_ramdisk(void) {
  int ret;
  struct boardioc_romdisk_s desc;

  desc.minor    = RAMDISK_DEVICE_MINOR;
  desc.nsectors = NSECTORS((ssize_t)__ramdisk_size);
  desc.sectsize = SECTORSIZE;
  desc.image    = __ramdisk_start;

  ret = boardctl(BOARDIOC_ROMDISK, (uintptr_t)&desc);
  if (ret < 0)
    {
      syslog(LOG_ERR, "Ramdisk register failed: %s\n", strerror(errno));
      syslog(LOG_ERR, "Ramdisk mountpoint /dev/ram%d\n",
                                          RAMDISK_DEVICE_MINOR);
      syslog(LOG_ERR, "Ramdisk length %lu, origin %lx\n",
                                          (ssize_t)__ramdisk_size,
                                          (uintptr_t)__ramdisk_start);
    }

  return ret;
}
```

We copied the RAM Disk from the QEMU Address (0x84000000) to the NuttX Address (__ramdisk_start): [qemu_rv_mm_init.c](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/ramdisk/arch/risc-v/src/qemu-rv/qemu_rv_mm_init.c#L271-L280)

```c
void qemu_rv_kernel_mappings(void) {
  ...
  // Copy 0x84000000 to __ramdisk_start (__ramdisk_size bytes)
  // TODO: RAM Disk must not exceed __ramdisk_size bytes
  memcpy((void *)__ramdisk_start, (void *)0x84000000, (size_t)__ramdisk_size);
```

[(Because somehow `map_region` crashes when we try to map 0x84000000)](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/ramdisk/arch/risc-v/src/qemu-rv/qemu_rv_mm_init.c#L280-L287)

We check that the RAM Disk Memory is sufficient: [fs_romfsutil.c](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/ramdisk/fs/romfs/fs_romfsutil.c#L85-L105)

```c
static uint32_t romfs_devread32(struct romfs_mountpt_s *rm, int ndx) {
  //// Stop if RAM Disk Memory is too small
  DEBUGASSERT(&rm->rm_buffer[ndx] < __ramdisk_start + (size_t)__ramdisk_size); ////
```

Before making the above changes, here's the log for QEMU Kernel Mode with Semihosting...

```text
+ genromfs -f initrd -d ../apps/bin -V NuttXBootVol
+ riscv64-unknown-elf-size nuttx
   text    data     bss     dec     hex filename
 171581     673   21872  194126   2f64e nuttx
+ riscv64-unknown-elf-objcopy -O binary nuttx nuttx.bin
+ cp .config nuttx.config
+ riscv64-unknown-elf-objdump -t -S --demangle --line-numbers --wide nuttx
+ sleep 10
+ qemu-system-riscv64 -semihosting -M virt,aclint=on -cpu rv64 -smp 8 -bios none -kernel nuttx -initrd initrd -nographic
ABCnx_start: Entry
uart_register: Registering /dev/console
uart_register: Registering /dev/ttyS0
work_start_lowpri: Starting low-priority kernel worker thread(s)
nx_start_application: Starting init task: /system/bin/init
hostfs_stat: relpath=bin/init
hostfs_open: relpath=bin/init, oflags=0x1, mode=0x1b6
elf_symname: Symbol has no name
elf_symvalue: SHN_UNDEF: Failed to get symbol name: -3
elf_relocateadd: Section 2 reloc 2: Undefined symbol[0] has no name: -3

NuttShell (NSH) NuttX-12.0.3
nsh> nx_start: CPU0: Beginning Idle Loop
```

Now we run QEMU Kernel Mode with Initial RAM Disk, without Semihosting...

And it boots OK on QEMU yay!

[See the Run Log](https://gist.github.com/lupyuen/8afee5b07b61bb7f9f202f7f8c5e3ab3)

# Modify NuttX Star64 to Load Initial RAM Disk

Read the article...

-   ["Star64 JH7110 + NuttX RTOS: RISC-V Semihosting and Initial RAM Disk"](https://lupyuen.github.io/articles/semihost)

Finally we can modify NuttX for Star64 JH7110 RISC-V SBC to mount the Apps Filesystem from an Initial RAM Disk. (Instead of Semihosting)

![NuttX for Star64 JH7110 RISC-V SBC will mount the Apps Filesystem from an Initial RAM Disk](https://lupyuen.github.io/images/semihost-star64.jpg)

We follow the steps from QEMU Kernel Mode's Initial RAM Disk. (See previous section)

We build NuttX Star64 in Kernel Mode: [Build Steps](https://github.com/lupyuen2/wip-pinephone-nuttx/tree/master/boards/risc-v/qemu-rv/rv-virt)

```bash
## Build NuttX Star64 in Kernel Mode
tools/configure.sh rv-virt:knsh64
make V=1 -j7

## Build Apps Filesystem
make export V=1
pushd ../apps
./tools/mkimport.sh -z -x ../nuttx/nuttx-export-*.tar.gz
make import V=1
popd
```

We generate the Initial RAM Disk `initrd` and copy to TFTP Folder (for Network Booting)...

```bash
## Generate Initial RAM Disk
cd nuttx
genromfs -f initrd -d ../apps/bin -V "NuttXBootVol"

## Copy NuttX Binary Image, Device Tree and Initial RAM Disk to TFTP Folder
cp nuttx.bin $HOME/tftproot/Image
cp ../jh7110-star64-pine64.dtb $HOME/tftproot
cp initrd $HOME/tftproot
```

[(About `genromfs`)](https://www.systutorials.com/docs/linux/man/8-genromfs/)

Initial RAM Disk `initrd` is 7.9 MB...

```text
→ ls -l initrd
-rw-r--r--  1 7930880 Jul 21 13:41 initrd
```

Below are the files that we changed in NuttX for Star64 to load the Initial RAM Disk (instead of Semihosting)...

- [Modified Files for Initial RAM Disk on Star64](https://github.com/lupyuen2/wip-pinephone-nuttx/pull/34/files)

These are the same changes that we made earlier for QEMU Kernel Mode's Initial RAM Disk.

(For a detailed explanation of the modified files, see the previous section)

Note that we copy the Initial RAM Disk from `0x4610` `0000` (instead of QEMU's `0x8400` `0000`): [qemu_rv_mm_init.c](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64c/arch/risc-v/src/qemu-rv/qemu_rv_mm_init.c#L271-L280)

```c
// Copy 0x46100000 to __ramdisk_start (__ramdisk_size bytes)
// TODO: RAM Disk must not exceed __ramdisk_size bytes
memcpy((void *)__ramdisk_start, (void *)0x46100000, (size_t)__ramdisk_size);
```

(Why `0x4610` `0000`? See `ramdisk_addr_r` below)

This is how we updated the NuttX Build Configuration in `make menuconfig`...

- Board Selection > Enable boardctl() interface > Enable application space creation of ROM disks

- RTOS Features > RTOS hooks > Custom board late initialization   

- File Systems > ROMFS file system 

- RTOS Features > Tasks and Scheduling > Auto-mount init file system 

  Set to `/system/bin`

- Build Setup > Debug Options > File System Debug Features > File System Error, Warnings and Info Output

- Disable: File Systems > Host File System   

- Manually delete from [`knsh64/defconfig`](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64c/boards/risc-v/qemu-rv/rv-virt/configs/knsh64/defconfig)...

  ```text
  CONFIG_HOST_MACOS=y
  CONFIG_INIT_MOUNT_DATA="fs=../apps"
  CONFIG_INIT_MOUNT_FSTYPE="hostfs"
  CONFIG_INIT_MOUNT_SOURCE=""
  ```

Updated Build Configuration: [knsh64/defconfig](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64c/boards/risc-v/qemu-rv/rv-virt/configs/knsh64/defconfig)

_What is the RAM Address of the Initial RAM Disk in Star64?_

Initial RAM Disk is loaded by Star64's U-Boot Bootloader at `0x4610` `0000`...

```bash
ramdisk_addr_r=0x46100000
```

[(Source)](https://lupyuen.github.io/articles/linux#u-boot-settings-for-star64)

Which means that we need to add these TFTP Commands to U-Boot Bootloader...

```bash
## Assume Initial RAM Disk is max 16 MB
setenv ramdisk_size 0x1000000
## Check that it's correct
printenv ramdisk_size
## Save it for future reboots
saveenv

## Load Kernel and Device Tree over TFTP
tftpboot ${kernel_addr_r} ${tftp_server}:Image
tftpboot ${fdt_addr_r} ${tftp_server}:jh7110-star64-pine64.dtb
fdt addr ${fdt_addr_r}

## Added this: Load Initial RAM Disk over TFTP
tftpboot ${ramdisk_addr_r} ${tftp_server}:initrd

## Changed this: Replaced `-` by `ramdisk_addr_r:ramdisk_size`
booti ${kernel_addr_r} ${ramdisk_addr_r}:${ramdisk_size} ${fdt_addr_r}
```

Which will change our U-Boot Boot Script to...

```bash
## Load the NuttX Image from TFTP Server
## kernel_addr_r=0x40200000
## tftp_server=192.168.x.x
if tftpboot ${kernel_addr_r} ${tftp_server}:Image;
then

  ## Load the Device Tree from TFTP Server
  ## fdt_addr_r=0x46000000
  if tftpboot ${fdt_addr_r} ${tftp_server}:jh7110-star64-pine64.dtb;
  then

    ## Set the RAM Address of Device Tree
    ## fdt_addr_r=0x46000000
    if fdt addr ${fdt_addr_r};
    then

      ## Load the Intial RAM Disk from TFTP Server
      ## ramdisk_addr_r=0x46100000
      if tftpboot ${ramdisk_addr_r} ${tftp_server}:initrd;
      then

        ## Boot the NuttX Image with the Initial RAM Disk and Device Tree
        ## kernel_addr_r=0x40200000
        ## ramdisk_addr_r=0x46100000
        ## ramdisk_size=0x1000000
        ## fdt_addr_r=0x46000000
        booti ${kernel_addr_r} ${ramdisk_addr_r}:${ramdisk_size} ${fdt_addr_r};
      fi;
    fi;
  fi;
fi
```

Which becomes...

```bash
## Assume Initial RAM Disk is max 16 MB
setenv ramdisk_size 0x1000000
## Check that it's correct
printenv ramdisk_size
## Save it for future reboots
saveenv

## Add the Boot Command for TFTP
setenv bootcmd_tftp 'if tftpboot ${kernel_addr_r} ${tftp_server}:Image ; then if tftpboot ${fdt_addr_r} ${tftp_server}:jh7110-star64-pine64.dtb ; then if fdt addr ${fdt_addr_r} ; then if tftpboot ${ramdisk_addr_r} ${tftp_server}:initrd ; then booti ${kernel_addr_r} ${ramdisk_addr_r}:${ramdisk_size} ${fdt_addr_r} ; fi ; fi ; fi ; fi'
## Check that it's correct
printenv bootcmd_tftp
## Save it for future reboots
saveenv
```

_What happens if we omit the RAM Disk Size?_

```text
$ booti ${kernel_addr_r} ${ramdisk_addr_r} ${fdt_addr_r}
Wrong Ramdisk Image Format
Ramdisk image is corrupt or invalid

## Assume max 16 MB
$ booti ${kernel_addr_r} ${ramdisk_addr_r}:0x1000000 ${fdt_addr_r}
## Boots OK
```

_Does the Initial RAM Disk work on Star64?_

Star64 JH7110 boots OK with the Initial RAM Disk yay!

```text
StarFive # booti ${kernel_addr_r} ${ramdisk_addr_r}:0x1000000 ${fdt_addr_r}
## Flattened Device Tree blob at 46000000
   Booting using the fdt blob at 0x46000000
   Using Device Tree in place at 0000000046000000, end 000000004600f43a

Starting kernel ...

clk u5_dw_i2c_clk_core already disabled
clk u5_dw_i2c_clk_apb already disabled
123067DFHBCInx_start: Entry
uart_register: Registering /dev/console
uart_register: Registering /dev/ttyS0
work_start_lowpri: Starting low-priority kernel worker thread(s)
board_late_initialize: 
nx_start_application: Starting init task: /system/bin/init
elf_symname: Symbol has no name
elf_symvalue: SHN_UNDEF: Failed to get symbol name: -3
elf_relocateadd: Section 2 reloc 2: Undefined symbol[0] has no name: -3
nx_start_application: ret=3
up_exit: TCB=0x404088d0 exiting
nx_start: CPU0: Beginning Idle Loop
```

TODO: Why no shell?

TODO: Why `nx_start_application: ret=3`?

TODO: Check User Address Space

TODO: Boot from MicroSD with Initial RAM Disk

# No UART Output from NuttX Shell

Read the article...

-   ["Star64 JH7110 + NuttX RTOS: RISC-V PLIC Interrupts and Serial I/O"](https://lupyuen.github.io/articles/plic)

From the previous section, we found out that NuttX Shell didn't appear on Star64 JH7110 SBC.

When we log [`uart_write`](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/ramdisk2/drivers/serial/serial.c#L1172-L1341), we see that the NuttX Shell is actually started!

```text
uart_write (0xc000a610):
0000  0a 4e 75 74 74 53 68 65 6c 6c 20 28 4e 53 48 29  .NuttShell (NSH)
0010  20 4e 75 74 74 58 2d 31 32 2e 30 2e 33 0a         NuttX-12.0.3.  

uart_write (0xc0015338):
0000  6e 73 68 3e 20                                   nsh>            

uart_write (0xc0015310):
0000  1b 5b 4b                                         .[K             
```

Just that the NuttX Shell couldn't produce any UART Output.

(This happens to all NuttX Apps, but not to NuttX Kernel)

Let's find out why, by tracing the UART Output in NuttX QEMU...

# UART Output in NuttX QEMU

Read the article...

-   ["Star64 JH7110 + NuttX RTOS: RISC-V PLIC Interrupts and Serial I/O"](https://lupyuen.github.io/articles/plic)

To understand how UART Output (`printf`) works in NuttX Apps (and NuttX Shell), we add logs to NuttX QEMU...

```text
ABCnx_start: Entry
up_irq_enable: 
up_enable_irq: irq=17
up_enable_irq: RISCV_IRQ_SOFT=17
uart_register: Registering /dev/console
uart_register: Registering /dev/ttyS0
up_enable_irq: irq=35
up_enable_irq: extirq=10, RISCV_IRQ_EXT=25
work_start_lowpri: Starting low-priority kernel worker thread(s)
board_late_initialize: 
nx_start_application: Starting init task: /system/bin/init
elf_symname: Symbol has no name
elf_symvalue: SHN_UNDEF: Failed to get symbol name: -3
elf_relocateadd: Section 2 reloc 2: Undefined symbol[0] has no name: -3
up_exit: TCB=0x802088d0 exiting
$%&riscv_doirq: irq=8
$%&riscv_doirq: irq=8
$%&riscv_doirq: irq=8
...
$%&riscv_doirq: irq=8
$%&riscv_doirq: irq=8
$%&riscv_doirq: irq=8
uart_write (0xc0200428):
0000  2a 2a 2a 6d 61 69 6e 0a                          ***main.        
FAAAAAAAADEF*F*F*FmFaFiFnF
$%&riscv_doirq: irq=8
$%&riscv_doirq: irq=8
$%&riscv_doirq: irq=8
...
$%&riscv_doirq: irq=8
$%&riscv_doirq: irq=8
$%&riscv_doirq: irq=8
uart_write (0xc000a610):
0000  0a 4e 75 74 74 53 68 65 6c 6c 20 28 4e 53 48 29  .NuttShell (NSH)
0010  20 4e 75 74 74 58 2d 31 32 2e 30 2e 33 0a         NuttX-12.0.3.  
FAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADEF
FNFuFtFtFSFhFeFlFlF F(FNFSFHF)F FNFuFtFtFXF-F1F2F.F0F.F3F
$%&riscv_doirq: irq=8
uart_write (0xc0015340):
0000  6e 73 68 3e 20                                   nsh>            
AAAAADEFnFsFhF>F $%&riscv_doirq: irq=8
uart_write (0xc0015318):
0000  1b 5b 4b                                         .[K             
AAADEF[FK$%&riscv_doirq: irq=8
nx_start: CPU0: Beginning Idle Loop
$%^&riscv_doirq: irq=35
#*ADEFa$%&riscv_doirq: irq=8
$%^&riscv_doirq: irq=35
#*ADEFa$%&riscv_doirq: irq=8
$%^&riscv_doirq: irq=35
#*ADEFa$%&riscv_doirq: irq=8
```

This says that NuttX Apps call [`uart_write`](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/ramdisk2/drivers/serial/serial.c#L1172-L1341), which calls...

- `A`: [`uart_putxmitchar`](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/ramdisk2/drivers/serial/serial.c#L150-L286) which calls...

- `D`: [`uart_xmitchars`](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/ramdisk2/drivers/serial/serial_io.c#L42-L107) which calls...

- `E`: [`uart_txready`](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/ramdisk2/drivers/serial/serial_io.c#L63-L68) and...

  `F`: [`u16550_send`](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/ramdisk2/drivers/serial/uart_16550.c#L1542-L1556)
  
When we type something, the UART Input will trigger an Interrupt...

(Also for NuttX Apps calling a System Function in NuttX Kernel)

- `$`: [`exception_common`](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/ramdisk2/arch/risc-v/src/common/riscv_exception_common.S#L63-L189) calls...

- `%^&`: [`riscv_dispatch_irq`](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/ramdisk2/arch/risc-v/src/qemu-rv/qemu_rv_irq_dispatch.c#L51-L92) which calls...

- [`riscv_doirq`](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/ramdisk2/arch/risc-v/src/common/riscv_doirq.c#L58-L131) which calls...

- `#`: [`u16550_interrupt`](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/ramdisk2/drivers/serial/uart_16550.c#L918-L1021)

_What is `riscv_doirq: irq=35`?_

This is the Interrupt triggered by UART Input.

QEMU UART is at [RISC-V IRQ 10](https://github.com/lupyuen/nuttx-star64/blob/main/qemu-riscv64.dts#L225-L226), which becomes NuttX IRQ 35 (10 + 25).

[(RISCV_IRQ_EXT = RISCV_IRQ_SEXT = 16 + 9 = 25)](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/ramdisk2/arch/risc-v/include/irq.h#L75-L86)

_Why so many `riscv_doirq: irq=8`?_

NuttX IRQ 8 is [`RISCV_IRQ_ECALLU`](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/ramdisk2/arch/risc-v/include/irq.h#L52-L74): ECALL from RISC-V User Mode to Supervisor Mode.

This happens when the NuttX App (User Mode) calls a System Function in NuttX Kernel (Supervisor Mode).

![UART Output in NuttX QEMU](https://lupyuen.github.io/images/plic-qemu.png)

Now we compare the above with Star64...

# Compare UART Output: Star64 vs QEMU

Read the article...

-   ["Star64 JH7110 + NuttX RTOS: RISC-V PLIC Interrupts and Serial I/O"](https://lupyuen.github.io/articles/plic)

In the previous section we added logs to UART I/O in NuttX QEMU. We add the same logs to NuttX Star64 and compare...

```text
123067BCnx_start: Entry
up_irq_enable: 
up_enable_irq: irq=17
up_enable_irq: RISCV_IRQ_SOFT=17
uart_register: Registering /dev/console
uart_register: Registering /dev/ttyS0
up_enable_irq: irq=57
up_enable_irq: extirq=32, RISCV_IRQ_EXT=25
work_start_lowpri: Starting low-priority kernel worker thread(s)
board_late_initialize: 
nx_start_application: Starting init task: /system/bin/init
elf_symname: Symbol has no name
elf_symvalue: SHN_UNDEF: Failed to get symbol name: -3
elf_relocateadd: Section 2 reloc 2: Undefined symbol[0] has no name: -3
nx_start_application: ret=3
up_exit: TCB=0x404088d0 exiting
$%&riscv_doirq: irq=8
$%&riscv_doirq: irq=8
$%&riscv_doirq: irq=8
...
$%&riscv_doirq: irq=8
$%&riscv_doirq: irq=8
$%&riscv_doirq: irq=8
uart_write (0xc0200428):
0000  2a 2a 2a 6d 61 69 6e 0a                          ***main.        
AAAAAAAAAD$%&riscv_doirq: irq=8
$%&riscv_doirq: irq=8
$%&riscv_doirq: irq=8
$%&riscv_doirq: irq=8
...
$%&riscv_doirq: irq=8
$%&riscv_doirq: irq=8
$%&riscv_doirq: irq=8
uart_write (0xc000a610):
0000  0a 4e 75 74 74 53 68 65 6c 6c 20 28 4e 53 48 29  .NuttShell (NSH)
0010  20 4e 75 74 74 58 2d 31 32 2e 30 2e 33 0a         NuttX-12.0.3.  
AAAAAAAAAAAAAAAriscv_doirq: irq=8
uart_write (0xc0015338):
0000  6e 73 68 3e 20                                   nsh>            
AAAAAD$%&riscv_doirq: irq=8
uart_write (0xc0015310):
0000  1b 5b 4b                                         .[K             
AAAD$%&riscv_doirq: irq=8
nx_start: CPU0: Beginning Idle Loop
```

From the previous section, we know that [`uart_write`](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/ramdisk2/drivers/serial/serial.c#L1172-L1341), should call...

- `A`: [`uart_putxmitchar`](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/ramdisk2/drivers/serial/serial.c#L150-L286) which calls...

- `D`: [`uart_xmitchars`](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/ramdisk2/drivers/serial/serial_io.c#L42-L107) which calls...

- `E`: [`uart_txready`](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/ramdisk2/drivers/serial/serial_io.c#L63-L68) and...

  `F`: [`u16550_send`](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/ramdisk2/drivers/serial/uart_16550.c#L1542-L1556)

BUT from the above Star64 Log, we see that [`uart_txready`](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/ramdisk2/drivers/serial/serial_io.c#L63-L68) is NOT Ready.

That's why NuttX Star64 doesn't call [`u16550_send`](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/ramdisk2/drivers/serial/uart_16550.c#L1542-L1556) to print the output.

_Is our [__Interrupt Controller__](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64c/arch/risc-v/src/qemu-rv/hardware/qemu_rv_memorymap.h#L27-L33) OK?_

NuttX Star64 doesn't respond to UART Input. We'll check why in a while.

[(See the __JH7110 U74 Memory Map__)](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/u74_memory_map.html)

_Is the UART IRQ Number correct?_

Star64 UART is [RISC-V IRQ 32](https://doc-en.rvspace.org/VisionFive2/DG_UART/JH7110_SDK/general_uart_controller.html), which becomes NuttX IRQ 57 (32 + 25).

[(RISCV_IRQ_EXT = RISCV_IRQ_SEXT = 16 + 9 = 25)](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/ramdisk2/arch/risc-v/include/irq.h#L75-L86)

```bash
CONFIG_16550_UART0_IRQ=57
```

[(Source)](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64d/boards/risc-v/qemu-rv/rv-virt/configs/knsh64/defconfig#L10-L17)

Also from [JH7110 Interrupt Connections](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/interrupt_connections.html): `u0_uart`  is at `global_interrupts[27]`

Which is correct because [SiFive U74-MC Core Complex Manual](https://starfivetech.com/uploads/u74mc_core_complex_manual_21G1.pdf) (Page 198) says that `global_interrupts[0]` is PLIC Interrupt ID 5.

Thus `u0_uart`(IRQ 32) is at `global_interrupts[27]`.

_Is it the same UART IRQ as Linux?_

We check the Linux Device Tree...

```text
dtc \
  -o jh7110-visionfive-v2.dts \
  -O dts \
  -I dtb \
  jh7110-visionfive-v2.dtb
```

Which produces [jh7110-visionfive-v2.dts](https://github.com/lupyuen/nuttx-star64/blob/main/jh7110-visionfive-v2.dts)

UART0 is indeed RISC-V IRQ 32: [jh7110-visionfive-v2.dts](https://github.com/lupyuen/nuttx-star64/blob/main/jh7110-visionfive-v2.dts#L619-L631)

```text
serial@10000000 {
  compatible = "snps,dw-apb-uart";
  reg = <0x00 0x10000000 0x00 0x10000>;
  reg-io-width = <0x04>;
  reg-shift = <0x02>;
  clocks = <0x08 0x92 0x08 0x91>;
  clock-names = "baudclk\0apb_pclk";
  resets = <0x21 0x53 0x21 0x54>;
  interrupts = <0x20>;
  status = "okay";
  pinctrl-names = "default";
  pinctrl-0 = <0x24>;
};
```

_Maybe the IRQ Numbers are different for NuttX vs Linux?_

We tried to enable a whole bunch of IRQs, but nothing got triggered...

```text
up_enable_irq: irq=26
up_enable_irq: extirq=1, RISCV_IRQ_EXT=25
up_enable_irq: irq=27
up_enable_irq: extirq=2, RISCV_IRQ_EXT=25
up_enable_irq: irq=28
up_enable_irq: extirq=3, RISCV_IRQ_EXT=25
up_enable_irq: irq=29
...
up_enable_irq: irq=86
up_enable_irq: extirq=61, RISCV_IRQ_EXT=25
up_enable_irq: irq=87
up_enable_irq: extirq=62, RISCV_IRQ_EXT=25
up_enable_irq: irq=88
up_enable_irq: extirq=63, RISCV_IRQ_EXT=25
```

So there's definitely a problem with our Interrupt Controller.

_Maybe IRQ 32 is too high? (QEMU IRQ is only 10)_

[JH7110 Interrupt Connections](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/interrupt_connections.html) says that Global Interrupts are numbered 0 to 126 (127 total interrupts). That's a lot more than NuttX QEMU can handle.

Let's fix NuttX Star64 to support more IRQs.

From [qemu-rv/irq.h](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64d/arch/risc-v/include/qemu-rv/irq.h#L31-L40):

```c
/* Map RISC-V exception code to NuttX IRQ */

//// "JH7110 Interrupt Connections" says that Global Interrupts are 0 to 126 (127 total interrupts)
//// https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/interrupt_connections.html
#define NR_IRQS (RISCV_IRQ_SEXT + 127)

// Previously:
////#define QEMU_RV_IRQ_UART0  (RISCV_IRQ_MEXT + 10)
////#define NR_IRQS (QEMU_RV_IRQ_UART0 + 1)
```

From [qemu_rv_irq.c](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64d/arch/risc-v/src/qemu-rv/qemu_rv_irq.c#L46-L72):

```c
void up_irqinitialize(void)
{
  ...
  /* Set priority for all global interrupts to 1 (lowest) */
  int id;
  ////TODO: Why 52 PLIC Interrupts?
  for (id = 1; id <= NR_IRQS; id++) //// Changed 52 to NR_IRQS
    {
      putreg32(1, (uintptr_t)(QEMU_RV_PLIC_PRIORITY + 4 * id));
    }
```

This is hardcoded to 64 IRQs, we should fix in future: [qemu_rv_irq.c](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64d/arch/risc-v/src/qemu-rv/qemu_rv_irq.c#L143-L198)

```c
void up_enable_irq(int irq)
{
  ...
  else if (irq > RISCV_IRQ_EXT)
    {
      extirq = irq - RISCV_IRQ_EXT;
      _info("extirq=%d, RISCV_IRQ_EXT=%d\n", extirq, RISCV_IRQ_EXT);////

      /* Set enable bit for the irq */

      if (0 <= extirq && extirq <= 63) ////TODO: Why 63?
        {
          modifyreg32(QEMU_RV_PLIC_ENABLE1 + (4 * (extirq / 32)),
                      0, 1 << (extirq % 32));
        }
```

Now we study the NuttX Code for Platform-Level Interrupt Controller...

# Platform-Level Interrupt Controller for Star64

Read the article...

-   ["Star64 JH7110 + NuttX RTOS: RISC-V PLIC Interrupts and Serial I/O"](https://lupyuen.github.io/articles/plic)

The Platform-Level Interrupt Controller (PLIC) handles Global Interrupts triggered by Peripherals (like UART).

(PLIC works like Arm's Global Interrupt Controller)

We update the [NuttX PLIC Code](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64d/arch/risc-v/src/qemu-rv/qemu_rv_irq.c#L45-L214) based on these docs...

- [SiFive U74-MC Core Complex Manual](https://starfivetech.com/uploads/u74mc_core_complex_manual_21G1.pdf)

- [PLIC Spec](https://github.com/riscv/riscv-plic-spec/blob/master/riscv-plic.adoc)

![PLIC in JH7110 (U74) SoC](https://lupyuen.github.io/images/plic-title.jpg)

_How to configure PLIC to forward Interrupts to the Harts?_

The PLIC Memory Map is below...

From [SiFive U74-MC Core Complex Manual](https://starfivetech.com/uploads/u74mc_core_complex_manual_21G1.pdf) Page 193 (PLIC Memory Map)

| Address | Width | Attr | Description
|---------|-------|------|------------
| 0x0C00_0004 | 4B | RW | Source 1 priority
| 0x0C00_0220 | 4B | RW | Source 136 priority
| 0x0C00_1000 | 4B | RO | Start of pending array
| 0x0C00_1010 | 4B | RO | Last word of pending array
| 0x0C00_2100 | 4B | RW | Start Hart 1 S-Mode interrupt enables
| 0x0C00_2110 | 4B | RW | End Hart 1 S-Mode interrupt enables
| 0x0C00_2200 | 4B | RW | Start Hart 2 S-Mode interrupt enables
| 0x0C00_2210 | 4B | RW | End Hart 2 S-Mode interrupt enables
| 0x0C00_2300 | 4B | RW | Start Hart 3 S-Mode interrupt enables
| 0x0C00_2310 | 4B | RW | End Hart 3 S-Mode interrupt enables
| 0x0C00_2400 | 4B | RW | Start Hart 4 S-Mode interrupt enables
| 0x0C00_2410 | 4B | RW | End Hart 4 S-Mode interrupt enables
| 0x0C20_2000 | 4B | RW | Hart 1 S-Mode priority threshold
| 0x0C20_2004 | 4B | RW | Hart 1 S-Mode claim/complete 
| 0x0C20_4000 | 4B | RW | Hart 2 S-Mode priority threshold
| 0x0C20_4004 | 4B | RW | Hart 2 S-Mode claim/complete
| 0x0C20_6000 | 4B | RW | Hart 3 S-Mode priority threshold
| 0x0C20_6004 | 4B | RW | Hart 3 S-Mode claim/complete 
| 0x0C20_8000 | 4B | RW | Hart 4 S-Mode priority threshold
| 0x0C20_8004 | 4B | RW | Hart 4 S-Mode claim/complete

There are 5 Harts in JH7110...
- __Hart 0:__ S7 Core (the limited core, unused)
- __Harts 1 to 4:__ U7 Cores (the full cores)

According to OpenSBI, we are now running on Hart 1. (Sounds right)

(We pass the Hart ID to NuttX as Hart 0, since NuttX expects Hart ID to start at 0)

Based on the above PLIC Memory Map, we fix the PLIC Addresses in NuttX to use Hart 1: [qemu_rv_plic.h](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64d/arch/risc-v/src/qemu-rv/hardware/qemu_rv_plic.h#L33-L59)

```c
// | 0x0C00_0004 | 4B | RW | Source 1 priority
#define QEMU_RV_PLIC_PRIORITY    (QEMU_RV_PLIC_BASE + 0x000000)

// | 0x0C00_1000 | 4B | RO | Start of pending array
#define QEMU_RV_PLIC_PENDING1    (QEMU_RV_PLIC_BASE + 0x001000)

// Previously:
// #define QEMU_RV_PLIC_PRIORITY    (QEMU_RV_PLIC_BASE + 0x000000)
// #define QEMU_RV_PLIC_PENDING1    (QEMU_RV_PLIC_BASE + 0x001000)

#ifdef CONFIG_ARCH_USE_S_MODE
// | 0x0C00_2100 | 4B | RW | Start Hart 1 S-Mode interrupt enables
#  define QEMU_RV_PLIC_ENABLE1   (QEMU_RV_PLIC_BASE + 0x002100)
#  define QEMU_RV_PLIC_ENABLE2   (QEMU_RV_PLIC_BASE + 0x002104)

// | 0x0C20_2000 | 4B | RW | Hart 1 S-Mode priority threshold
#  define QEMU_RV_PLIC_THRESHOLD (QEMU_RV_PLIC_BASE + 0x202000)

// | 0x0C20_2004 | 4B | RW | Hart 1 S-Mode claim/complete 
#  define QEMU_RV_PLIC_CLAIM     (QEMU_RV_PLIC_BASE + 0x202004)

// Previously:
// #  define QEMU_RV_PLIC_ENABLE1   (QEMU_RV_PLIC_BASE + 0x002080)
// #  define QEMU_RV_PLIC_ENABLE2   (QEMU_RV_PLIC_BASE + 0x002084)
// #  define QEMU_RV_PLIC_THRESHOLD (QEMU_RV_PLIC_BASE + 0x201000)
// #  define QEMU_RV_PLIC_CLAIM     (QEMU_RV_PLIC_BASE + 0x201004)
```

_What about the PLIC Base Address?_

According to [U74 Memory Map](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/u74_memory_map.html), the Base Addresses are:

```text
0x00_0200_0000  0x00_0200_FFFF    RW A  CLINT
0x00_0C00_0000  0x00_0FFF_FFFF    RW A  PLIC
```

Which are correct in NuttX: [qemu_rv_memorymap.h](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64d/arch/risc-v/src/qemu-rv/hardware/qemu_rv_memorymap.h#L30-L32)

```c
#define QEMU_RV_CLINT_BASE   0x02000000
#define QEMU_RV_PLIC_BASE    0x0c000000
```

Note that there's a Core-Local Interruptor (CLINT) that handles Software Interrupt and Timer Interrupt...

![PLIC and CLINT in JH7110 (U74) SoC](https://lupyuen.github.io/images/plic-clint.jpg)

TODO: Do we need to handle CLINT?

Let's check that the RISC-V Interrupts are delegated correctly...

# Delegate Machine-Mode Interrupts to Supervisor-Mode

Read the article...

-   ["Star64 JH7110 + NuttX RTOS: RISC-V PLIC Interrupts and Serial I/O"](https://lupyuen.github.io/articles/plic)

_NuttX runs in RISC-V Supervisor Mode, which can't handle Interrupts directly. (Needs Machine Mode) How can we be sure that the RISC-V Interrupts are correctly handled in Supervisor Mode?_

From [SiFive Interrupt Cookbook](https://sifive.cdn.prismic.io/sifive/0d163928-2128-42be-a75a-464df65e04e0_sifive-interrupt-cookbook.pdf), Page 15:

> A CPU operating in Supervisor mode will trap to Machine mode upon the arrival of a Machine
mode interrupt, unless the Machine mode interrupt has been delegated to Supervisor mode
through the mideleg register. On the contrary, Supervisor interrupts will not immediately trigger
if a CPU is in Machine mode. While operating in Supervisor mode, a CPU does not have visibility to configure Machine mode interrupts.

According to the [RISC-V Spec](https://five-embeddev.com/riscv-isa-manual/latest/machine.html#machine-trap-delegation-registers-medeleg-and-mideleg), MIDELEG needs to be configured orrectly to delegate Machine Mode Interrupts to Supervisor Mode.

From [OpenSBI Log](https://lupyuen.github.io/articles/linux#appendix-opensbi-log-for-star64), we see the value of MIDELEG...

```bash
Boot HART MIDELEG: 0x0000000000000222
Boot HART MEDELEG: 0x000000000000b109
```

MIDELEG is defined by the following bits: [csr.h](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64d/arch/risc-v/include/csr.h#L343-L346):

```c
#define MIP_SSIP (0x1 << 1)
#define MIP_STIP (0x1 << 5)
#define MIP_MTIP (0x1 << 7)
#define MIP_SEIP (0x1 << 9)
```

So `Boot HART MIDELEG: 0x0000000000000222` means...
- SSIP: Delegate Supervisor Software Interrupt
- STIP: Delegate Supervisor Timer Interrupt
- SEIP: Delegate Supervisor External Interrupt

(But not MTIP: Delegate Machine Timer Interrupt)

Thus we're good, the interrupts should be correctly delegated from Machine Mode to Supervisor Mode for NuttX.

FYI: This is same for NuttX SBI: [nuttsbi/sbi_start.c](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64d/arch/risc-v/src/nuttsbi/sbi_start.c#L91-L94)

```c
  /* Delegate interrupts */

  reg = (MIP_SSIP | MIP_STIP | MIP_SEIP);
  WRITE_CSR(mideleg, reg);

  /* Delegate exceptions (all of them) */

  reg = ((1 << RISCV_IRQ_IAMISALIGNED) |
         (1 << RISCV_IRQ_INSTRUCTIONPF) |
         (1 << RISCV_IRQ_LOADPF) |
         (1 << RISCV_IRQ_STOREPF) |
         (1 << RISCV_IRQ_ECALLU));
  WRITE_CSR(medeleg, reg);
```

[SiFive Interrupt Cookbook](https://sifive.cdn.prismic.io/sifive/0d163928-2128-42be-a75a-464df65e04e0_sifive-interrupt-cookbook.pdf) states the Machine vs Supervisor Interrupt IDs:

Machine Mode Interrupts:
- Software Interrupt: Interrupt ID: 3
- Timer Interrupt: Interrupt ID: 7
- External Interrupt: Interrupt ID: 11

Supervisor Mode Interrupts:
- Software Interrupt: Interrupt ID: 1
- Timer Interrupt: Interrupt ID: 5
- External Interrupt: Interrupt ID: 9

# NuttX Star64 handles UART Interrupts

Read the article...

-   ["Star64 JH7110 + NuttX RTOS: RISC-V PLIC Interrupts and Serial I/O"](https://lupyuen.github.io/articles/plic)

_After fixing PLIC Interrupts on Star64... Are UART Interrupts OK?_

UART Interrupts at RISC-V IRQ 32 (NuttX IRQ 57) are now OK yay! But still no UART Output though...

```text
123067BCnx_start: Entry
up_irq_enable: 
up_enable_irq: irq=17
up_enable_irq: RISCV_IRQ_SOFT=17
uart_register: Registering /dev/console
uart_register: Registering /dev/ttyS0
up_enable_irq: irq=57
up_enable_irq: extirq=32, RISCV_IRQ_EXT=25
$%^&riscv_doirq: irq=57
#*$%^&riscv_doirq: irq=57
#*$%^&riscv_doirq: irq=57
#*$%^&riscv_doirq: irq=57
#*$%^&riscv_doirq: irq=57
...
#*$%^&riscv_doirq: irq=57
#*$%^&riscv_doirq: irq=57
#*$%^&riscv_doirq: irq=57
#*$%^&riscv_doirq: irq=57
#*$%^&nx_start: CPU0: Beginning Idle Loop
```

And NuttX detects the UART Input Interrupts when we type yay!

```text
123067BCnx_start: Entry
up_irq_enable: 
up_enable_irq: irq=17
up_enable_irq: RISCV_IRQ_SOFT=17
uart_register: Registering /dev/console
uart_register: Registering /dev/ttyS0
up_enable_irq: irq=57
up_enable_irq: extirq=32, RISCV_IRQ_EXT=25
u16550_rxint: enable=1
056789056789056789056789056789056789056789056789056789056789056789056789056789056789056789056789056789056789056789056789056789056789056789056789056789056789056789056789056789056789056789056789056789056789056789056789w056789o056789r056789k056789_056789s056789t056789a056789r056789t056789_056789l056789o056789w056789p056789r056789i056789:056789 056789S056789t056789a056789r056789056789t056789i056789n056789g056789 056789l056789o056789w056789-056789p056789r056789i056789o056789r056789i056789t056789y056789 056789k056789e056789r056789n056789e056789l056789 056789w056789o056789r056789k056789e056789r056789 056789t056789h056789r056789e+056789a
+++056789d++++056789(+++056789s+056789)056789
```

[(`+` means UART Input Interrupt)](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64d/drivers/serial/uart_16550.c#L965-L978)

But why is UART Interrupt triggered repeatedly with [UART_IIR_INTSTATUS = 0](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64d/drivers/serial/uart_16550.c#L954-L966)?

Is it because we didn't Complete a RISC-V Interrupt correctly?

_What happens if we don't Complete an Interrupt?_

Completing an Interrupt happens here: [qemu_rv_irq_dispatch.c](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64d/arch/risc-v/src/qemu-rv/qemu_rv_irq_dispatch.c#L81-L88)

```c
if (RISCV_IRQ_EXT <= irq)
  {
    /* Then write PLIC_CLAIM to clear pending in PLIC */
    putreg32(irq - RISCV_IRQ_EXT, QEMU_RV_PLIC_CLAIM);
  }
```

If we don't Complete an Interrupt, we won't receive any subsequent Interrupts (like UART Input)...

```text
123067BCnx_start: Entry
up_irq_enable: 
up_enable_irq: irq=17
up_enable_irq: RISCV_IRQ_SOFT=17
uart_register: Registering /dev/console
uart_register: Registering /dev/ttyS0
up_enable_irq: irq=57
up_enable_irq: extirq=32, RISCV_IRQ_EXT=25
u16550_rxint: enable=1
work_start_lowpri: Starting low-priority kernel worker thread(s)
board_late_initialize: 
nx_start_application: Starting init task: /system/bin/init
elf_symname: Symbol has no name
elf_symvalue: SHN_UNDEF: Failed to get symbol name: -3
elf_relocateadd: Section 2 reloc 2: Undefined symbol[0] has no name: -3
nx_start_application: ret=3
up_exit: TCB=0x404088d0 exiting
uart_write (0xc0200428):
0000  2a 2a 2a 6d 61 69 6e 0a                          ***main.        
u16550_txint: enable=0
AAAAAAAAAu16550_txint: enable=1
Duart_write (0xc000a610):
0000  0a 4e 75 74 74 53 68 65 6c 6c 20 28 4e 53 48 29  .NuttShell (NSH)
0010  20 4e 75 74 74 58 2d 31 32 2e 30 2e 33 0a         NuttX-12.0.3.  
u16550_txint: enable=0
AAAAAAAAAAAAAAAu16550_txint: enable=1
Duart_write (0xc0015338):
0000  6e 73 68 3e 20                                   nsh>            
u16550_txint: enable=0
AAAAAu16550_txint: enable=1
Duart_write (0xc0015310):
0000  1b 5b 4b                                         .[K             
u16550_txint: enable=0
AAAu16550_txint: enable=1
Du16550_rxint: enable=0
u16550_rxint: enable=1
nx_start: CPU0: Beginning Idle Loop
```

(No response to UART Input)

So it seems we are Completing Interrupts correctly.

We checked the other RISC-V NuttX Ports, they Claim and Complete Interrupts the exact same way.

_Are we Completing the Interrupt too soon? Maybe we should slow down?_

Let's slow down the Interrupt Completion with a Logging Delay: [qemu_rv_irq_dispatch.c](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64d/arch/risc-v/src/qemu-rv/qemu_rv_irq_dispatch.c#L81-L88)

```c
if (RISCV_IRQ_EXT <= irq)
  {
    _info("irq=%d, RISCV_IRQ_EXT=%d\n", irq, RISCV_IRQ_EXT);////
    /* Then write PLIC_CLAIM to clear pending in PLIC */
    putreg32(irq - RISCV_IRQ_EXT, QEMU_RV_PLIC_CLAIM);
  }
```

Seems to work better...

```text
123067BCnx_start: Entry
up_irq_enable: 
up_enable_irq: irq=17
up_enable_irq: RISCV_IRQ_SOFT=17
uart_register: Registering /dev/console
uart_register: Registering /dev/ttyS0
up_enable_irq: irq=57
up_enable_irq: extirq=32, RISCV_IRQ_EXT=25
u16550_rxint: enable=1
riscv_dispatch_irq: irq=57, RISCV_IRQ_EXT=25
056789riscv_dispatch_irq: irq=57, RISCV_IRQ_EXT=25
riscv_dispatch_irq: irq=57, RISCV_IRQ_EXT=25
riscv_dispatch_irq: irq=57, RISCV_IRQ_EXT=25
riscv_dispatch_irq: irq=57, RISCV_IRQ_EXT=25
...
riscv_dispatch_irq: irq=57, RISCV_IRQ_EXT=25
riscv_dispatch_irq: irq=57, RISCV_IRQ_EXT=25
riscv_dispatch_irq: irq=57, RISCV_IRQ_EXT=25
nx_start: CPU0: Beginning Idle Loop
```

Also we increase the System Delay (to match PinePhone):

- System Type > Delay loops per millisecond = 116524

```bash
CONFIG_BOARD_LOOPSPERMSEC=116524
```

[(Source)](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64d/boards/risc-v/qemu-rv/rv-virt/configs/knsh64/defconfig#L47)

_UART might need some time to warm up? Maybe we enable the IRQ later?_

Let's delay the enabling of IRQ to later...

We comment out the Enable IRQ in [uart_16550.c](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64d/drivers/serial/uart_16550.c#L860-L871):

```c
static int u16550_attach(struct uart_dev_s *dev) {
  ...
  /* Attach and enable the IRQ */
  ret = irq_attach(priv->irq, u16550_interrupt, dev);
#ifndef CONFIG_ARCH_NOINTC
  if (ret == OK)
    {
      /* Enable the interrupt (RX and TX interrupts are still disabled
       * in the UART */
      ////Enable Interrupt later:
      ////up_enable_irq(priv->irq);
```

And add it to `uart_write`: [serial.c](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64d/drivers/serial/serial.c#L1177-L1188)

```c
static ssize_t uart_write(FAR struct file *filep, FAR const char *buffer,
                          size_t buflen) {
  static int count = 0;
  if (count++ == 3) { up_enable_irq(57); }////
```

Seems better...

```text
123067BCnx_start: Entry
up_irq_enable: 
up_enable_irq: irq=17
up_enable_irq: RISCV_IRQ_SOFT=17
uart_register: Registering /dev/console
uart_register: Registering /dev/ttyS0
u16550_rxint: enable=1
work_start_lowpri: Starting low-priority kernel worker thread(s)
board_late_initialize: 
nx_start_application: Starting init task: /system/bin/init
elf_symname: Symbol has no name
elf_symvalue: SHN_UNDEF: Failed to get symbol name: -3
elf_relocateadd: Section 2 reloc 2: Undefined symbol[0] has no name: -3
nx_start_application: ret=3
up_exit: TCB=0x404088d0 exiting
uart_write (0xc0200428):
0000  2a 2a 2a 6d 61 69 6e 0a                          ***main.        
up_enable_irq: irq=57
up_enable_irq: extirq=32, RISCV_IRQ_EXT=25
056789056789056789056789056789056789u05678910567896056789505678950567890056789_056789t056789x056789i056789n056789t056789:056789 056789e056789n056789a056789b056789l056789e056789=0567890056789
056789056789056789A056789056789056789056789056789056789056789056789056789056789056789056789056789AAAAA056789AAA056789u05678910567896056789505678950567890056789_056789t056789x056789i056789n056789t056789:056789 056789e056789n056789a056789b056789l056789e056789=0567891056789
056789D-D-D-D-D-D-D-D-D-D-D-D-D-D-D-D-D-D-D-D-D-D-D-D-D-D-D-D-
```

After removing the logs, NSH works OK yay!

Watch what happens when we enter `ls` at the NSH Shell...

[(Watch the Demo on YouTube)](https://youtu.be/TdSJdiQFsv8)

![NSH on Star64](https://lupyuen.github.io/images/plic-nsh2.png)

```text
123067BCnx_start: Entry
up_irq_enable: 
up_enable_irq: irq=17
up_enable_irq: RISCV_IRQ_SOFT=17
uart_register: Registering /dev/console
uart_register: Registering /dev/ttyS0
work_start_lowpri: Starting low-priority kernel worker thread(s)
board_late_initialize: 
nx_start_application: Starting init task: /system/bin/init
elf_symname: Symbol has no name
elf_symvalue: SHN_UNDEF: Failed to get symbol name: -3
elf_relocateadd: Section 2 reloc 2: Undefined symbol[0] has no name: -3
nx_start_application: ret=3
up_exit: TCB=0x404088d0 exiting
up_enable_irq: irq=57
up_enable_irq: extirq=32, RISCV_IRQ_EXT=25
..***main

NuttShell (NSH) NuttX-12.0.3
nsh> ......++.+.l......s......
................................................p.o.s.i.x._.s.p.a.w.n..:. .p.i.d.=...0.x.c.0.2.0.2.9.7.8. .p.a.t.h.=..l.s. .f.i.l.e._.a.c.t.i.o.n.s.=...0.x.c.0.2.0.2.9.8.0. .a.t.t.r.=...0.x.c.0.2.0.2.9.8.8. .a.r.g.v.=...0.x.c.0.2.0.2.a.2.8.
.........................................................e.x.e.c._.s.p.a.w.n.:. .E.R.R.O..R.:. .F.a.i.l.e.d. .t.o. .l.o.a.d. .p.r.o.g.r.a.m. .'..l.s.'.:. ..-.2.
.......n.x.p.o.s.i.x._.s.p.a.w.n._.e.x.e.c.:. .E.R.R.O.R.:. .e.x.e.c. .f.a.i.l.e.d.:. ..2.
............................................................................................................../:
............................................................... dev......../
.............. proc......../
............... system........./
.............................................................nsh> ...................n.x._.s.t.a.r.t.:. .C.P.U.0.:. .B.e.g.i.n.n.i.n.g. .I.d.l.e. .L.o.o.p.
..........................
```

(So amazing that NuttX Apps and Context Switching are OK... Even though we haven't implemented the RISC-V Timer!)

But it's super slow. Each dot is 1 Million Calls to the UART Interrupt Handler, with UART Interrupt Status [UART_IIR_INTSTATUS = 0](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64d/drivers/serial/uart_16550.c#L954-L966)! 

From [uart_16550.c](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64d/drivers/serial/uart_16550.c#L948-L967):

```c
/* Get the current UART status and check for loop
  * termination conditions */
status = u16550_serialin(priv, UART_IIR_OFFSET);

/* The UART_IIR_INTSTATUS bit should be zero if there are pending
  * interrupts */
if ((status & UART_IIR_INTSTATUS) != 0)
  {
    /* Break out of the loop when there is no longer a
      * pending interrupt
      */
    //// Print after every 1 million interrupts:
    static int i = 0;
    if (i++ % 1000000 == 1) {
      *(volatile uint8_t *)0x10000000 = '.';
```

TODO: Why is UART Interrupt triggered repeatedly with [UART_IIR_INTSTATUS = 0](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64d/drivers/serial/uart_16550.c#L954-L966)?

_Maybe because OpenSBI is still handling UART Interrupts in Machine Mode?_

We tried to disable PLIC Interrupts for Machine Mode: [qemu_rv_irq.c](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64d/arch/risc-v/src/qemu-rv/qemu_rv_irq.c#L58-L63)

```c
  // Disable All Global Interrupts for Hart 1 Machine-Mode
  // | 0x0C00_2080 | 4B | RW | Start Hart 1 M-Mode interrupt enables
  #define QEMU_RV_PLIC_ENABLE1_MMODE   (QEMU_RV_PLIC_BASE + 0x002080)
  #define QEMU_RV_PLIC_ENABLE2_MMODE   (QEMU_RV_PLIC_BASE + 0x002084)
  putreg32(0x0, QEMU_RV_PLIC_ENABLE1_MMODE);
  putreg32(0x0, QEMU_RV_PLIC_ENABLE2_MMODE);
```

But we still see spurious UART interrupts.

TODO: How does OpenSBI handle UART I/O? Are the UART Interrupts still routed to OpenSBI? Can we remove them from OpenSBI?

TODO: [Robert Lipe](https://twitter.com/robertlipe/status/1685830584688340992?t=wTD98qn0WfhUCDho6px6gw) suggests that we check for floating inputs on the control signals

TODO: Throttle interrupts (for now) in [riscv_dispatch_irq](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64d/arch/risc-v/src/qemu-rv/qemu_rv_irq_dispatch.c#L56-L91)

TODO: Did we configure 16550 UART Interrupt Register correctly?

TODO: Is NuttX 16550 UART Driver any different from Linux?

# NuttX boots OK on Star64 JH7110

Read the article...

-   ["Star64 JH7110 + NuttX RTOS: Creating the First Release for the RISC-V SBC"](https://lupyuen.github.io/articles/release)

From the previous section we saw that JH7110 triggers too many spurious UART interrupts...

- ["Spurious UART Interrupts"](https://lupyuen.github.io/articles/plic#spurious-uart-interrupts)

JH7110 uses a Synopsys DesignWare 8250 UART that has a peculiar problem with the Line Control Register (LCR)... If we write to LCR while the UART is busy, it will trigger spurious UART Interrupts.

The fix is to wait for the UART to be not busy before writing to LCR. Here's my proposed patch for the NuttX 16550 UART Driver...

- ["Fix the Spurious UART Interrupts"](https://lupyuen.github.io/articles/plic#appendix-fix-the-spurious-uart-interrupts)

After fixing the spurious UART interrupts, now NuttX boots OK on Star64 yay!

![NuttX boots OK on Star64 JH7110](https://lupyuen.github.io/images/star64-bootok.png)

```text
Starting kernel ...
clk u5_dw_i2c_clk_core already disabled
clk u5_dw_i2c_clk_apb already disabled
BCnx_start: Entry
uart_register: Registering /dev/console
uart_register: Registering /dev/ttyS0
work_start_lowpri: Starting low-priority kernel worker thread(s)
nx_start_application: Starting init task: /system/bin/init
elf_symname: Symbol has no name
elf_symvalue: SHN_UNDEF: Failed to get symbol name: -3
elf_relocateadd: Section 2 reloc 2: Undefined symbol[0] has no name: -3
up_exit: TCB=0x40409890 exiting
nx_start: CPU0: Beginning Idle Loop

NuttShell (NSH) NuttX-12.0.3
nsh> uname -a
posix_spawn: pid=0xc0202978 path=uname file_actions=0xc0202980 attr=0xc0202988 argv=0xc0202a28
exec_spawn: ERROR: Failed to load program 'uname': -2
nxposix_spawn_exec: ERROR: exec failed: 2
NuttX 12.0.3 7a92743-dirty Aug  3 2023 18:06:04 risc-v star64
nsh> ls -l
posix_spawn: pid=0xc0202978 path=ls file_actions=0xc0202980 attr=0xc0202988 argv=0xc0202a28
exec_spawn: ERROR: Failed to load program 'ls': -2
nxposix_spawn_exec: ERROR: exec failed: 2
/:
 dr--r--r--       0 dev/
 dr--r--r--       0 proc/
 dr--r--r--       0 system/
nsh> 
```

[(Watch the Demo Video on YouTube)](https://youtu.be/6vQ-TXXojbQ)

[(See the Complete Log)](https://gist.github.com/lupyuen/eef8de0817ceed2072b2bacc925cdd96)

_How did we build NuttX for Star64?_

To build NuttX for Star64, [install the prerequisites](https://nuttx.apache.org/docs/latest/quickstart/install.html) and [clone the git repositories](https://nuttx.apache.org/docs/latest/quickstart/install.html) for ``nuttx`` and ``apps``.

Before building NuttX for Star64, download the __RISC-V Toolchain riscv64-unknown-elf__ from [SiFive RISC-V Tools](https://github.com/sifive/freedom-tools/releases/tag/v2020.12.0).

Add the downloaded toolchain `riscv64-unknown-elf-toolchain-.../bin` to the `PATH` Environment Variable.

Check the RISC-V Toolchain:

```bash
$ riscv64-unknown-elf-gcc -v
```

Configure the NuttX project and build the project:

```bash
$ cd nuttx
$ tools/configure.sh star64:nsh
$ make
$ riscv64-unknown-elf-objcopy -O binary nuttx nuttx.bin
```

This produces the NuttX Kernel ``nuttx.bin``.  Next, build the NuttX Apps Filesystem:

```bash
$ make export
$ pushd ../apps
$ tools/mkimport.sh -z -x ../nuttx/nuttx-export-*.tar.gz
$ make import
$ popd
$ genromfs -f initrd -d ../apps/bin -V "NuttXBootVol"
```

This generates the Initial RAM Disk ``initrd``.

Download the [Device Tree jh7110-visionfive-v2.dtb](https://github.com/starfive-tech/VisionFive2/releases/download/VF2_v3.1.5/jh7110-visionfive-v2.dtb) from [StarFive VisionFive2 Software Releases](https://github.com/starfive-tech/VisionFive2/releases) into the ``nuttx`` folder.

Now we create a Bootable MicroSD...

[(See the Build Outputs)](https://github.com/lupyuen2/wip-pinephone-nuttx/releases/tag/jh7110b-0.0.1)

[(See the Build Steps)](https://github.com/lupyuen2/wip-pinephone-nuttx/releases/tag/jh7110b-0.0.1)

[(See the Build Log)](https://gist.github.com/lupyuen/c6dc9aeec74d399029ebaf46ac16ef79)

# Bootable MicroSD for NuttX

Read the article...

-   ["Star64 JH7110 + NuttX RTOS: Creating the First Release for the RISC-V SBC"](https://lupyuen.github.io/articles/release)

_How do we create a Bootable MicroSD for NuttX?_

From the previous section, we have the NuttX Kernel ``nuttx.bin``, Initial RAM Disk ``initrd`` and Device Tree `jh7110-visionfive-v2.dtb`.

We'll pack all 3 files into a Flat Image Tree (FIT).

Inside the ``nuttx`` folder, create a Text File named ``nuttx.its``
with the following content: [nuttx.its](https://github.com/lupyuen/nuttx-star64/blob/main/nuttx.its)

```text
/dts-v1/;

/ {
  description = "NuttX FIT image";
  #address-cells = <2>;

  images {
    vmlinux {
      description = "vmlinux";
      data = /incbin/("./nuttx.bin");
      type = "kernel";
      arch = "riscv";
      os = "linux";
      load = <0x0 0x40200000>;
      entry = <0x0 0x40200000>;
      compression = "none";
    };

    ramdisk {
      description = "buildroot initramfs";
      data = /incbin/("./initrd");
      type = "ramdisk";
      arch = "riscv";
      os = "linux";
      load = <0x0 0x46100000>;
      compression = "none";
      hash-1 {
        algo = "sha256";
      };
    };

    fdt {
      data = /incbin/("./jh7110-visionfive-v2.dtb");
      type = "flat_dt";
      arch = "riscv";
      load = <0x0 0x46000000>;
      compression = "none";
      hash-1 {
        algo = "sha256";
      };
    };
  };

  configurations {
    default = "nuttx";

    nuttx {
      description = "NuttX";
      kernel = "vmlinux";
      fdt = "fdt";
      loadables = "ramdisk";
    };
  };
};
```

[(Based on visionfive2-fit-image.its)](https://github.com/starfive-tech/VisionFive2/blob/JH7110_VisionFive2_devel/conf/visionfive2-fit-image.its)

Package the NuttX Kernel, Initial RAM Disk and Device Tree into a
Flat Image Tree:

```bash
## For macOS:
brew install u-boot-tools
## For Linux:
sudo apt install u-boot-tools

## Generate FIT Image from `nuttx.bin`, `initrd` and `jh7110-visionfive-v2.dtb`.
## `nuttx.its` must be in the same directory as the NuttX binaries!
mkimage \
  -f nuttx.its \
  -A riscv \
  -O linux \
  -T flat_dt \
  starfiveu.fit

## To check FIT image
mkimage -l starfiveu.fit
```

We will see...

```text
→ mkimage -f nuttx.its -A riscv -O linux -T flat_dt starfiveu.fit
FIT description: NuttX FIT image
Created:         Fri Aug  4 23:20:52 2023
 Image 0 (vmlinux)
  Description:  vmlinux
  Created:      Fri Aug  4 23:20:52 2023
  Type:         Kernel Image
  Compression:  uncompressed
  Data Size:    2097800 Bytes = 2048.63 KiB = 2.00 MiB
  Architecture: RISC-V
  OS:           Linux
  Load Address: 0x40200000
  Entry Point:  0x40200000
 Image 1 (ramdisk)
  Description:  buildroot initramfs
  Created:      Fri Aug  4 23:20:52 2023
  Type:         RAMDisk Image
  Compression:  uncompressed
  Data Size:    8086528 Bytes = 7897.00 KiB = 7.71 MiB
  Architecture: RISC-V
  OS:           Linux
  Load Address: 0x46100000
  Entry Point:  unavailable
  Hash algo:    sha256
  Hash value:   44b3603e6e611ade7361a936aab09def23651399d4a0a3c284f47082d788e877
 Image 2 (fdt)
  Description:  unavailable
  Created:      Fri Aug  4 23:20:52 2023
  Type:         Flat Device Tree
  Compression:  uncompressed
  Data Size:    50235 Bytes = 49.06 KiB = 0.05 MiB
  Architecture: RISC-V
  Load Address: 0x46000000
  Hash algo:    sha256
  Hash value:   42767c996f0544f513280805b41f996446df8b3956c656bdbb782125ae8ffeec
 Default Configuration: 'nuttx220569'
 Configuration 0 (nuttx220569)
  Description:  NuttX
  Kernel:       vmlinux
  FDT:          fdt
  Loadables:    ramdisk
```

The Flat Image Tree ``starfiveu.fit`` will be copied to a microSD Card
in the next step.

To prepare the microSD Card, download the [microSD Image sdcard.img](https://github.com/starfive-tech/VisionFive2/releases/download/VF2_v3.1.5/sdcard.img) from [StarFive VisionFive2 Software Releases](https://github.com/starfive-tech/VisionFive2/releases)

Write the downloaded image to a microSD Card with [Balena Etcher](https://www.balena.io/etcher/) or [GNOME Disks](https://wiki.gnome.org/Apps/Disks).

Copy the file ``starfiveu.fit`` from the previous section and overwrite the file on the microSD Card.

```bash
## Copy to microSD
cp starfiveu.fit "/Volumes/NO NAME"
ls -l "/Volumes/NO NAME/starfiveu.fit"

## Unmount microSD
## TODO: Verify that /dev/disk2 is microSD
diskutil unmountDisk /dev/disk2
```

Check that Star64 is connected to our computer via a USB Serial Adapter.

Insert the microSD Card into Star64 and power up Star64.
NuttX boots on Star64 and NuttShell (nsh) appears in the Serial Console.

To see the available commands in NuttShell:

```bash
$ help
```

[Booting NuttX over TFTP](https://lupyuen.github.io/articles/tftp) is also supported on Star64.

[(See the Build Outputs)](https://github.com/lupyuen2/wip-pinephone-nuttx/releases/tag/jh7110b-0.0.1)

[(See the Build Steps)](https://github.com/lupyuen2/wip-pinephone-nuttx/releases/tag/jh7110b-0.0.1)

[(See the Build Log)](https://gist.github.com/lupyuen/c6dc9aeec74d399029ebaf46ac16ef79)

More about Flat Image Tree...

- [Flattened Image Tree (FIT) Format](https://u-boot.readthedocs.io/en/latest/usage/fit/source_file_format.html)

- [Single kernel and FDT blob](https://u-boot.readthedocs.io/en/latest/usage/fit/kernel_fdt.html)

- [Multiple kernels, ramdisks and FDT blobs](https://u-boot.readthedocs.io/en/latest/usage/fit/multi.html)

TODO: Why use sdcard.img

# Add Star64 JH7110 Arch and Board to NuttX

Read the article...

-   ["Star64 JH7110 + NuttX RTOS: Creating the First Release for the RISC-V SBC"](https://lupyuen.github.io/articles/release)

_How did we add Star64 JH7110 to NuttX as a new Arch and Board?_

We added Star64 JH7110 to NuttX with 3 Pull Requests...

1.  First we fix any dependencies needed by Star64 JH7110. This PR fixes the 16550 UART Driver used by JH7110...

    [Fix 16550 UART](https://github.com/apache/nuttx/pull/10019)

1.  Next we submit the PR that implements the JH7110 SoC as a __NuttX Arch__...

    [Add support for JH7110 SoC](https://github.com/apache/nuttx/pull/10069)

    We add JH7110 to the Kconfig for the RISC-V SoCs: [arch/risc-v/Kconfig](https://github.com/apache/nuttx/pull/10069/files#diff-9c348f27c59e1ed0d1d9c24e172d233747ee09835ab0aa7f156da1b7caa6a5fb)

    And we create a Kconfig for JH7110: [arch/risc-v/src/jh7110/Kconfig](https://github.com/apache/nuttx/pull/10069/files#diff-36a3009882ced77a24e9a7fd7ce3cf481ded4655f1adc366e7722a87ceab293b)

    Then we add the source files for JH7110 at...

    [arch/risc-v/src/jh7110](https://github.com/apache/nuttx/tree/master/arch/risc-v/src/jh7110)

1.  Finally we submit the PR that implements Star64 SBC as a __NuttX Board__...

    [Add support for Star64 SBC](https://github.com/lupyuen2/wip-pinephone-nuttx/pull/40)

    We add Star64 to the Kconfig for the NuttX Boards: [nuttx/boards/Kconfig](https://github.com/lupyuen2/wip-pinephone-nuttx/pull/38/files#diff-60cc096e3a9b22a769602cbbc3b0f5e7731e72db7b0338da04fcf665ed753b64)

    We create a Kconfig for Star64: [nuttx/boards/risc-v/jh7110/star64/Kconfig](https://github.com/lupyuen2/wip-pinephone-nuttx/pull/38/files#diff-76f41ff047f7cc79980a18f527aa05f1337be8416d3d946048b099743f10631c)

    And we add the source files for Star64 at...

    [boards/risc-v/jh7110/star64](https://github.com/apache/nuttx/tree/master/boards/risc-v/jh7110/star64)

1.  In the same PR, update the __NuttX Docs__...

    Add JH7110 and Star64 to the list of supported platforms:
    
    [Documentation/introduction/detailed_support.rst](https://github.com/lupyuen2/wip-pinephone-nuttx/pull/38/files#diff-d8a0e68fcb8fcb7e919c4b01226b6a25f888ed297145b82c719875cf8e6f5ae4)

    ![Supported Platforms](https://lupyuen.github.io/images/release-doc3.png)

    Create a page for the JH7110 NuttX Arch:

    [Documentation/platforms/risc-v/jh7110/index.rst](https://github.com/lupyuen2/wip-pinephone-nuttx/pull/38/files#diff-79d8d013e3cbf7600551f1ac23beb5db8bd234a0067576bfe0997b16e5d5c148)

    ![JH7110 Arch](https://lupyuen.github.io/images/release-doc2.png)

    Under JH7110, create a page for the Star64 NuttX Board:
    
    [Documentation/platforms/risc-v/jh7110/boards/star64/index.rst](https://github.com/lupyuen2/wip-pinephone-nuttx/pull/38/files#diff-a57fa454397c544c8a717c35212a88d3e3e0c77c9c6e402f5bb52dfeb62e1349)

    ![Star64 Board](https://lupyuen.github.io/images/release-doc1.png)

_Seems we need to copy a bunch of source files across branches?_

No sweat! Suppose we created a staging PR in our own repo...

- [github.com/lupyuen2/wip-pinephone-nuttx/pull/40](https://github.com/lupyuen2/wip-pinephone-nuttx/pull/40)

This command produces a list of changed files...

```bash
## TODO: Change this to your PR
pr=https://github.com/lupyuen2/wip-pinephone-nuttx/pull/40
curl -L $pr.diff \
  | grep "diff --git" \
  | sort \
  | cut -d" " -f3 \
  | cut -c3-
```

Like this...

```text
boards/risc-v/jh7110/star64/include/board.h
boards/risc-v/jh7110/star64/include/board_memorymap.h
boards/risc-v/jh7110/star64/scripts/Make.defs
boards/risc-v/jh7110/star64/scripts/ld.script
```

That we can copy to another branch in a script...

```bash
b=$HOME/new_branch
mkdir -p $b/boards/risc-v/jh7110/star64/include
mkdir -p $b/boards/risc-v/jh7110/star64/scripts

a=boards/risc-v/jh7110/star64/include/board.h
cp $a $b/$a
a=boards/risc-v/jh7110/star64/include/board_memorymap.h
cp $a $b/$a
a=boards/risc-v/jh7110/star64/scripts/Make.defs
cp $a $b/$a
a=boards/risc-v/jh7110/star64/scripts/ld.script
cp $a $b/$a
```

_How did we generate the NuttX Build Configuration?_

The NuttX Build Configuration for Star64 is at...

[boards/risc-v/jh7110/star64/configs/nsh/defconfig](https://github.com/lupyuen2/wip-pinephone-nuttx/pull/40/files#diff-cdbd91013d0074f15d469491b707d1d6576752bd7b7b9ec6ed311edba8ab4b53)

We generated the `defconfig` with this command...

```bash
make menuconfig \
  && make savedefconfig \
  && grep -v CONFIG_HOST defconfig \
  >boards/risc-v/jh7110/star64/configs/nsh/defconfig
```

During development, we should enable additional debug options...

```text
CONFIG_DEBUG_ASSERTIONS=y
CONFIG_DEBUG_ASSERTIONS_EXPRESSION=y
CONFIG_DEBUG_BINFMT=y
CONFIG_DEBUG_BINFMT_ERROR=y
CONFIG_DEBUG_BINFMT_WARN=y
CONFIG_DEBUG_ERROR=y
CONFIG_DEBUG_FEATURES=y
CONFIG_DEBUG_FS=y
CONFIG_DEBUG_FS_ERROR=y
CONFIG_DEBUG_FS_WARN=y
CONFIG_DEBUG_FULLOPT=y
CONFIG_DEBUG_INFO=y
CONFIG_DEBUG_MM=y
CONFIG_DEBUG_MM_ERROR=y
CONFIG_DEBUG_MM_WARN=y
CONFIG_DEBUG_SCHED=y
CONFIG_DEBUG_SCHED_ERROR=y
CONFIG_DEBUG_SCHED_INFO=y
CONFIG_DEBUG_SCHED_WARN=y
CONFIG_DEBUG_SYMBOLS=y
CONFIG_DEBUG_WARN=y
```

- BINFMT is the Binary Loader, good for troubleshooting NuttX App ELF loading issues

- SCHED is for Task Scheduler, which will show the spawning of NuttX App Tasks

- MM is for Memory Management, for troubleshooting Memory Mapping issues

- FS is for File System

Before merging with NuttX Mainline, remove the BINFMT, FS, MM and SCHED debug options.

TODO: GPIO next

# StarFive VisionFive2 Software Release

Read the article...

-   ["Star64 JH7110 + NuttX RTOS: Creating the First Release for the RISC-V SBC"](https://lupyuen.github.io/articles/release)

StarFive VisionFive2 Software Releases seem to boot OK on Star64...

- [VisionFive2 Software Releases](https://github.com/starfive-tech/VisionFive2/releases)

- [SD Card Image](https://github.com/starfive-tech/VisionFive2/releases/download/VF2_v3.1.5/sdcard.img)

[(See the Boot Log for Star64)](https://gist.github.com/lupyuen/030e4feb2fa95319290f3027032c24a8)

Login with...

```text
buildroot login: root
Password: starfive
```

Based on the files above, we figured out how to generate the Flat Image Tree for NuttX: [Makefile](https://github.com/starfive-tech/VisionFive2/blob/JH7110_VisionFive2_devel/Makefile#L279-L283)

Also we see the script that generates the SD Card Image: [genimage.sh](https://github.com/starfive-tech/VisionFive2/blob/JH7110_VisionFive2_devel/genimage.sh)

```bash
genimage \
  --rootpath "${ROOTPATH_TMP}"     \
  --tmppath "${GENIMAGE_TMP}"    \
  --inputpath "${INPUT_DIR}"  \
  --outputpath "${OUTPUT_DIR}" \
  --config genimage-vf2.cfg
```

The SD Card Partitions are defined in [genimage-vf2.cfg](https://github.com/starfive-tech/VisionFive2/blob/JH7110_VisionFive2_devel/conf/genimage-vf2.cfg):

```text
image sdcard.img {
  hdimage {
    gpt = true
  }

  partition spl {
    image = "work/u-boot-spl.bin.normal.out"
    partition-type-uuid = 2E54B353-1271-4842-806F-E436D6AF6985
    offset = 2M
    size = 2M
  }

  partition uboot {
    image = "work/visionfive2_fw_payload.img"
    partition-type-uuid = 5B193300-FC78-40CD-8002-E86C45580B47
    offset = 4M
    size = 4M
  }

  partition image {
    # partition-type = 0xC
    partition-type-uuid = EBD0A0A2-B9E5-4433-87C0-68B6B72699C7
    image = "work/starfive-visionfive2-vfat.part"
    offset = 8M
    size = 292M
  }

  partition root {
    # partition-type = 0x83
    partition-type-uuid = 0FC63DAF-8483-4772-8E79-3D69D8477DE4
    image = "work/buildroot_rootfs/images/rootfs.ext4"
    offset = 300M
    bootable = true
  }
}
```

Useful for creating our own SD Card Partitions!

(We won't need the `spl`, `uboot` and `root` partitions for NuttX)

# UART Clock for JH7110

Read the article...

-   ["Star64 JH7110 + NuttX RTOS: Creating the First Release for the RISC-V SBC"](https://lupyuen.github.io/articles/release)

_How did we figure out the UART Clock for JH7110?_

```bash
CONFIG_16550_UART0_CLOCK=23040000
```

[(Source)](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/57d5bba4723b58c7bb947f9fa206be377c80c8d0/boards/risc-v/jh7110/star64/configs/nsh/defconfig#L10-L18)

We logged the values of DLM and DLL in the UART Driver during startup...

```c
uint32_t dlm = u16550_serialin(priv, UART_DLM_OFFSET);
uint32_t dll = u16550_serialin(priv, UART_DLL_OFFSET);
```

[(We capture DLM and DLL only when DLAB=1)](https://github.com/apache/nuttx/blob/master/drivers/serial/uart_16550.c#L817-L851)

(Be careful to print only when DLAB=0)

According to our log, DLM is 0 and DLL is 13. Which means..

```text
dlm =  0 = (div >> 8)
dll = 13 = (div & 0xff)
```

Which gives `div=13`. Now since `baud=115200` at startup...

```text
div = (uartclk + (baud << 3)) / (baud << 4)
13  = (uartclk + 921600) / 1843200
uartclk = (13 * 1843200) - 921600
        = 23040000
```

Thus `uartclk=23040000`. And that's why we set...

```bash
CONFIG_16550_UART0_CLOCK=23040000
```

[(Source)](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/57d5bba4723b58c7bb947f9fa206be377c80c8d0/boards/risc-v/jh7110/star64/configs/nsh/defconfig#L10-L18)

# HDMI Display for Star64 JH7110

Read the article...

-   ["RISC-V Star64 JH7110: Inside the Display Controller"](https://lupyuen.github.io/articles/display2)

_Will NuttX work with the HDMI Display on Star64?_

Let's find out! Maybe our HDMI code will be reused for PineTab-V's MIPI DSI Display Panel. Here are the official docs...

- [Display Subsystem](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/display_subsystem.html)

- [SDK for HDMI](http://doc-en.rvspace.org/VisionFive2/DG_HDMI/)

- [Display Controller Developing Guide](http://doc-en.rvspace.org/VisionFive2/DG_Display/)

- [GPU Developing and Porting Guide](http://doc-en.rvspace.org/VisionFive2/DG_GPU/)

- [Multimedia Developing Guide](http://doc-en.rvspace.org/VisionFive2/DG_Multimedia/)

- [MIPI LCD Developing and Porting Guide](http://doc-en.rvspace.org/VisionFive2/DG_LCD/)

From the docs above we have the [Display Subsystem Block Diagram](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/block_diagram_display.html)...

![Display Subsystem Block Diagram](https://doc-en.rvspace.org/JH7110/TRM/Image/RD/JH7110/vout_block_diagram18.png)

[(Source)](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/block_diagram_display.html)

Which says that JH7110 uses a __DC8200 Dual Display Controller__ to drive the MIPI DSI and HDMI Displays.

[(But the DC8200 docs are confidential sigh)](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/detail_info_display.html)

And we have the [Display Subsystem Clock and Reset](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/clock_n_reset_display.html)...

![Display Subsystem Clock and Reset](https://doc-en.rvspace.org/JH7110/TRM/Image/RD/JH7110/vout_clkrst18.png)

[(Source)](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/clock_n_reset_display.html)

So to make HDMI work on JH7110, we need a create a NuttX Driver for the DC8200 Display Controller...

# DC8200 Display Controller for Star64 JH7110

Read the article...

-   ["RISC-V Star64 JH7110: Inside the Display Controller"](https://lupyuen.github.io/articles/display2)

Let's talk about the __DC8200 Dual Display Controller__.

[(But the DC8200 docs are confidential sigh)](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/detail_info_display.html)

Here's the [Block Diagram of DC8200 Display Controller](https://doc-en.rvspace.org/VisionFive2/DG_Display/JH7110_SDK/block_diagram_display.html)...

![Block Diagram of DC8200 Display Controller](https://doc-en.rvspace.org/VisionFive2/DG_Display/Image/JH7110_SDK/Display_Block_Diagram.png)

[(Source)](https://doc-en.rvspace.org/VisionFive2/DG_Display/JH7110_SDK/block_diagram_display.html)

(Display Devices refer to MIPI DPHY and HDMI, interchangeable)

Here are the [Linux Drivers for DC8200 Display Controller](https://doc-en.rvspace.org/VisionFive2/DG_Display/JH7110_SDK/source_code_structure_display.html)...

- [vs_dc.c](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc.c): Display Controller

- [vs_dc_hw.c](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc_hw.c): Framebuffer and Overlay (similar to A64 Display Engine)

- [vs_drv.c](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_drv.c): Device for Direct Rendering Manager

- [vs_crtc.c](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_crtc.c): Display Pipeline (Colour / Gamma / LUT)

- [vs_plane.c](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_plane.c): Display Plane

- [vs_simple_enc.c](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_simple_enc.c): [Display Subsystem (DSS)](https://software-dl.ti.com/processor-sdk-linux/esd/docs/06_03_00_106/linux/Foundational_Components/Kernel/Kernel_Drivers/Display/DSS.html) Encoder

- [vs_gem.c](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_gem.c): [Graphics Execution Manager](https://en.wikipedia.org/wiki/Direct_Rendering_Manager#Graphics_Execution_Manager) (Memory Management Framework)

- [vs_virtual.c](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_virtual.c): Virtual Display

- [vs_dc_dec.c](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc_dec.c): Bitmap Decompression

[(See the Notes here)](https://github.com/starfive-tech/linux/tree/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon)

We'll see the Call Flow in a while.

Are these used?

- [vs_dc_mmu.c](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc_mmu.c): Memory Mapping

- [vs_fb.c](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_fb.c): GEM Memory Mapping for Framebuffer

Here's the (partial) [Linux Device Tree for DC8200](https://doc-en.rvspace.org/VisionFive2/DG_Display/JH7110_SDK/device_tree_config_display.html)...

```text
&dc8200 {
  status = "okay";

  dc_out: port {
    #address-cells = <1>;
    #size-cells = <0>;
    dc_out_dpi0: endpoint@0 {
      reg = <0>;
      remote-endpoint = <&hdmi_input0>;
    };
    dc_out_dpi1: endpoint@1 {
      reg = <1>;
      remote-endpoint = <&hdmi_in_lcdc>;
    };

    dc_out_dpi2: endpoint@2 {
      reg = <2>;
      remote-endpoint = <&mipi_in>;
    };
  };
};
```

[(Source)](https://doc-en.rvspace.org/VisionFive2/DG_Display/JH7110_SDK/device_tree_config_display.html)

HDMI I2C Encoder in JH7110 is the [NXP Semiconductors TDA998X HDMI Encoder](https://doc-en.rvspace.org/VisionFive2/DG_Display/JH7110_SDK/kernel_menu_config_diplay.html)

Next we need to create a NuttX Driver for the HDMI Controller...

# HDMI Controller for Star64 JH7110

The HDMI Controller for JH7110 is [Inno HDMI 2.0 Transmitter For TSMC28HPC+](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/detail_info_display.html).

Based on [JH7110 HDMI Developing Guide](https://doc-en.rvspace.org/VisionFive2/DG_HDMI/JH7110_SDK/source_code_structure_hdmi.html), the Linux Drivers for JH7110 HDMI (VeriSilicon Inno HDMI) are...

- [inno_hdmi.c](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/inno_hdmi.c)

- [inno_hdmi.h](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/inno_hdmi.h)

The [Linux Device Tree](https://doc-en.rvspace.org/VisionFive2/DG_HDMI/JH7110_SDK/device_tree_hdmi.html) looks like...

```text
hdmi: hdmi@29590000 {
    compatible = "starfive,jh7100-hdmi","inno,hdmi";
      reg = <0x0 0x29590000 0x0 0x4000>;
      interrupts = <99>;
      status = "disabled";
      clocks = <&clkvout JH7110_U0_HDMI_TX_CLK_SYS>,
        <&clkvout JH7110_U0_HDMI_TX_CLK_MCLK>,
        <&clkvout JH7110_U0_HDMI_TX_CLK_BCLK>,
        <&hdmitx0_pixelclk>;
      clock-names = "sysclk", "mclk","bclk","pclk";
      resets = <&rstgen RSTN_U0_HDMI_TX_HDMI>;
      reset-names = "hdmi_tx";
    };
...
&hdmi {
  status = "okay";
  pinctrl-names = "default";
  pinctrl-0 = <&inno_hdmi_pins>;

  hdmi_in: port {
    #address-cells = <1>;
    #size-cells = <0>;
    hdmi_in_lcdc: endpoint@0 {
      reg = <0>;
      remote-endpoint = <&dc_out_dpi1>;
    };
  };
};
```

[(Source)](https://doc-en.rvspace.org/VisionFive2/DG_HDMI/JH7110_SDK/device_tree_hdmi.html)

We see the [HDMI Initialization Process](https://doc-en.rvspace.org/VisionFive2/DG_HDMI/JH7110_SDK/initialization_process.html)...

![HDMI Initialization Process](https://doc-en.rvspace.org/VisionFive2/DG_HDMI/Image/JH7110_SDK/HDMI_Init.svg)

[(Source)](https://doc-en.rvspace.org/VisionFive2/DG_HDMI/JH7110_SDK/initialization_process.html)

And the [HDMI Plug and Unplug Process](https://doc-en.rvspace.org/VisionFive2/DG_HDMI/JH7110_SDK/plug_n_unplug_process.html)...

![HDMI Plug and Unplug Process](https://doc-en.rvspace.org/VisionFive2/DG_HDMI/Image/JH7110_SDK/HDMI_Pug_Unplug.svg)

[(Source)](https://doc-en.rvspace.org/VisionFive2/DG_HDMI/JH7110_SDK/plug_n_unplug_process.html)

# Test HDMI for Star64 JH7110

_How will we test the HDMI Display for Star64 JH7110?_

We run the [`modetest` command to test HDMI](https://doc-en.rvspace.org/VisionFive2/DG_Display/JH7110_SDK/test_example_display.html)...

```bash
modetest \
  -M starfive \
  -D 0 \
  -a \
  -s 116@31:1920x1080 \
  -P 39@31:1920x1080@RG16 \
  -Ftiles 
```

[(Source)](https://doc-en.rvspace.org/VisionFive2/DG_Display/JH7110_SDK/test_example_display.html)

`116@31:1920x1080` means `<Connector ID>@<CRTC ID>: <Resolution>`

`39@31:1920x1080@RG16` means `<Plane ID>@<CRTC ID>: <Resolution>@<Format>`

[(CRTC "CRT Controller" refers to the Display Pipeline)](https://en.wikipedia.org/wiki/Direct_Rendering_Manager#KMS_device_model)

See also...

- [Before Debug](https://doc-en.rvspace.org/VisionFive2/DG_Display/JH7110_SDK/before_debug.html)

- [Debug Display](https://doc-en.rvspace.org/VisionFive2/DG_Display/JH7110_SDK/debug_hdmi.html)

TODO: What's inside the modetest app? [modetest.c](https://gitlab.freedesktop.org/mesa/drm/-/blob/main/tests/modetest/modetest.c)

TODO: What parameters does modetest pass to the DC8200 Driver?

TODO: Can we create a simpler modetest for our own testing on NuttX?

# Direct Rendering Manager Driver for DC8200

Read the article...

-   ["RISC-V Star64 JH7110: Inside the Display Controller"](https://lupyuen.github.io/articles/display2)

![JH7110 Linux Display Driver](https://lupyuen.github.io/images/jh7110-display.jpg)

Let's walk through the code in the Linux Driver for DC8200 Display Controller, to understand how we'll implement it in NuttX.

The DRM Driver is named "starfive"...

```c
// name = "starfive"
static struct platform_driver vs_drm_platform_driver = {
  .probe  = vs_drm_platform_probe,
  .remove = vs_drm_platform_remove,
  ...
};
```

[(Source)](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_drv.c#L448-L457)

Here are the DRM Operations supported by the driver...

```c
static struct drm_driver vs_drm_driver = {
  .driver_features    = DRIVER_MODESET | DRIVER_ATOMIC | DRIVER_GEM,
  .lastclose          = drm_fb_helper_lastclose,
  .prime_handle_to_fd = drm_gem_prime_handle_to_fd,
  .prime_fd_to_handle = drm_gem_prime_fd_to_handle,
  .gem_prime_import   = vs_gem_prime_import,
  .gem_prime_import_sg_table = vs_gem_prime_import_sg_table,
  .gem_prime_mmap     = vs_gem_prime_mmap,
  .dumb_create        = vs_gem_dumb_create,
#ifdef CONFIG_DEBUG_FS
  .debugfs_init       = vs_debugfs_init,
#endif
  .fops  = &fops,
  .name  = "starfive",
  .desc  = "VeriSilicon DRM driver",
  .date  = "20191101",
  .major = DRV_MAJOR,
  .minor = DRV_MINOR,
};
```

[(Source)](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_drv.c#L125-L143)

The DRM Driver includes these Sub Drivers...

```c
static struct platform_driver *drm_sub_drivers[] = {
  /* put display control driver at start */
  &dc_platform_driver,

  /* connector */
#ifdef CONFIG_STARFIVE_INNO_HDMI
  &inno_hdmi_driver,
#endif

  &simple_encoder_driver,

#ifdef CONFIG_VERISILICON_VIRTUAL_DISPLAY
  &virtual_display_platform_driver,
#endif
};
```

[(Source)](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_drv.c#L301-L315)

(More about [dc_platform_driver](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc.c#L1642-L1649) in the next section)

[vs_drm_init](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_drv.c#L459-L472) registers [drm_sub_drivers](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_drv.c#L301-L315) and [vs_drm_platform_driver](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_drv.c#L448-L457)
 at startup.

Here are the File Operations supported by the DRM Driver...

```c
static const struct file_operations fops = {
  .owner     = THIS_MODULE,
  .open      = drm_open,
  .release   = drm_release,
  .unlocked_ioctl = drm_ioctl,
  .compat_ioctl   = drm_compat_ioctl,
  .poll      = drm_poll,
  .read      = drm_read,
  .mmap      = vs_gem_mmap,
};
```

[(Source)](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_drv.c#L54-L63)

[(More about Direct Rendering Manager)](https://en.wikipedia.org/wiki/Direct_Rendering_Manager)

[(__Justin / Fishwaldo__ suggests that we check out the simpler HDMI Driver in U-Boot)](https://fosstodon.org/@Fishwaldo/110902984442385966)

# Call Flow for DC8200 Display Controller Driver

Read the article...

-   ["RISC-V Star64 JH7110: Inside the Display Controller"](https://lupyuen.github.io/articles/display2)

The DC8200 Controller Driver is named "vs-dc" (for VeriSilicon)...

```c
// name = "vs-dc"
struct platform_driver dc_platform_driver = {
  .probe  = dc_probe,
  .remove = dc_remove,
  ...
};
```

[(Source)](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc.c#L1642-L1649)

Probe for Display Controller is implemented here: [dc_probe](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc.c#L1595-L1629)

We see the Component Functions exposed by the driver...

```c
const struct component_ops dc_component_ops = {
  .bind   = dc_bind,
  .unbind = dc_unbind,
};
```

[(Source)](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc.c#L1584-L1587)

Bind to Display Controller is here...

- [dc_bind](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc.c#L1421-L1573), which calls..

- [dc_init](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc.c#L644-L722), which calls...

- [dc_hw_init](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc_hw.c#L1301-L1361)

Here are the Display Pipeline [(CRTC)](https://www.kernel.org/doc/html/v4.15/gpu/drm-kms.html) functions exposed by the driver...

```c
static const struct vs_crtc_funcs dc_crtc_funcs = {
  .enable        = vs_dc_enable,
  .disable       = vs_dc_disable,
  .mode_fixup    = vs_dc_mode_fixup,
  .set_gamma     = vs_dc_set_gamma,
  .enable_gamma  = vs_dc_enable_gamma,
  .enable_vblank = vs_dc_enable_vblank,
  .commit        = vs_dc_commit,
};
```

[(Source)](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc.c#L1400-L1408)

Enable Display Pipeline is implemented here...

- [vs_dc_enable](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc.c#L740-L826), which calls...

- [dc_hw_setup_display](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc_hw.c#L1480-L1487)

Enable Display Pipeline [vs_dc_enable](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc.c#L740-L826) is called by [vs_crtc_atomic_enable](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_crtc.c#L265-L276)

Which is called by [drm_atomic_helper](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/drm_atomic_helper.c#L1323-L1408)

```c
static const struct drm_crtc_helper_funcs vs_crtc_helper_funcs = {
  .mode_fixup     = vs_crtc_mode_fixup,
  .atomic_enable  = vs_crtc_atomic_enable,
  .atomic_disable = vs_crtc_atomic_disable,
  .atomic_begin   = vs_crtc_atomic_begin,
  .atomic_flush   = vs_crtc_atomic_flush,
};
```

[(Source)](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_crtc.c#L338-L344)

Commit Display Pipeline is here...

- [vs_dc_commit](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc.c#L1381-L1398), which calls...

- [dc_hw_commit](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc_hw.c#L2038-L2076)

Commit Display Pipeline [vs_dc_commit](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc.c#L1381-L1398) is called by [vs_crtc_atomic_flush](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_crtc.c#L320-L336)

Which is called by [drm_atomic_helper](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/drm_atomic_helper.c#L2445-L2570)

These are the exposed functions for the Display Plane...

```c
static const struct vs_plane_funcs dc_plane_funcs = {
  .update  = vs_dc_update_plane,
  .disable = vs_dc_disable_plane,
  .check   = vs_dc_check_plane,
};
```

[(Source)](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc.c#L1410-L1414)

Update Display Plane is here...

- [vs_dc_update_plane](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc.c#L1262-L1280), which calls...

- [update_plane](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc.c#L1153-L1196), which calls...

- [dc_hw_update_plane](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc_hw.c#L1368-L1399)

Update Display Plane [vs_dc_update_plane](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc.c#L1262-L1280) is called by [vs_plane_atomic_update](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_plane.c#L268-L301)

Which is called by [drm_atomic_helper](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/drm_atomic_helper.c#L2445-L2570)

```c
const struct drm_plane_helper_funcs vs_plane_helper_funcs = {
  .atomic_check   = vs_plane_atomic_check,
  .atomic_update  = vs_plane_atomic_update,
  .atomic_disable = vs_plane_atomic_disable,
};
```

[(Source)](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_plane.c#L314-L318)

Refer to [Linux DRM Internals](https://www.kernel.org/doc/html/v4.15/gpu/drm-internals.html)

# Call Flow for DC8200 Display Hardware Driver

Read the article...

-   ["RISC-V Star64 JH7110: Inside the Display Controller"](https://lupyuen.github.io/articles/display2)

Display Planes Info: [dc_hw_planes](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc_hw.c#L472-L1084)

Display Controller Info: [dc_info](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc_hw.c#L1086-L1150)

Initialise Display Hardware: [dc_hw_init](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc_hw.c#L1301-L1361)
- Read the Hardware Revision and Chip ID
- Initialise every Layer / Display Plane
- Initialise every Panel (Cursor)

Commit Display Hardware: [dc_hw_commit](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc_hw.c#L2038-L2076)
- Call [gamma_ex_commit](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc_hw.c#L1548-L1574)
- Call [plane_ex_commit](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc_hw.c#L1768-L1863)
- Update Cursor
- Update QoS

Update Display Plane: [dc_hw_update_plane](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc_hw.c#L1368-L1399)
- Copy Framebuffer
- Copy Scale
- Copy Position
- Copy Blend

Display Hardware Functions:

```c
static const struct dc_hw_funcs hw_func = {
  .gamma   = &gamma_ex_commit,
  .plane   = &plane_ex_commit,
  .display = setup_display_ex,
};
```

[(Source)](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc_hw.c#L2032-L2036)

Setup Display (Upper Level): [dc_hw_setup_display](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc_hw.c#L1480-L1487)
- Copy Display Struct
- Call [setup_display_ex](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc_hw.c#L1971-L2030)

Setup Display (Extended): [setup_display_ex](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc_hw.c#L1971-L2030)
- Set Colour Format
- Call [setup_display](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc_hw.c#L1865-L1969)

Setup Display (Lower Level): [setup_display](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc_hw.c#L1865-L1969)
- Set DPI Config
- Disable Display Panel
- Set Display Horizontal Resolution
- Set Display Horizontal Sync
- Set Display Vertical Resolution
- Set Display Vertical Resolution Sync
- Configure Framebuffer Sync Mode
- Set Framebuffer Background Colour
- Set Display Dither
- Enable Display Panel
- Set Overlay Config
- Set Cursor Config

Commit Display Plane (Extended): [plane_ex_commit](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc_hw.c#L1768-L1863)
- Set Colour Space
- Set Gamma
- Call [plane_commit](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc_hw.c#L1576-L1766)

Commit Display Plane: [plane_commit](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc_hw.c#L1576-L1766)
- For every Layer / Display Plane:
- Set Framebuffer YUV Address
- Set Framebuffer YUV Stride
- Set Framebuffer Width and Height
- Clear Framebuffer
- Set Primary Framebuffer Config
- Set Non-Primary Framebuffer Config
- Enable Framebuffer Scaling (X and Y)
- Set Framebuffer Offset (X and Y)
- Set Framebuffer Blending
- Set Colour Key / Transparency
- Set ROI

[plane_ex_commit](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc_hw.c#L1768-L1863) and [gamma_ex_commit](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc_hw.c#L1548-L1574) are called by [dc_hw_commit](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_dc_hw.c#L2038-L2076)

# Call Flow for DC8200 Framebuffer Driver

Read the article...

-   ["RISC-V Star64 JH7110: Inside the Display Controller"](https://lupyuen.github.io/articles/display2)

At startup, [vs_drm_bind](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_drv.c#L193-L271) calls [vs_mode_config_init](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_fb.c#L178-L191) to register the Framebuffer Driver: [vs_mode_config_funcs](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_fb.c#L166-L172).

Which is defined as...

```c
static const struct drm_mode_config_funcs vs_mode_config_funcs = {
  .fb_create       = vs_fb_create,
  .get_format_info = vs_get_format_info,
  .output_poll_changed = drm_fb_helper_output_poll_changed,
  .atomic_check    = drm_atomic_helper_check,
  .atomic_commit   = drm_atomic_helper_commit,
};
```

[(Source)](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_fb.c#L166-L172)

[vs_fb_create](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_fb.c#L60-L123) is called by [drm_framebuffer](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/drm_framebuffer.c#L286-L329)

[vs_get_format_info](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_fb.c#L155-L164) is called by [drm_fourcc](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/drm_fourcc.c#L302-L325)

Framebuffer Formats: [vs_formats](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_fb.c#L134-L139)

# Call Flow for DC8200 Virtual Display Driver

TODO

```c
static const struct drm_connector_helper_funcs vd_connector_helper_funcs = {
  .get_modes    = vd_get_modes,
  .mode_valid   = vd_mode_valid,
  .best_encoder = vd_best_encoder,
};
```

[(Source)](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_virtual.c#L197-L201)

Display Resolutions: [vd_get_modes](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_virtual.c#L153-L181)

```c
static const struct drm_connector_funcs vd_connector_funcs = {
  .fill_modes = drm_helper_probe_single_connector_modes,
  .destroy    = vd_connector_destroy,
  .detect     = vd_connector_detect,
  .atomic_duplicate_state = drm_atomic_helper_connector_duplicate_state,
  .atomic_destroy_state   = drm_atomic_helper_connector_destroy_state,
  .reset = drm_atomic_helper_connector_reset,
};
```

[(Source)](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_virtual.c#L215-L222)

```c
const struct component_ops vd_component_ops = {
  .bind   = vd_bind,
  .unbind = vd_unbind,
};
```

[(Source)](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_virtual.c#L311-L314)

```c
// name = "vs-virtual-display"
struct platform_driver virtual_display_platform_driver = {
  .probe  = vd_probe,
  .remove = vd_remove,
  ...
};
```

[(Source)](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_virtual.c#L353-L360)

Display Pipelines:

```c
static const struct drm_crtc_funcs vs_crtc_funcs = {
  .set_config = drm_atomic_helper_set_config,
  .destroy    = vs_crtc_destroy,
  .page_flip  = drm_atomic_helper_page_flip,
  .reset      = vs_crtc_reset,
  .atomic_duplicate_state = vs_crtc_atomic_duplicate_state,
  .atomic_destroy_state   = vs_crtc_atomic_destroy_state,
  .atomic_set_property    = vs_crtc_atomic_set_property,
  .atomic_get_property    = vs_crtc_atomic_get_property,
  //.gamma_set    = drm_atomic_helper_legacy_gamma_set,
  .late_register  = vs_crtc_late_register,
  .enable_vblank  = vs_crtc_enable_vblank,
  .disable_vblank = vs_crtc_disable_vblank,
};
```

[(Source)](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_crtc.c#L207-L220)

Simple Encoder Driver:

```c
// name = "vs-simple-encoder"
struct platform_driver simple_encoder_driver = {
  .probe  = encoder_probe,
  .remove = encoder_remove,
  ...
};
```

[(Source)](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/vs_simple_enc.c#L300-L307)

# Call Flow for HDMI Controller Driver

TODO


```c
// name = "innohdmi-starfive"
struct platform_driver inno_hdmi_driver = {
  .probe  = inno_hdmi_probe,
  .remove = inno_hdmi_remove,
  ...
};
```

[(Source)](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/inno_hdmi.c#L1155-L1163)

```c
static const struct drm_encoder_helper_funcs inno_hdmi_encoder_helper_funcs = {
  .enable     = inno_hdmi_encoder_enable,
  .disable    = inno_hdmi_encoder_disable,
  .mode_fixup = inno_hdmi_encoder_mode_fixup,
  .mode_set   = inno_hdmi_encoder_mode_set,
  .atomic_check = inno_hdmi_encoder_atomic_check,
};
```

[(Source)](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/inno_hdmi.c#L651-L657)

MIPI DSI:

```c
// name = "dw-mipi-dsi"
struct platform_driver dw_mipi_dsi_driver = {
  .probe  = dsi_probe,
  .remove = dsi_remove,
  ...
};
```

[(Source)](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/dw_mipi_dsi.c#L1066-L1073)

```c
// name = "cdns-dsi"
static struct platform_driver cdns_dsi_platform_driver = {
  .probe  = cdns_dsi_drm_probe,
  .remove = cdns_dsi_drm_remove,
  ...
};
```

[(Source)](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/starfive_drm_dsi.c#L1679-L1687)

```c
static const struct component_ops dsi_component_ops = {
  .bind   = dsi_bind,
  .unbind = dsi_unbind,
};
```

[(Source)](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/dw_mipi_dsi.c#L998-L1001)

```c
static const struct drm_bridge_funcs dw_mipi_dsi_bridge_funcs = {
  .mode_set  = bridge_mode_set,
  .enable    = bridge_enable,
  .post_disable = bridge_post_disable,
  .attach     = bridge_attach,
  .mode_fixup = bridge_mode_fixup,
};
```

[(Source)](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/gpu/drm/verisilicon/dw_mipi_dsi.c#L869-L875)

# LCD Panel for Star64 JH7110

Also in the JH7110 Display Docs: How to connect an LCD Panel to JH7110.

JH7110's MIPI DSI Controller is [Cadence MIPI DSI v1.3.1 TX Controller IP (DSITX)](https://doc-en.rvspace.org/VisionFive2/DG_LCD/JH7110_SDK/ic_specification_lcd.html)...

![Cadence MIPI DSI v1.3.1 TX Controller IP (DSITX)](https://doc-en.rvspace.org/VisionFive2/DG_LCD/Image/JH7110_SDK/ic_spec.png)

[(Source)](https://doc-en.rvspace.org/VisionFive2/DG_LCD/JH7110_SDK/ic_specification_lcd.html)

JH7110's MIPI DPHY Controller is [MIPI DPHY M31 (M31DPHYRX611TL028D_00151501)](https://doc-en.rvspace.org/VisionFive2/DG_LCD/JH7110_SDK/ic_specification_lcd.html)...

![MIPI DPHY M31 (M31DPHYRX611TL028D_00151501)](https://doc-en.rvspace.org/VisionFive2/DG_LCD/Image/JH7110_SDK/MIPI_DPHY_M31.png)

[(Source)](https://doc-en.rvspace.org/VisionFive2/DG_LCD/JH7110_SDK/ic_specification_lcd.html)

Refer to the...

- [Linux Display Driver](https://doc-en.rvspace.org/VisionFive2/DG_LCD/JH7110_SDK/display_driver_locations_lcd.html)

- [Linux Device Tree](https://doc-en.rvspace.org/VisionFive2/DG_LCD/JH7110_SDK/device_tree_configuration_lcd.html)

See also the Sample LCD Panel Code for Seeed LCD Panel...

- [Enable LCD](https://doc-en.rvspace.org/VisionFive2/DG_LCD/JH7110_SDK/enable_lcd.html)

- [Disable LCD](https://doc-en.rvspace.org/VisionFive2/DG_LCD/JH7110_SDK/disable_lcd.html)

- [Obtain LCD Information](https://doc-en.rvspace.org/VisionFive2/DG_LCD/JH7110_SDK/obtain_lcd_information.html)

Here's the [LCD Initialisation Process](https://doc-en.rvspace.org/VisionFive2/DG_LCD/JH7110_SDK/initalization_lcd.html)

![LCD Initialisation Process](https://doc-en.rvspace.org/VisionFive2/DG_LCD/Image/JH7110_SDK/LCD_Init.svg)

[(Source)](https://doc-en.rvspace.org/VisionFive2/DG_LCD/JH7110_SDK/initalization_lcd.html)

And the [MIPI Parameter Configuration](https://doc-en.rvspace.org/VisionFive2/DG_LCD/JH7110_SDK/mipi_configuration.html) for 1C2L (2-lane MIPI DSI) and 1C4L (4-lane MIPI DSI).

# HDMI Driver for U-Boot Bootloader

We're building the NuttX HDMI Driver for Star64 JH7110 RISC-V SBC.

[__Justin (Fishwaldo)__](https://fosstodon.org/@Fishwaldo/110902984442385966) suggests that we check out the simpler HDMI Driver in __U-Boot Bootloader__...

- [__U-Boot Display Driver for JH7110__](https://github.com/starfive-tech/u-boot/tree/JH7110_VisionFive2_devel/drivers/video/starfive)

Here's our analysis of the Display Driver in U-Boot (which calls the HDMI Driver below):

- [sf_vop_probe](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/video/starfive/sf_vop.c#L657-L699): Call [sf_vop_power](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/video/starfive/sf_vop.c#L76-L112), [vout_probe_resources_jh7110](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/video/starfive/sf_vop.c#L250-L367) and [sf_display_init](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/video/starfive/sf_vop.c#L369-L655). Flush the dcache.

  TODO: Who calls [sf_vop_probe](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/video/starfive/sf_vop.c#L657-L699)?

- [sf_vop_power](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/video/starfive/sf_vop.c#L76-L112): Power on (Where is the code?)

- [vout_probe_resources_jh7110](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/video/starfive/sf_vop.c#L250-L367): Enable Clocks noc_disp, vout_src, top_vout_axi, top_vout_ahb, dc_pix0, dc_pix1, dc_axi, dc_core, dc_ahb, hdmitx0_pixelclk. Deassert Resets noc_disp, rst_vout_src, dc8200_rst_axi, dc8200_rst_core, dc8200_rst_ahb. (Similar to [Linux Driver vs_dc_enable](https://lupyuen.github.io/articles/display2#vs_dc_enable))

- [sf_display_init](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/video/starfive/sf_vop.c#L369-L655): Call [dc_hw_init](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/video/starfive/sf_vop.c#L237-L248), [device_probe](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/core/device.c#L484-L596) and [display_enable](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/video/display-uclass.c#L23-L40). Set Clock pix_src as pix0's parent. Set HDMI Clock Rate pix_src. Write to HDMI Registers.

  ([device_probe](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/core/device.c#L484-L596) calls [inno_hdmi_probe](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/video/starfive/sf_hdmi.c#L500-L541), which is explained below)

  ([display_enable](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/video/display-uclass.c#L23-L40) calls [inno_hdmi_enable](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/video/starfive/sf_hdmi.c#L444-L457), which is explained below)

- [dc_hw_init](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/video/starfive/sf_vop.c#L237-L248): Read Hardware Revision and Chip ID (similar to [Linux Driver dc_hw_init](https://lupyuen.github.io/articles/display2))

And here's our analysis of the HDMI Driver in U-Boot:

- [inno_hdmi_probe](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/video/starfive/sf_hdmi.c#L500-L541): Enable HDMI Clocks sys_clk, mclk, bclk. Read HDMI Status.

  ([inno_hdmi_probe](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/video/starfive/sf_hdmi.c#L500-L541) is called by [device_probe](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/core/device.c#L484-L596), which is called by [sf_display_init](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/video/starfive/sf_vop.c#L369-L655))

- [inno_hdmi_enable](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/video/starfive/sf_hdmi.c#L444-L457): Configure 1920x1080 60Hz. Power on HDMI Tx Phy and HDMI TDMS. Start Data Sync. Call [inno_hdmi_detect](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/video/starfive/sf_hdmi.c#L32-L58) and [inno_hdmi_tx_phy_param_config](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/video/starfive/sf_hdmi.c#L389-L425)

  ([inno_hdmi_enable](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/video/starfive/sf_hdmi.c#L444-L457) is called by [display_enable](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/video/display-uclass.c#L23-L40), which is called by [sf_display_init](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/video/starfive/sf_vop.c#L369-L655))

- [inno_hdmi_detect](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/video/starfive/sf_hdmi.c#L32-L58): Enable Pre-PLL, Post-PLL, LDO, Serializer

- [inno_hdmi_tx_phy_param_config](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/video/starfive/sf_hdmi.c#L389-L425): Call [inno_hdmi_config_1920x1080p60](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/video/starfive/sf_hdmi.c#L245-L288) and [inno_hdmi_tx_ctrl](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/video/starfive/sf_hdmi.c#L376-L387)

- [inno_hdmi_config_1920x1080p60](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/video/starfive/sf_hdmi.c#L245-L288): Config PLL for 1080p, 60hz

- [inno_hdmi_tx_ctrl](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/video/starfive/sf_hdmi.c#L376-L387): Config Video Format Identification Code. bist mode: 0x00, normal mode: 0x10, phy mode: 0x4

Here's the Device Tree for U-Boot:

- [starfive_visionfive2.dts](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/arch/riscv/dts/starfive_visionfive2.dts)

  Which includes [jh7110.dtsi](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/arch/riscv/dts/jh7110.dtsi)

- [starfive_visionfive2-u-boot.dtsi](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/arch/riscv/dts/starfive_visionfive2-u-boot.dtsi)

  Which includes [jh7110-u-boot.dtsi](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/arch/riscv/dts/jh7110-u-boot.dtsi)

From U-Boot Device Tree: [jh7110.dtsi](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/arch/riscv/dts/jh7110.dtsi#L1292-L1343)

```text
dc8200: dc8200@29400000 {
  compatible = "starfive,sf-dc8200";
  reg = 
    <0x0 0x29400000 0x0 0x100>,
    <0x0 0x29400800 0x0 0x2000>;
  reg-names = "hi", "low";
  status = "okay";

  clocks = 
    <&clkgen JH7110_NOC_BUS_CLK_DISP_AXI>,
    <&clkgen JH7110_VOUT_SRC>,
    <&clkgen JH7110_VOUT_TOP_CLK_VOUT_AXI>,
    <&clkgen JH7110_VOUT_TOP_CLK_VOUT_AHB>,
    <&clkvout JH7110_U0_DC8200_CLK_PIX0>,
    <&clkvout JH7110_U0_DC8200_CLK_PIX1>,
    <&clkvout JH7110_U0_DC8200_CLK_AXI>,
    <&clkvout JH7110_U0_DC8200_CLK_CORE>,
    <&clkvout JH7110_U0_DC8200_CLK_AHB>,
    <&clkvout JH7110_DOM_VOUT_TOP_LCD_CLK>,
    <&hdmitx0_pixelclk>,
    <&clkvout JH7110_DC8200_PIX0>,
    <&clkvout JH7110_U0_DC8200_CLK_PIX0_OUT>,
    <&clkvout JH7110_U0_DC8200_CLK_PIX1_OUT>;
  clock-names =
    "disp_axi","vout_src",
    "top_vout_axi","top_vout_ahb",
    "dc_pix0","dc_pix1",
    "dc_axi","dc_core","dc_ahb",
    "top_vout_lcd","hdmitx0_pixelclk","dc8200_pix0",
    "dc8200_pix0_out","dc8200_pix1_out";
  resets = 
    <&rstgen RSTN_U0_DOM_VOUT_TOP_SRC>,
    <&rstgen RSTN_U0_DC8200_AXI>,
    <&rstgen RSTN_U0_DC8200_AHB>,
    <&rstgen RSTN_U0_DC8200_CORE>,
    <&rstgen RSTN_U0_NOC_BUS_DISP_AXI_N>;
  reset-names =
    "rst_vout_src","rst_axi","rst_ahb","rst_core",
    "rst_noc_disp";
```

U-Boot Clocks and Resets Mapped Nicely:

| Clock Names | Clocks |
|:------------|:-------|  
| disp_axi / noc_disp | JH7110_NOC_BUS_CLK_DISP_AXI
| vout_src | JH7110_VOUT_SRC
| top_vout_axi | JH7110_VOUT_TOP_CLK_VOUT_AXI
| top_vout_ahb | JH7110_VOUT_TOP_CLK_VOUT_AHB
| dc_pix0 | JH7110_U0_DC8200_CLK_PIX0
| dc_pix1 | JH7110_U0_DC8200_CLK_PIX1
| dc_axi | JH7110_U0_DC8200_CLK_AXI
| dc_core | JH7110_U0_DC8200_CLK_CORE
| dc_ahb | JH7110_U0_DC8200_CLK_AHB
| top_vout_lcd | JH7110_DOM_VOUT_TOP_LCD_CLK
| hdmitx0_pixelclk | hdmitx0_pixelclk
| dc8200_pix0 | JH7110_DC8200_PIX0
| dc8200_pix0_out | JH7110_U0_DC8200_CLK_PIX0_OUT
| dc8200_pix1_out | JH7110_U0_DC8200_CLK_PIX1_OUT

| Reset Names | Resets |
|:------------|:-------|    
| rst_vout_src | RSTN_U0_DOM_VOUT_TOP_SRC
| rst_axi | RSTN_U0_DC8200_AXI
| rst_ahb | RSTN_U0_DC8200_AHB
| rst_core | RSTN_U0_DC8200_CORE
| rst_noc_disp | RSTN_U0_NOC_BUS_DISP_AXI_N

U-Boot Clocks are defined here: [clk-jh7110.c](https://github.com/starfive-tech/u-boot/blob/JH7110_VisionFive2_devel/drivers/clk/starfive/clk-jh7110.c)

From the Linux Device Tree: [jh7110.dtsi](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/arch/riscv/boot/dts/starfive/jh7110.dtsi#L339-L360)

```text
dc8200: dc8200@29400000 {
  compatible = "starfive,jh7110-dc8200","verisilicon,dc8200";
  verisilicon,dss-syscon = <&dssctrl>;//20220624 panel syscon
  reg =
    <0x0 0x29400000 0x0 0x100>,
    <0x0 0x29400800 0x0 0x2000>,
    <0x0 0x17030000 0x0 0x1000>;
  interrupts = <95>;
  status = "disabled";
  clocks =
    <&clkgen JH7110_NOC_BUS_CLK_DISP_AXI>,
    <&clkgen JH7110_VOUT_SRC>,
    <&clkgen JH7110_VOUT_TOP_CLK_VOUT_AXI>,
    <&clkgen JH7110_VOUT_TOP_CLK_VOUT_AHB>,
    <&clkvout JH7110_U0_DC8200_CLK_PIX0>,
    <&clkvout JH7110_U0_DC8200_CLK_PIX1>,
    <&clkvout JH7110_U0_DC8200_CLK_AXI>,
    <&clkvout JH7110_U0_DC8200_CLK_CORE>,
    <&clkvout JH7110_U0_DC8200_CLK_AHB>,
    <&clkgen JH7110_VOUT_TOP_CLK_VOUT_AXI>,
    <&clkvout JH7110_DOM_VOUT_TOP_LCD_CLK>,
    <&hdmitx0_pixelclk>,
    <&clkvout JH7110_DC8200_PIX0>,
    <&clkvout JH7110_U0_DC8200_CLK_PIX0_OUT>,
    <&clkvout JH7110_U0_DC8200_CLK_PIX1_OUT>;
  clock-names =
    "noc_disp","vout_src",
    "top_vout_axi","top_vout_ahb",
    "pix_clk","vout_pix1",
    "axi_clk","core_clk","vout_ahb",
    "vout_top_axi","vout_top_lcd","hdmitx0_pixelclk","dc8200_pix0",
    "dc8200_pix0_out","dc8200_pix1_out";
  resets = 
    <&rstgen RSTN_U0_DOM_VOUT_TOP_SRC>,
    <&rstgen RSTN_U0_DC8200_AXI>,
    <&rstgen RSTN_U0_DC8200_AHB>,
    <&rstgen RSTN_U0_DC8200_CORE>,
    <&rstgen RSTN_U0_NOC_BUS_DISP_AXI_N>;
  reset-names =
    "rst_vout_src","rst_axi","rst_ahb","rst_core",
    "rst_noc_disp";
};

clkvout: clock-controller@295C0000 {
  compatible = "starfive,jh7110-clk-vout";
  reg = <0x0 0x295C0000 0x0 0x10000>;
  reg-names = "vout";
  clocks = 
    <&hdmitx0_pixelclk>,
    <&mipitx_dphy_rxesc>,
    <&mipitx_dphy_txbytehs>,
    <&clkgen JH7110_VOUT_SRC>,
    <&clkgen JH7110_VOUT_TOP_CLK_VOUT_AHB>;
  clock-names =
    "hdmitx0_pixelclk",
    "mipitx_dphy_rxesc",
    "mipitx_dphy_txbytehs",
    "vout_src",
    "vout_top_ahb";
  resets = <&rstgen RSTN_U0_DOM_VOUT_TOP_SRC>;
  reset-names = "vout_src";
  #clock-cells = <1>;
  power-domains = <&pwrc JH7110_PD_VOUT>;
  status = "okay";
};
```

Linux Clocks and Resets Mapped Nicely:

| Clock Names | Clocks |
|:------------|:-------|  
|noc_disp | JH7110_NOC_BUS_CLK_DISP_AXI
|vout_src | JH7110_VOUT_SRC
|top_vout_axi | JH7110_VOUT_TOP_CLK_VOUT_AXI
|top_vout_ahb | JH7110_VOUT_TOP_CLK_VOUT_AHB
|pix_clk | JH7110_U0_DC8200_CLK_PIX0
|vout_pix1 | JH7110_U0_DC8200_CLK_PIX1
|axi_clk | JH7110_U0_DC8200_CLK_AXI
|core_clk | JH7110_U0_DC8200_CLK_CORE
|vout_ahb | JH7110_U0_DC8200_CLK_AHB
|vout_top_axi | JH7110_VOUT_TOP_CLK_VOUT_AXI
|vout_top_lcd | JH7110_DOM_VOUT_TOP_LCD_CLK
|hdmitx0_pixelclk | hdmitx0_pixelclk
|dc8200_pix0 | JH7110_DC8200_PIX0
|dc8200_pix0_out | JH7110_U0_DC8200_CLK_PIX0_OUT
|dc8200_pix1_out | JH7110_U0_DC8200_CLK_PIX1_OUT

| Reset Names | Resets |
|:------------|:-------|    
|rst_vout_src | RSTN_U0_DOM_VOUT_TOP_SRC
|rst_axi | RSTN_U0_DC8200_AXI
|rst_ahb | RSTN_U0_DC8200_AHB
|rst_core | RSTN_U0_DC8200_CORE
|rst_noc_disp | RSTN_U0_NOC_BUS_DISP_AXI_N

See the [JH7110 Memory Map](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/memory_map_display.html) and [Control Registers](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/controller_registers_display.html)

Based on [DOM VOUT CRG](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/dom_vout_crg.html), here are the Clock Registers and the Reset Register....

- clk_u0_dc8200_clk_axi: Offset 0x10
- clk_u0_dc8200_clk_core: Offset 0x14
- clk_u0_dc8200_clk_ahb: Offset 0x18
- clk_u0_dc8200_clk_pix0: Offset 0x1c
- clk_u0_dc8200_clk_pix1: Offset 0x20
- clk_dom_vout_top_lcd_clk: Offset 0x24
- clk_u0_cdns_dsiTx_clk_apb: Offset 0x28
- clk_u0_cdns_dsiTx_clk_sys: Offset 0x2c
- clk_u0_cdns_dsiTx_clk_dpi: Offset 0x30
- clk_u0_cdns_dsiTx_clk_txesc: Offset 0x34
- clk_u0_mipitx_dphy_clk_txesc: Offset 0x38
- clk_u0_hdmi_tx_clk_mclk: Offset 0x3c
- clk_u0_hdmi_tx_clk_bclk: Offset 0x40
- clk_u0_hdmi_tx_clk_sys: Offset 0x44
- Software_RESET_assert0_addr_assert_sel: Offset 0x38
  - Bit [0]	rstn_u0_dc8200_rstn_axi
    - 1: Assert reset
    - 0: De-assert reset

  - Bit [1]	rstn_u0_dc8200_rstn_ahb
    - 1: Assert reset
    - 0: De-assert reset

  - Bit [2]	rstn_u0_dc8200_rstn_core
    - 1: Assert reset
    - 0: De-assert reset

  - Bit [9]	rstn_u0_hdmi_tx_rstn_hdmi
    - 1: Assert reset
    - 0: De-assert reset

TODO: Reconcile the above drivers with the [Official Linux Driver](https://lupyuen.github.io/articles/display2)

TODO: Test on NuttX

TODO: Do we really need I2C for testing HDMI?

# Poking the Star64 JH7110 Display Controller with U-Boot Bootloader

![Star64 JH7110 Display Controller is alive!](https://lupyuen.github.io/images/display3-title.png)

In the olden days we would `peek` and `poke` the Display Controller, to see weird and wonderful displays.

Today (46 years later), we poke around the Display Controller of Star64 JH7110 SBC with a modern tool (not BASIC): U-Boot Bootloader!

(Spoiler: No weird and wonderful displays for today!)

Boot Star64 SBC without a microSD Card. Shut down our TFTP Server. We should see the U-Boot Prompt.

The `md` command dumps the JH7110 Memory: RAM, ROM, even I/O Registers!

```text
# md
md - memory display
Usage: md [.b, .w, .l, .q] address [# of objects]
```

We can dump the Boot ROM at `0x2A00` `0000`...

```text
# md 2A000000
2a000000: 00000297 12628293 30529073 30005073  ......b.s.R0sP.0
2a000010: 30405073 41014081 42014181 43014281  sP@0.@.A.A.B.B.C
2a000020: 44014381 45014481 46014581 47014681  .C.D.D.E.E.F.F.G
2a000030: 48014781 49014881 4a014981 4b014a81  .G.H.H.I.I.J.J.K
2a000040: 4c014b81 4d014c81 4e014d81 4f014e81  .K.L.L.M.M.N.N.O
2a000050: 01974f81 8193d710 02970ae1 82930000  .O..............
2a000060: 907305a2 02933052 85630010 50730402  ..s.R0....c...sP
2a000070: 22f37c14 02b2f140 d7102117 b8810113  .|."@....!......
2a000080: 40510133 25734581 1d63f140 033704b5  3.Q@.Es%@.c...7.
2a000090: 23b70110 30230110 03210003 fe734de3  ...#..#0..!..Ms.
2a0000a0: f0018293 f0018313 00628e63 f2018393  ........c.b.....
2a0000b0: 00737a63 0002be03 01c33023 032102a1  czs.....#0....!.
2a0000c0: fe736ae3 f2018313 d7101397 a9838393  .js.............
2a0000d0: 00737763 00033023 4de30321 00effe73  cws.#0..!..Ms...
2a0000e0: a81d61d0 10734621 00733046 26731050  .a..!Fs.F0s.P.s&
2a0000f0: 8a213440 04b7da7d 25730200 1913f140  @4!.}.....s%@...
```

(Where is the Source Code for JH7110 Boot ROM?)

We can dump the UART Registers at `0x1000` `0000`...

```text
# md 10000000
10000000: 0000006d 00000000 000000c1 00000003  m...............
10000010: 00000003 00000000 00000000 00000000  ................
10000020: 00000000 00000000 00000000 00000000  ................
10000030: 00000064 00000064 00000064 00000064  d...d...d...d...
10000040: 00000064 00000064 00000064 00000064  d...d...d...d...
10000050: 00000064 00000064 00000064 00000064  d...d...d...d...
10000060: 00000064 00000064 00000064 00000064  d...d...d...d...
10000070: 00000000 00000000 00000000 00000003  ................
10000080: 00000001 00000000 00000000 00000001  ................
10000090: 00000000 00000000 00000001 00000000  ................
100000a0: 00000000 00000000 00000000 00000000  ................
100000b0: 00000000 00000000 00000000 00000000  ................
100000c0: 00000000 00000000 00000000 00000000  ................
100000d0: 00000000 00000000 00000000 00000000  ................
100000e0: 00000000 00000000 00000000 00000000  ................
100000f0: 00000000 00000000 3331342a 44570110  ........*413..WD
```

Let's write to UART. The `mw` command writes to JH7110 Memory...

```text
# mw
mw - memory write (fill)
Usage: mw [.b, .w, .l, .q] address value [count]
```

(Hmmm sounds like a Security Risk)

Let's poke the UART Transmit Register at `0x1000` `0000`...

```text
# mw 10000000 2a 1
*
```

Yep it prints "`*`", which is ASCII Code 2A!

Based on the [JH7110 System Memory Map](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/system_memory_map.html), the Display Controller Registers are at...

- DC8200 AHB0: 0x2940_0000
- DC8200 AHB1: 0x2948_0000
- U0_HDMITX: 0x2959_0000
- VOUT_SYSCON: 0x295B_0000
- VOUT_CRG: 0x295C_0000
- DSI TX: 0x295D_0000
- MIPITX DPHY: 0x295E_0000

But the values are all zero!

```text
# md 29400000
29400000: 00000000 00000000 00000000 00000000  ................
29400010: 00000000 00000000 00000000 00000000  ................

# md 29480000
29480000: 00000000 00000000 00000000 00000000  ................
29480010: 00000000 00000000 00000000 00000000  ................

# md 29590000
29590000: 00000000 00000000 00000000 00000000  ................
29590010: 00000000 00000000 00000000 00000000  ................

# md 295B0000
295b0000: 00000000 00000000 00000000 00000000  ................
295b0010: 00000000 00000000 00000000 00000000  ................

# md 295C0000
295c0000: 00000000 00000000 00000000 00000000  ................
295c0010: 00000000 00000000 00000000 00000000  ................
```

Maybe because the Display Controller is not powered up?

Can we poke the PMU Registers and Clock and Reset Registers to power it up?

Let's find out...

# Power Management Registers for Star64 JH7110 Display Controller

_Can we poke the Power Management Registers to power up the Display Controller?_

From [JH7110 Power Management](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/overview_pm.html)...

![Power Management](https://doc-en.rvspace.org/JH7110/TRM/Image/RD/JH7110/power_stratey.png)

Display Controller (vout) is powered by the Power Domains...
- dom_dig
- dom_vout

_How to enable these Power Domains?_

We refer to the [Power Management Unit (PMU) Registers](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/register_info_pmu.html)

From [System Memory Map](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/system_memory_map.html), PMU is at 0x1703_0000...

```text
# md 17030000
17030000: 00000000 00000000 000000ff 00000003  ................
17030010: 00000000 0000ffff 04008402 04010040  ............@...
17030020: 00010040 00000000 00000000 00000000  @...............
17030030: 00000000 00000000 00000000 00000000  ................
17030040: 00000000 00000000 000007ff 00000012  ................
17030050: 0000001f ffffffff 00000001 00000003  ................
17030060: 00000000 00000000 00000080 00000000  ................
17030070: 00000000 00000000 00000000 00000000  ................
17030080: 00000003 00000000 00000203 00000000  ................
17030090: 00000020 00000003 000001c3 00000000   ...............
170300a0: 00000000 00000000 00000000 00000000  ................
170300b0: 00000000 00000000 00000000 00000000  ................
170300c0: 00000000 00000000 00000000 00000000  ................
170300d0: 00000000 00000000 00000000 00000000  ................
170300e0: 00000000 00000000 00000000 00000000  ................
170300f0: 00000000 00000000 00000000 00000000  ................
```

_Which Power Domains are already enabled?_

The [Current Power Mode Register](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/register_info_pmu.html) is at Offset Address 0x80. (Address 0x17030080)

From U-Boot Log above, Current Power Mode is 3, which means...
- Bit 0 (systop_power_mode): SYSTOP Power is Enabled
- Bit 1 (cpu_power_mode): CPU Power is Enabled
- But Bit 4 (vout_power_mode): VOUT Power is Disabled!

_How to enable VOUT Power?_

From [PMU Function Description](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/function_descript_pmu.html)...

> SW encourage Turn-on sequence:

> (1) Configure the register SW turn-on power mode (offset 0x0c), write the bit 1 which power domain will be turn-on, write the others 0;

> (2) Write the SW Turn-on command sequence. Write the register Software encourage (offset 0x44) 0xff –> 0x05 –> 0x50

Which is implemented in the Linux Driver (with no delays in the Command Sequence): [jh7110_pmu.c](https://github.com/starfive-tech/linux/blob/JH7110_VisionFive2_devel/drivers/soc/starfive/jh7110_pmu.c#L132-L147)

_What's a "Software Encourage"?_

Something got Lost in Translation. Let's assume it means "Software Trigger".

We do it in U-Boot like this...

```text
md 1703000c 1
mw 1703000c 0x10 1
md 1703000c 1

mw 17030044 0xff 1
mw 17030044 0x05 1
mw 17030044 0x50 1
```

Then we check status if VOUT Power is on...

```text
md 17030080 1
md 29400000 0x40
md 29480000 0x40
md 29590000 0x40
md 295B0000 0x40
md 295C0000 0x40
```

Here's the U-Boot Log...

```text
StarFive # md 1703000c 1
1703000c: 00000003                             ....
StarFive # mw 1703000c 0x10 1
StarFive # 
StarFive # md 1703000c 1
1703000c: 00000010                             ....
StarFive # md 17030080 1
17030080: 00000003                             ....
StarFive # mw 17030044 0xff 1
StarFive # 
StarFive # md 17030080 1
17030080: 00000003                             ....
StarFive # mw 17030044 0x05 1
StarFive # 
StarFive # md 17030080 1
17030080: 00000003                             ....
StarFive # mw 17030044 0x50 1
StarFive # 
StarFive # md 17030080 1
17030080: 00000013                             ....
```

_Is the Display Controller now powered up?_

From U-Boot Log above, the [Current Power Mode](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/register_info_pmu.html) (0x17030080) is 0x13, which means...

- Bit 0 (systop_power_mode): SYSTOP Power is Enabled
- Bit 1 (cpu_power_mode): CPU Power is Enabled
- Bit 4 (vout_power_mode): VOUT Power is Enabled

But the Display Controller Registers are still missing...

```text
StarFive # md 29400000 0x40
29400000: 00000000 00000000 00000000 00000000  ................
29400010: 00000000 00000000 00000000 00000000  ................
29400020: 00000000 00000000 00000000 00000000  ................
29400030: 00000000 00000000 00000000 00000000  ................
29400040: 00000000 00000000 00000000 00000000  ................
29400050: 00000000 00000000 00000000 00000000  ................
29400060: 00000000 00000000 00000000 00000000  ................
29400070: 00000000 00000000 00000000 00000000  ................
29400080: 00000000 00000000 00000000 00000000  ................
29400090: 00000000 00000000 00000000 00000000  ................
294000a0: 00000000 00000000 00000000 00000000  ................
294000b0: 00000000 00000000 00000000 00000000  ................
294000c0: 00000000 00000000 00000000 00000000  ................
294000d0: 00000000 00000000 00000000 00000000  ................
294000e0: 00000000 00000000 00000000 00000000  ................
294000f0: 00000000 00000000 00000000 00000000  ................
StarFive # md 29480000 0x40
29480000: 00000000 00000000 00000000 00000000  ................
29480010: 00000000 00000000 00000000 00000000  ................
29480020: 00000000 00000000 00000000 00000000  ................
29480030: 00000000 00000000 00000000 00000000  ................
29480040: 00000000 00000000 00000000 00000000  ................
29480050: 00000000 00000000 00000000 00000000  ................
29480060: 00000000 00000000 00000000 00000000  ................
29480070: 00000000 00000000 00000000 00000000  ................
29480080: 00000000 00000000 00000000 00000000  ................
29480090: 00000000 00000000 00000000 00000000  ................
294800a0: 00000000 00000000 00000000 00000000  ................
294800b0: 00000000 00000000 00000000 00000000  ................
294800c0: 00000000 00000000 00000000 00000000  ................
294800d0: 00000000 00000000 00000000 00000000  ................
294800e0: 00000000 00000000 00000000 00000000  ................
294800f0: 00000000 00000000 00000000 00000000  ................
StarFive # md 29590000 0x40
29590000: 00000000 00000000 00000000 00000000  ................
29590010: 00000000 00000000 00000000 00000000  ................
29590020: 00000000 00000000 00000000 00000000  ................
29590030: 00000000 00000000 00000000 00000000  ................
29590040: 00000000 00000000 00000000 00000000  ................
29590050: 00000000 00000000 00000000 00000000  ................
29590060: 00000000 00000000 00000000 00000000  ................
29590070: 00000000 00000000 00000000 00000000  ................
29590080: 00000000 00000000 00000000 00000000  ................
29590090: 00000000 00000000 00000000 00000000  ................
295900a0: 00000000 00000000 00000000 00000000  ................
295900b0: 00000000 00000000 00000000 00000000  ................
295900c0: 00000000 00000000 00000000 00000000  ................
295900d0: 00000000 00000000 00000000 00000000  ................
295900e0: 00000000 00000000 00000000 00000000  ................
295900f0: 00000000 00000000 00000000 00000000  ................
StarFive # md 295B0000 0x40
295b0000: 00000000 00000000 00000000 00000000  ................
295b0010: 00000000 00000000 00000000 00000000  ................
295b0020: 00000000 00000000 00000000 00000000  ................
295b0030: 00000000 00000000 00000000 00000000  ................
295b0040: 00000000 00000000 00000000 00000000  ................
295b0050: 00000000 00000000 00000000 00000000  ................
295b0060: 00000000 00000000 00000000 00000000  ................
295b0070: 00000000 00000000 00000000 00000000  ................
295b0080: 00000000 00000000 00000000 00000000  ................
295b0090: 00000000 00000000 00000000 00000000  ................
295b00a0: 00000000 00000000 00000000 00000000  ................
295b00b0: 00000000 00000000 00000000 00000000  ................
295b00c0: 00000000 00000000 00000000 00000000  ................
295b00d0: 00000000 00000000 00000000 00000000  ................
295b00e0: 00000000 00000000 00000000 00000000  ................
295b00f0: 00000000 00000000 00000000 00000000  ................
StarFive # md 295C0000 0x40
295c0000: 00000000 00000000 00000000 00000000  ................
295c0010: 00000000 00000000 00000000 00000000  ................
295c0020: 00000000 00000000 00000000 00000000  ................
295c0030: 00000000 00000000 00000000 00000000  ................
295c0040: 00000000 00000000 00000000 00000000  ................
295c0050: 00000000 00000000 00000000 00000000  ................
295c0060: 00000000 00000000 00000000 00000000  ................
295c0070: 00000000 00000000 00000000 00000000  ................
295c0080: 00000000 00000000 00000000 00000000  ................
295c0090: 00000000 00000000 00000000 00000000  ................
295c00a0: 00000000 00000000 00000000 00000000  ................
295c00b0: 00000000 00000000 00000000 00000000  ................
295c00c0: 00000000 00000000 00000000 00000000  ................
295c00d0: 00000000 00000000 00000000 00000000  ................
295c00e0: 00000000 00000000 00000000 00000000  ................
295c00f0: 00000000 00000000 00000000 00000000  ................
StarFive # 
```

Let's poke the Clock and Reset Registers...

# Clock and Reset Registers for Star64 JH7110 Display Controller

_VOUT Power is already enabled via PMU. How do we poke the Clock and Reset Registers to power up the Display Controller?_

Based on the [JH7110 Clock Structure](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/clock_structure.html)...

![Clock Structure](https://doc-en.rvspace.org/JH7110/TRM/Image/Drawing/Clock_Structure.svg)

Display Controller (vout_crg, top left) is clocked and reset by...
- clk_vout_root
- mipiphy ref clk
- hdmiphy ref clk
- clk_vout_src (1228.8M)
- clk_vout_axi (614.4M)
- clk_vout_ahb (204.8M)（clk_ahb1）
- clk_mclk (51.2M)
- rstn_vout

_How to enable the above clocks and deassert the above reset?_

We refer to the [System Clock and Reset (SYS CRG) Registers](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/sys_crg.html).

From [System Memory Map](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/system_memory_map.html), System CRG is at 0x1302_0000...

```text
# md 13020000
13020000: 01000000 00000001 00000002 00000000  ................
13020010: 01000002 01000000 00000003 00000003  ................
13020020: 00000002 80000000 80000000 00000004  ................
13020030: 80000000 00000002 00000002 00000002  ................
13020040: 00000002 0000000c 00000000 00000000  ................
13020050: 00000002 00000002 80000014 80000010  ................
13020060: 8000000c 80000000 80000000 80000000  ................
13020070: 80000000 80000000 80000000 00000006  ................
13020080: 80000000 80000000 80000000 80000000  ................
13020090: 80000000 80000000 80000000 80000000  ................
130200a0: 00000002 00000002 00000002 01000000  ................
130200b0: 80000000 00000003 00000000 00000000  ................
130200c0: 00000000 0000000c 00000000 00000000  ................
130200d0: 00000000 80000000 00000003 00000002  ................
130200e0: 80000000 80000000 00000000 00000002  ................
130200f0: 00000000 00000000 00000000 00000000  ................
```

TODO: Which Clocks and Registers are already enabled / deasserted?

Based on the [System Control Registers](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/sys_crg.html), we need to enable these clocks...
- Clock AHB 1: Offset  0x28
- MCLK Out: Offset  0x4c
- clk_u0_sft7110_noc_bus_clk_cpu_axi: Offset  0x98
- clk_u0_sft7110_noc_bus_clk_axicfg0_axi: Offset  0x9c
- clk_u0_dom_vout_top_clk_dom_vout_top_clk_vout_src: Offset  0xe8
- Clock NOC Display AXI: Offset  0xf0
- Clock Video Output AHB: Offset  0xf4
- Clock Video Output AXI: Offset  0xf8
- Clock Video Output HDMI TX0 MCLK: Offset  0xfc

(OK looks excessive, but better to enable more clocks than too few!)

For the Clock Registers above, we should set Bit 31 (clk_icg) to 1...
- 1: Clock enable
- 0: Clock disable

Here are the U-Boot Commands to enable the clocks...

```text
md 13020028 1
mw 13020028 0x80000000 1
md 13020028 1

md 1302004c 1
mw 1302004c 0x80000000 1
md 1302004c 1

md 13020098 1
mw 13020098 0x80000000 1
md 13020098 1

md 1302009c 1
mw 1302009c 0x80000000 1
md 1302009c 1

md 130200e8 1
mw 130200e8 0x80000000 1
md 130200e8 1

md 130200f0 1
mw 130200f0 0x80000000 1
md 130200f0 1

md 130200f4 1
mw 130200f4 0x80000000 1
md 130200f4 1

md 130200f8 1
mw 130200f8 0x80000000 1
md 130200f8 1

md 130200fc 1
mw 130200fc 0x80000000 1
md 130200fc 1
```

Here's the U-Boot Log...

```text
StarFive # md 13020028 1
13020028: 80000000                             ....
StarFive # mw 13020028 0x80000000 1
StarFive # 
StarFive # md 13020028 1
13020028: 80000000                             ....
StarFive # md 1302004c 1
1302004c: 00000000                             ....
StarFive # mw 1302004c 0x80000000 1
StarFive # 
StarFive # md 1302004c 1
1302004c: 80000000                             ....
StarFive # md 13020098 1
13020098: 80000000                             ....
StarFive # mw 13020098 0x80000000 1
StarFive # 
StarFive # md 13020098 1
13020098: 80000000                             ....
StarFive # md 1302009c 1
1302009c: 80000000                             ....
StarFive # mw 1302009c 0x80000000 1
StarFive # 
StarFive # md 1302009c 1
1302009c: 80000000                             ....
StarFive # md 130200e8 1
130200e8: 00000000                             ....
StarFive # mw 130200e8 0x80000000 1
StarFive # 
StarFive # md 130200e8 1
130200e8: 80000000                             ....
StarFive # md 130200f0 1
130200f0: 00000000                             ....
StarFive # mw 130200f0 0x80000000 1
StarFive # 
StarFive # md 130200f0 1
130200f0: 80000000                             ....
StarFive # md 130200f4 1
130200f4: 00000000                             ....
StarFive # mw 130200f4 0x80000000 1
StarFive # 
StarFive # md 130200f4 1
130200f4: 80000000                             ....
StarFive # md 130200f8 1
130200f8: 00000000                             ....
StarFive # mw 130200f8 0x80000000 1
StarFive # 
StarFive # md 130200f8 1
130200f8: 80000000                             ....
StarFive # md 130200fc 1
130200fc: 00000000                             ....
StarFive # mw 130200fc 0x80000000 1
StarFive # 
StarFive # md 130200fc 1
130200fc: 80000000                             ....
StarFive # 
```

_What about the Resets?_

Based on the [System Control Registers](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/sys_crg.html), we need to deassert these resets...

- Software RESET 1 Address Selector: Offset 0x2fc

  Bit 11: rstn_u0_dom_vout_top_rstn_dom_vout_top_rstn_vout_src
  - 1: Assert reset
  - 0: De-assert reset

- SYSCRG RESET Status 0: Offset 0x308

  Bit 26: rstn_u0_sft7110_noc_bus_reset_disp_axi_n
  - 1: Assert reset
  - 0: De-assert reset

- SYSCRG RESET Status 1: Offset 0x30c

  Bit 11: rstn_u0_dom_vout_top_rstn_dom_vout_top_rstn_vout_src
  - 1: Assert reset
  - 0: De-assert reset

These are the U-Boot Commands to Deassert the above Resets...

```text
md 130202fc 1
mw 130202fc 0x7e7f600 1
md 130202fc 1

md 13020308 1
mw 13020308 0xfb9fffff 1
md 13020308 1

md 1302030c 1
```

(The last one is already deasserted, no need to change it)

Then we check the Display Registers...

```text
md 29400000 0x20
md 29480000 0x20
md 29590000 0x20
md 295B0000 0x20
md 295C0000 0x20
```

Here's the U-Boot Log...

```text
StarFive # md 1703000c 1
1703000c: 00000003                             ....
StarFive # mw 1703000c 0x10 1
StarFive # 
StarFive # md 1703000c 1
1703000c: 00000010                             ....
StarFive # mw 17030044 0xff 1
StarFive # 
StarFive # mw 17030044 0x05 1
StarFive # 
StarFive # mw 17030044 0x50 1
StarFive # 
StarFive # md 17030080 1
17030080: 00000013                             ....
StarFive # mw 13020028 0x80000000 1
StarFive # 
StarFive # mw 1302004c 0x80000000 1
StarFive # 
StarFive # mw 13020098 0x80000000 1
StarFive # 
StarFive # mw 1302009c 0x80000000 1
StarFive # 
StarFive # mw 130200e8 0x80000000 1
StarFive # 
StarFive # mw 130200f0 0x80000000 1
StarFive # 
StarFive # mw 130200f4 0x80000000 1
StarFive # 
StarFive # mw 130200f8 0x80000000 1
StarFive # 
StarFive # mw 130200fc 0x80000000 1
StarFive # 
StarFive # mw 130202fc 0x7e7f600 1
StarFive # 
StarFive # mw 13020308 0xfb9fffff 1
StarFive # 
StarFive # md 295B0000 0x40
295b0000: 00000000 000b0000 00000000 00000000  ................
295b0010: 00000000 00000000 00000000 00000000  ................
295b0020: 00000000 00000000 00000000 00000000  ................
295b0030: 00000000 00000000 00000000 00000000  ................
295b0040: 00000000 00000000 00000000 00000000  ................
295b0050: 00000000 00000000 00000000 00000000  ................
295b0060: 00000000 00000000 00000000 00000000  ................
295b0070: 00000000 00000000 00000000 00000000  ................
295b0080: 00000000 00000000 00000000 00000000  ................
295b0090: 00000000 00000000 00000000 00000000  ................
295b00a0: 00000000 00000000 00000000 00000000  ................
295b00b0: 00000000 00000000 00000000 00000000  ................
295b00c0: 00000000 00000000 00000000 00000000  ................
295b00d0: 00000000 00000000 00000000 00000000  ................
295b00e0: 00000000 00000000 00000000 00000000  ................
295b00f0: 00000000 00000000 00000000 00000000  ................
StarFive # md 295C0000 0x40
295c0000: 00000004 00000004 00000004 0000000c  ................
295c0010: 00000000 00000000 00000000 00000000  ................
295c0020: 00000000 00000000 00000000 00000000  ................
295c0030: 00000000 00000000 00000000 00000000  ................
295c0040: 00000000 00000000 00000fff 00000000  ................
295c0050: 00000000 00000000 00000000 00000000  ................
295c0060: 00000000 00000000 00000000 00000000  ................
295c0070: 00000000 00000000 00000000 00000000  ................
295c0080: 00000000 00000000 00000000 00000000  ................
295c0090: 00000000 00000000 00000000 00000000  ................
295c00a0: 00000000 00000000 00000000 00000000  ................
295c00b0: 00000000 00000000 00000000 00000000  ................
295c00c0: 00000000 00000000 00000000 00000000  ................
295c00d0: 00000000 00000000 00000000 00000000  ................
295c00e0: 00000000 00000000 00000000 00000000  ................
295c00f0: 00000000 00000000 00000000 00000000  ................
StarFive # 
```

The Display Controller Registers are now visible at VOUT_CRG (0x295C_0000) yay!

Which means Display Controller is alive yay!

![Star64 JH7110 Display Controller is alive!](https://lupyuen.github.io/images/display3-title.png)

The Default Values seem to match [DOM VOUT CRG](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/dom_vout_crg.html).

(`clk_tx_esc` should have default `24'hc`, there is a typo in the doc: `24'h12`)

![`clk_tx_esc` should have default `24'hc`, there is a typo in the doc: `24'h12`](https://lupyuen.github.io/images/display3-typo.png)

FYI: It hangs when we read U0_HDMITX at 0x2959_0000. Probably because Display Controller is actually powered up.

```text
StarFive # mw 13020028 0x80000000 1
StarFive # 
StarFive # mw 1302004c 0x80000000 1
StarFive # 
StarFive # mw 13020098 0x80000000 1
StarFive # 
StarFive # mw 1302009c 0x80000000 1
StarFive # 
StarFive # mw 130200e8 0x80000000 1
StarFive # 
StarFive # mw 130200f0 0x80000000 1
StarFive # 
StarFive # mw 130200f4 0x80000000 1
StarFive # 
StarFive # mw 130200f8 0x80000000 1
StarFive # 
StarFive # mw 130200fc 0x80000000 1
StarFive # 
StarFive # mw 130202fc 0x7e7f600 1
StarFive # 
StarFive # mw 13020308 0xfb9fffff 1
StarFive # 
StarFive # md 29400000 0x40
29400000: 00000000 00000000 00000000 00000000  ................
29400010: 00000000 00000000 00000000 00000000  ................
29400020: 00000000 00000000 00000000 00000000  ................
29400030: 00000000 00000000 00000000 00000000  ................
29400040: 00000000 00000000 00000000 00000000  ................
29400050: 00000000 00000000 00000000 00000000  ................
29400060: 00000000 00000000 00000000 00000000  ................
29400070: 00000000 00000000 00000000 00000000  ................
29400080: 00000000 00000000 00000000 00000000  ................
29400090: 00000000 00000000 00000000 00000000  ................
294000a0: 00000000 00000000 00000000 00000000  ................
294000b0: 00000000 00000000 00000000 00000000  ................
294000c0: 00000000 00000000 00000000 00000000  ................
294000d0: 00000000 00000000 00000000 00000000  ................
294000e0: 00000000 00000000 00000000 00000000  ................
294000f0: 00000000 00000000 00000000 00000000  ................
StarFive # md 29480000 0x40
29480000: 00000000 00000000 00000000 00000000  ................
29480010: 00000000 00000000 00000000 00000000  ................
29480020: 00000000 00000000 00000000 00000000  ................
29480030: 00000000 00000000 00000000 00000000  ................
29480040: 00000000 00000000 00000000 00000000  ................
29480050: 00000000 00000000 00000000 00000000  ................
29480060: 00000000 00000000 00000000 00000000  ................
29480070: 00000000 00000000 00000000 00000000  ................
29480080: 00000000 00000000 00000000 00000000  ................
29480090: 00000000 00000000 00000000 00000000  ................
294800a0: 00000000 00000000 00000000 00000000  ................
294800b0: 00000000 00000000 00000000 00000000  ................
294800c0: 00000000 00000000 00000000 00000000  ................
294800d0: 00000000 00000000 00000000 00000000  ................
294800e0: 00000000 00000000 00000000 00000000  ................
294800f0: 00000000 00000000 00000000 00000000  ................
StarFive # md 29590000 0x40
```

# Automate U-Boot to Power Up Display Controller

_That's a long list of U-Boot Commands. Can we automate this?_

```text
mw 1703000c 0x10 1
mw 17030044 0xff 1
mw 17030044 0x05 1
mw 17030044 0x50 1
mw 13020028 0x80000000 1
mw 1302004c 0x80000000 1
mw 13020098 0x80000000 1
mw 1302009c 0x80000000 1
mw 130200e8 0x80000000 1
mw 130200f0 0x80000000 1
mw 130200f4 0x80000000 1
mw 130200f8 0x80000000 1
mw 130200fc 0x80000000 1
mw 130202fc 0x7e7f600 1
mw 13020308 0xfb9fffff 1
md 295C0000 0x20
```

Sure can! Run this in U-Boot...

```text
## Create the command to power up the Display Controller
setenv display_on 'mw 1703000c 0x10 1 ; mw 17030044 0xff 1 ; mw 17030044 0x05 1 ; mw 17030044 0x50 1 ; mw 13020028 0x80000000 1 ; mw 1302004c 0x80000000 1 ; mw 13020098 0x80000000 1 ; mw 1302009c 0x80000000 1 ; mw 130200e8 0x80000000 1 ; mw 130200f0 0x80000000 1 ; mw 130200f4 0x80000000 1 ; mw 130200f8 0x80000000 1 ; mw 130200fc 0x80000000 1 ; mw 130202fc 0x7e7f600 1 ; mw 13020308 0xfb9fffff 1 ; md 295C0000 0x20 ; '

## Check that it's correct
printenv display_on

## Save it for future reboots
saveenv

## Run the command to power up the Display Controller
run display_on
```

(The `run` feels a bit like BASIC)

We should see...

```text
StarFive # run display_on
295c0000: 00000004 00000004 00000004 0000000c  ................
295c0010: 00000000 00000000 00000000 00000000  ................
295c0020: 00000000 00000000 00000000 00000000  ................
295c0030: 00000000 00000000 00000000 00000000  ................
295c0040: 00000000 00000000 00000fff 00000000  ................
295c0050: 00000000 00000000 00000000 00000000  ................
295c0060: 00000000 00000000 00000000 00000000  ................
295c0070: 00000000 00000000 00000000 00000000  ................
```

So much easier!

Maybe we could use this to render something to the HDMI Display!

(Before converting to C for NuttX)

_How will we test this in NuttX?_

Probably inside `board_late_initialize` like this: [jh7110_appinit.c](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/hdmi/boards/risc-v/jh7110/star64/src/jh7110_appinit.c#L154-L215)

```c
void board_late_initialize(void) {
  /* Mount the RAM Disk */
  mount_ramdisk();

  /* Perform board-specific initialization */
#ifdef CONFIG_NSH_ARCHINIT
  mount(NULL, "/proc", "procfs", 0, NULL);
#endif

  // Verfy that Display Controller is down
  uint32_t val = getreg32(0x295C0000);
  DEBUGASSERT(val == 0);

  // Power up the Display Controller
  // TODO: Switch to constants
  putreg32(0x10, 0x1703000c);
  putreg32(0xff, 0x17030044);
  putreg32(0x05, 0x17030044);
  putreg32(0x50, 0x17030044);
  putreg32(0x80000000, 0x13020028);
  putreg32(0x80000000, 0x1302004c);
  putreg32(0x80000000, 0x13020098);
  putreg32(0x80000000, 0x1302009c);
  putreg32(0x80000000, 0x130200e8);
  putreg32(0x80000000, 0x130200f0);
  putreg32(0x80000000, 0x130200f4);
  putreg32(0x80000000, 0x130200f8);
  putreg32(0x80000000, 0x130200fc);

  // Software RESET 1 Address Selector: Offset 0x2fc
  // Clear Bit 11: rstn_u0_dom_vout_top_rstn_dom_vout_top_rstn_vout_src
  modifyreg32(0x130202fc, 1 << 11, 0);  // Addr, Clear Bits, Set Bits

  // SYSCRG RESET Status 0: Offset 0x308
  // Clear Bit 26: rstn_u0_sft7110_noc_bus_reset_disp_axi_n
  modifyreg32(0x13020308, 1 << 26, 0);  // Addr, Clear Bits, Set Bits

  // Verfy that Display Controller is up
  val = getreg32(0x295C0000);
  DEBUGASSERT(val == 4);

  // Test HDMI
  int test_hdmi(void);
  int ret = test_hdmi();
  DEBUGASSERT(ret == 0);
}

// Display Subsystem Base Address
// https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/memory_map_display.html
#define DISPLAY_BASE_ADDRESS (0x29400000)

// DOM VOUT Control Registers
// https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/memory_map_display.html
#define CRG_BASE_ADDRESS     (DISPLAY_BASE_ADDRESS + 0x1C0000)

// Enable Clock
// https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/dom_vout_crg.html
#define CLK_ICG (1 << 31)

// https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/dom_vout_crg.html
#define clk_u0_dc8200_clk_pix0 (CRG_BASE_ADDRESS + 0x1c)

// Test HDMI
int test_hdmi(void) { ... }
```

# JH7110 System Configuration Registers

TODO

[SYS SYSCON: System Configuration Registers](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/sys_syscon.html)

From [System Memory Map](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/system_memory_map.html), System SYSCON is at 0x1303_0000

```text
# md 13030000
13030000: 00000000 00000000 00000000 00000000  ................
13030010: 00000000 00d54d54 034fea80 0000007d  ....TM....O.}...
13030020: 45555555 042ba603 45e00000 00c7a60c  UUUE..+....E....
13030030: 45333333 00000002 00000000 00000000  333E............
13030040: 00000000 00000000 00000000 00000000  ................
13030050: 00000000 00000000 00000000 00000000  ................
13030060: 00000002 00000000 2a000000 00000000  ...........*....
13030070: 2a000000 00000000 2a000000 00000000  ...*.......*....
13030080: 2a000000 01aa8000 00000d54 6aa00000  ...*....T......j
13030090: 00000004 00000000 00000000 00042600  .............&..
130300a0: 00000000 00000000 00000000 00000000  ................
130300b0: 00000000 00000000 00000000 00000000  ................
130300c0: 00000000 00000000 00000000 00000000  ................
130300d0: 00000000 00000000 00000000 00000000  ................
130300e0: 00000000 00000000 00000000 00000000  ................
130300f0: 00000000 00000000 00000000 00000000  ................
```

TODO: Which SYSCON Registers are already configured?

# JH7110 Bus Connection

TODO

From [Bus Connection](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/bus_connection.html):

![Bus Connection](https://doc-en.rvspace.org/JH7110/TRM/Image/RD/JH7110/stg_mtrx_connection17.png)

TODO: Do we need to bother with Bus Connections?

# PineTab-V Factory Test Code

The PineTab-V ships with [Factory Test Code](https://wiki.pine64.org/wiki/PineTab-V_Releases#Factory_releases).

> ![PineTab-V Factory Test Code](https://lupyuen.github.io/images/pinetabv-factory.jpg)

The factory test reference source code has been mirrored here (for quicker downloading)...

- [PineTab-V_factorytestcode_SDK-20230725.tar.gz](https://drive.google.com/file/d/1OZkcGFVvyTn36JLebxT9_89blbOHM5ON/view?usp=drive_link)

Let's look inside the Factory Test Code...

# PineTab-V Device Tree

[(__LCD Panel in PineTab-V__ is actually BOE TH101MB31IG002-28A)](https://fosstodon.org/@Fishwaldo/110902984462760802)

Inside the PineTab-V Factory Test Code (from previous section), we see the PineTab-V Device Tree for Linux:

[VisionFive2/linux/arch/riscv/boot/dts/starfive/jh7110-visionfive-v2.dtsi](https://github.com/lupyuen/nuttx-star64/blob/main/pinetabv-jh7110-visionfive-v2.dtsi)

From the above Device Tree we see the LCD Panel (StarFive Jadard on MIPI DSI1) and Touch Panel (Goodix GT911)...

```text
&i2c2 {
  clock-frequency = <100000>;
  i2c-sda-hold-time-ns = <300>;
  i2c-sda-falling-time-ns = <510>;
  i2c-scl-falling-time-ns = <510>;
  auto_calc_scl_lhcnt;
  status = "okay";
  ...
  panel_radxa@19 {
    status = "okay";
    compatible ="starfive_jadard";
    reg = <0x19>;
    //reset-gpio = <&gpio 23 0>;
    blen-gpio = <&gpio 45 0>;
    enable-gpio = <&gpio 37 0>;

    port {
      panel_out1: endpoint {
        remote-endpoint = <&dsi1_output>;
        };
    };
  };

  touchscreen@14 {
    status = "okay";
    compatible = "goodix,gt911";
    reg = <0x14>;
    irq-gpios = <&gpio 30 GPIO_ACTIVE_HIGH>;
    reset-gpios = <&gpio 31 GPIO_ACTIVE_HIGH>;
  };
};
```

Which maps to this Linux Driver for StarFive Jadard Display Panel: (which one?)

- er88577b: [VisionFive2/linux/drivers/gpu/drm/panel/panel-er88577b.c](https://github.com/lupyuen/nuttx-star64/blob/main/panel-er88577b.c)

- jd9365da-h3: [VisionFive2/linux/drivers/gpu/drm/panel/panel-jadard-jd9365da-h3.c](https://github.com/lupyuen/nuttx-star64/blob/main/panel-jadard-jd9365da-h3.c)

StarFive Jadard is also mentioned in [JH7110 MIPI LCD Developing and Porting Guide](https://doc-en.rvspace.org/VisionFive2/DG_LCD/JH7110_SDK/configuration_for_1c4l_port.html)

We also see the Galaxycore GC02M2 Camera (on MIPI CSI)...

```text
&gpio {
  ...
  gc02m2_pins: gc02m2_pins {
    gc02m2pins-pwdn {
      starfive,pins = <PAD_GPIO25>;
      starfive,pinmux = <PAD_GPIO25_FUNC_SEL 0>;
      starfive,pin-ioconfig = <IO(GPIO_IE(1))>;
      starfive,pin-gpio-dout = <GPO_HIGH>;
      starfive,pin-gpio-doen = <OEN_LOW>;
    };

    gc02m2_pins-rst {
      starfive,pins = <PAD_GPIO33>;
      starfive,pinmux = <PAD_GPIO33_FUNC_SEL 0>;
      starfive,pin-ioconfig = <IO(GPIO_IE(1))>;
      starfive,pin-gpio-dout = <GPO_HIGH>;
      starfive,pin-gpio-doen = <OEN_LOW>;
    };

    // gc02m2_pins-sw {
    //   starfive,pins = <PAD_GPIO53>;
    //   starfive,pinmux = <PAD_GPIO53_FUNC_SEL 0>;
    //   starfive,pin-ioconfig = <IO(GPIO_IE(1))>;
    //   starfive,pin-gpio-dout = <GPO_LOW>;
    //   starfive,pin-gpio-doen = <OEN_LOW>;
    // };
  };
  ...
&i2c6 {
  clock-frequency = <100000>;
  i2c-sda-hold-time-ns = <300>;
  i2c-sda-falling-time-ns = <510>;
  i2c-scl-falling-time-ns = <510>;
  auto_calc_scl_lhcnt;
  pinctrl-names = "default";
  pinctrl-0 = <&i2c6_pins>;
  status = "okay";
  ...
  gc02m2: gc02m2@37 {
    status = "okay";
    compatible = "galaxycore,gc02m2";
    pinctrl-names = "default";
    pinctrl-0 = <&gc02m2_pins>;
    reg = <0x37>;
    clocks = <&clk_ext_camera>;
    clock-names = "xvclk";
    reset-gpio = <&gpio 33 GPIO_ACTIVE_HIGH>;
    pwdn-gpio = <&gpio 25 GPIO_ACTIVE_LOW>;
    // sw-gpios = <&gpio 53 GPIO_ACTIVE_LOW>;

    port {
      gc02m2_to_csi2rx0: endpoint {
        remote-endpoint = <&csi2rx0_from_gc02m2>;
        bus-type = <4>;      /* MIPI CSI-2 D-PHY */
        data-lanes = <1>;
        link-frequencies = /bits/ 64 <336000000>;
      };
    };
  };
};
...
&vin_sysctl {
  /* when use dvp open this pinctrl*/
  status = "okay";

  ports {
    #address-cells = <1>;
    #size-cells = <0>;

    port@1 {
      reg = <1>;
      #address-cells = <1>;
      #size-cells = <0>;
      ...
      csi2rx0_from_gc02m2: endpoint@1 {
        reg = <1>;
        remote-endpoint = <&gc02m2_to_csi2rx0>;
        bus-type = <4>;      /* MIPI CSI-2 D-PHY */
        clock-lanes = <0>;
        data-lanes = <2 1>;
        lane-polarities = <0 0 0>;
        status = "okay";
      };
    };
  };
};
```

# RAM Disk Address for RISC-V QEMU

Read the article...

-   ["Star64 JH7110 + NuttX RTOS: RISC-V Semihosting and Initial RAM Disk"](https://lupyuen.github.io/articles/semihost)

_Can we enable logging for RISC-V QEMU?_

Yep we use the `-trace "*"` option like this...

```bash
qemu-system-riscv64 \
  -semihosting \
  -M virt,aclint=on \
  -cpu rv64 \
  -smp 8 \
  -bios none \
  -kernel nuttx \
  -initrd initrd \
  -nographic \
  -trace "*"
```

In the QEMU Command above we loaded the Initial RAM Disk `initrd`.

To discover the RAM Address of the Initial RAM Disk, we check the QEMU Trace Log:

```text
resettablloader_write_rom nuttx
  ELF program header segment 0:
  @0x80000000 size=0x2b374 ROM=0
loader_write_rom nuttx
  ELF program header segment 1:
  @0x80200000 size=0x2a1 ROM=0
loader_write_rom initrd:
  @0x84000000 size=0x2fc3e8 ROM=0
loader_write_rom fdt:
  @0x87000000 size=0x100000 ROM=0
```

So Initial RAM Disk is loaded at `0x8400` `0000`

(`__ramdisk_start` from the previous section)

Also we see that Kernel is loaded at `0x8000` `0000`, Device Tree at `0x8700` `0000`.

# Device Tree for RISC-V QEMU

Read the article...

-   ["Star64 JH7110 + NuttX RTOS: RISC-V Semihosting and Initial RAM Disk"](https://lupyuen.github.io/articles/semihost)

To dump the Device Tree for QEMU RISC-V, we specify `dumpdtb`...

```bash
## Dump Device Tree for QEMU RISC-V
qemu-system-riscv64 \
  -semihosting \
  -M virt,aclint=on,dumpdtb=qemu-riscv64.dtb \
  -cpu rv64 \
  -smp 8 \
  -bios none \
  -kernel nuttx \
  -nographic

## Convert Device Tree to text format
dtc \
  -o qemu-riscv64.dts \
  -O dts \
  -I dtb \
  qemu-riscv64.dtb
```

This produces the Device Tree for QEMU RISC-V...

- [qemu-riscv64.dts: Device Tree for QEMU RISC-V](https://github.com/lupyuen/nuttx-star64/blob/main/qemu-riscv64.dts)

Which is helpful for browsing the Memory Addresses of I/O Peripherals.

# TODO

TODO: Port [__up_mtimer_initialize__](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64a/arch/risc-v/src/qemu-rv/qemu_rv_timerisr.c#L151-L210) to Star64

TODO: RISC-V Exceptions [riscv_exception_common.S](https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64/arch/risc-v/src/common/riscv_exception_common.S#L77)

TODO: Handle Machine Exception

https://github.com/lupyuen2/wip-pinephone-nuttx/blob/star64d/arch/risc-v/src/qemu-rv/qemu_rv_exception_m.S#L64

TODO: Check PolarFire Icicle 

https://lupyuen.github.io/articles/privilege#other-risc-v-ports-of-nuttx

TODO: Check Linux Boot Code

https://github.com/torvalds/linux/blob/master/arch/riscv/kernel/head.S

TODO: Linux SBI Interface

https://github.com/torvalds/linux/blob/master/arch/riscv/kernel/sbi.c

# U-Boot Bootloader Log for TFTP

```text
U-Boot SPL 2021.10 (Jan 19 2023 - 04:09:41 +0800)
DDR version: dc2e84f0.
Trying to boot from SPI
U-Boot SPL 2021.10 (Jan 19 2023 - 04:09:41 +0800)
DDR version: dc2e84f0.
Trying to boot from SPI

OpenSBI v1.2
   ____                    _____ ____ _____
  / __ \                  / ____|  _ \_   _|
 | |  | |_ __   ___ _ __ | (___ | |_) || |
 | |  | | '_ \ / _ \ '_ \ \___ \|  _ < | |
 | |__| | |_) |  __/ | | |____) | |_) || |_
  \____/| .__/ \___|_| |_|_____/|____/_____|
        | |
        |_|

Platform Name             : StarFive VisionFive V2
Platform Features         : medeleg
Platform HART Count       : 5
Platform IPI Device       : aclint-mswi
Platform Timer Device     : aclint-mtimer @ 4000000Hz
Platform Console Device   : uart8250
Platform HSM Device       : jh7110-hsm
Platform PMU Device       : ---
Platform Reboot Device    : pm-reset
Platform Shutdown Device  : pm-reset
Firmware Base             : 0x40000000
Firmware Size             : 288 KB
Runtime SBI Version       : 1.0

Domain0 Name              : root
Domain0 Boot HART         : 1
Domain0 HARTs             : 0*,1*,2*,3*,4*
Domain0 Region00          : 0x0000000002000000-0x000000000200ffff (I)
Domain0 Region01          : 0x0000000040000000-0x000000004007ffff ()
Domain0 Region02          : 0x0000000000000000-0xffffffffffffffff (R,W,X)
Domain0 Next Address      : 0x0000000040200000
Domain0 Next Arg1         : 0x0000000042200000
Domain0 Next Mode         : S-mode
Domain0 SysReset          : yes

Boot HART ID              : 1
Boot HART Domain          : root
Boot HART Priv Version    : v1.11
Boot HART Base ISA        : rv64imafdcbx
Boot HART ISA Extensions  : none
Boot HART PMP Count       : 8
Boot HART PMP Granularity : 4096
Boot HART PMP Address Bits: 34
Boot HART MHPM Count      : 2
Boot HART MIDELEG         : 0x0000000000000222
Boot HART MEDELEG         : 0x000000000000b109


U-Boot 2021.10 (Jan 19 2023 - 04:09:41 +0800), Build: jenkins-github_visionfive2-6

CPU:   rv64imacu
Model: StarFive VisionFive V2
DRAM:  8 GiB
MMC:   sdio0@16010000: 0, sdio1@16020000: 1
Loading Environment from SPIFlash... SF: Detected gd25lq128 with page size 256 Bytes, erase size 4 KiB, total 16 MiB
*** Warning - bad CRC, using default environment

StarFive EEPROM format v2

--------EEPROM INFO--------
Vendor : PINE64
Product full SN: STAR64V1-2310-D008E000-00000003
data version: 0x2
PCB revision: 0xc1
BOM revision: A
Ethernet MAC0 address: 6c:cf:39:00:75:5d
Ethernet MAC1 address: 6c:cf:39:00:75:5e
--------EEPROM INFO--------

In:    serial@10000000
Out:   serial@10000000
Err:   serial@10000000
Model: StarFive VisionFive V2
Net:   eth0: ethernet@16030000, eth1: ethernet@16040000
Card did not respond to voltage select! : -110
Card did not respond to voltage select! : -110
bootmode flash device 0
Card did not respond to voltage select! : -110
Hit any key to stop autoboot:  2  1  0 
Card did not respond to voltage select! : -110
Couldn't find partition mmc 0:3
Can't set block device
Importing environment from mmc0 ...
## Warning: Input data exceeds 1048576 bytes - truncated
## Info: input data size = 1048578 = 0x100002
Card did not respond to voltage select! : -110
Couldn't find partition mmc 1:2
Can't set block device
## Warning: defaulting to text format
## Error: "boot2" not defined
Card did not respond to voltage select! : -110
ethernet@16030000 Waiting for PHY auto negotiation to complete....... done
BOOTP broadcast 1
*** Unhandled DHCP Option in OFFER/ACK: 43
*** Unhandled DHCP Option in OFFER/ACK: 43
DHCP client bound to address 192.168.x.x (351 ms)
Using ethernet@16030000 device
TFTP from server 192.168.x.x; our IP address is 192.168.x.x
Filename 'boot.scr.uimg'.
Load address: 0x43900000
Loading: *
TFTP server died; starting again
BOOTP broadcast 1
*** Unhandled DHCP Option in OFFER/ACK: 43
*** Unhandled DHCP Option in OFFER/ACK: 43
DHCP client bound to address 192.168.x.x (576 ms)
Using ethernet@16030000 device
TFTP from server 192.168.x.x; our IP address is 192.168.x.x
Filename 'boot.scr.uimg'.
Load address: 0x40200000
Loading: *
TFTP server died; starting again

StarFive # setenv tftp_server 192.168.x.x

StarFive # tftpboot ${kernel_addr_r} ${tftp_server}:Image
Using ethernet@16030000 device
TFTP from server 192.168.x.x; our IP address is 192.168.x.x
Filename 'Image'.
Load address: 0x40200000
Loading: *#############################################################T ####
[8C #################################################################
[8C #############
[8C 221.7 KiB/s
done
Bytes transferred = 2097832 (2002a8 hex)

StarFive # tftpboot ${fdt_addr_r} ${tftp_server}:jh7110-star64-pine64.dtb
Using ethernet@16030000 device
TFTP from server 192.168.x.x; our IP address is 192.168.x.x
Filename 'jh7110-star64-pine64.dtb'.
Load address: 0x46000000
Loading: *####
[8C 374 KiB/s
done
Bytes transferred = 50235 (c43b hex)

StarFive # fdt addr ${fdt_addr_r}

StarFive # booti ${kernel_addr_r} - ${fdt_addr_r}
## Flattened Device Tree blob at 46000000
   Booting using the fdt blob at 0x46000000
   Using Device Tree in place at 0000000046000000, end 000000004600f43a

Starting kernel ...

clk u5_dw_i2c_clk_core already disabled
clk u5_dw_i2c_clk_apb already disabled
123067DFAGHBC
```

# U-Boot Bootloader Log for Auto Network Boot

```text
U-Boot SPL 2021.10 (Jan 19 2023 - 04:09:41 +0800)
DDR version: dc2e84f0.
Trying to boot from SPI

OpenSBI v1.2
   ____                    _____ ____ _____
  / __ \                  / ____|  _ \_   _|
 | |  | |_ __   ___ _ __ | (___ | |_) || |
 | |  | | '_ \ / _ \ '_ \ \___ \|  _ < | |
 | |__| | |_) |  __/ | | |____) | |_) || |_
  \____/| .__/ \___|_| |_|_____/|____/_____|
        | |
        |_|

Platform Name             : StarFive VisionFive V2
Platform Features         : medeleg
Platform HART Count       : 5
Platform IPI Device       : aclint-mswi
Platform Timer Device     : aclint-mtimer @ 4000000Hz
Platform Console Device   : uart8250
Platform HSM Device       : jh7110-hsm
Platform PMU Device       : ---
Platform Reboot Device    : pm-reset
Platform Shutdown Device  : pm-reset
Firmware Base             : 0x40000000
Firmware Size             : 288 KB
Runtime SBI Version       : 1.0

Domain0 Name              : root
Domain0 Boot HART         : 1
Domain0 HARTs             : 0*,1*,2*,3*,4*
Domain0 Region00          : 0x0000000002000000-0x000000000200ffff (I)
Domain0 Region01          : 0x0000000040000000-0x000000004007ffff ()
Domain0 Region02          : 0x0000000000000000-0xffffffffffffffff (R,W,X)
Domain0 Next Address      : 0x0000000040200000
Domain0 Next Arg1         : 0x0000000042200000
Domain0 Next Mode         : S-mode
Domain0 SysReset          : yes

Boot HART ID              : 1
Boot HART Domain          : root
Boot HART Priv Version    : v1.11
Boot HART Base ISA        : rv64imafdcbx
Boot HART ISA Extensions  : none
Boot HART PMP Count       : 8
Boot HART PMP Granularity : 4096
Boot HART PMP Address Bits: 34
Boot HART MHPM Count      : 2
Boot HART MIDELEG         : 0x0000000000000222
Boot HART MEDELEG         : 0x000000000000b109


U-Boot 2021.10 (Jan 19 2023 - 04:09:41 +0800), Build: jenkins-github_visionfive2-6

CPU:   rv64imacu
Model: StarFive VisionFive V2
DRAM:  8 GiB
MMC:   sdio0@16010000: 0, sdio1@16020000: 1
Loading Environment from SPIFlash... SF: Detected gd25lq128 with page size 256 Bytes, erase size 4 KiB, total 16 MiB
OK
StarFive EEPROM format v2

--------EEPROM INFO--------
Vendor : PINE64
Product full SN: STAR64V1-2310-D008E000-00000003
data version: 0x2
PCB revision: 0xc1
BOM revision: A
Ethernet MAC0 address: 6c:cf:39:00:75:5d
Ethernet MAC1 address: 6c:cf:39:00:75:5e
--------EEPROM INFO--------

In:    serial@10000000
Out:   serial@10000000
Err:   serial@10000000
Model: StarFive VisionFive V2
Net:   eth0: ethernet@16030000, eth1: ethernet@16040000
Card did not respond to voltage select! : -110
Card did not respond to voltage select! : -110
bootmode flash device 0
Card did not respond to voltage select! : -110
Hit any key to stop autoboot:  2  1  0 
Card did not respond to voltage select! : -110
Couldn't find partition mmc 0:3
Can't set block device
Importing environment from mmc0 ...
Card did not respond to voltage select! : -110
Couldn't find partition mmc 1:2
Can't set block device
## Warning: defaulting to text format
## Error: "boot2" not defined
Card did not respond to voltage select! : -110
ethernet@16030000 Waiting for PHY auto negotiation to complete....... done
BOOTP broadcast 1
*** Unhandled DHCP Option in OFFER/ACK: 43
*** Unhandled DHCP Option in OFFER/ACK: 43
DHCP client bound to address 192.168.x.x (550 ms)
Using ethernet@16030000 device
TFTP from server 192.168.x.x; our IP address is 192.168.x.x
Filename 'boot.scr.uimg'.
Load address: 0x43900000
Loading: *
TFTP server died; starting again
BOOTP broadcast 1
*** Unhandled DHCP Option in OFFER/ACK: 43
*** Unhandled DHCP Option in OFFER/ACK: 43
DHCP client bound to address 192.168.x.x (547 ms)
Using ethernet@16030000 device
TFTP from server 192.168.x.x; our IP address is 192.168.x.x
Filename 'boot.scr.uimg'.
Load address: 0x40200000
Loading: *
TFTP server died; starting again
Using ethernet@16030000 device
TFTP from server 192.168.x.x; our IP address is 192.168.x.x
Filename 'Image'.
Load address: 0x40200000
Loading: *#################################################################
[8C ###########################################################T ######T 
[8C #############
[8C 147.5 KiB/s
done
Bytes transferred = 2097832 (2002a8 hex)
Using ethernet@16030000 device
TFTP from server 192.168.x.x; our IP address is 192.168.x.x
Filename 'jh7110-star64-pine64.dtb'.
Load address: 0x46000000
Loading: *#T ###
[8C 8.8 KiB/s
done
Bytes transferred = 50235 (c43b hex)
## Flattened Device Tree blob at 46000000
   Booting using the fdt blob at 0x46000000
   Using Device Tree in place at 0000000046000000, end 000000004600f43a

Starting kernel ...

clk u5_dw_i2c_clk_core already disabled
clk u5_dw_i2c_clk_apb already disabled
123067DFAGHBCUnhandled exception: Store/AMO access fault
EPC: 0000000040200628 RA: 00000000402004ba TVAL: ffffff8000008000
EPC: ffffffff804ba628 RA: ffffffff804ba4ba reloc adjusted

SP:  0000000040406a30 GP:  00000000ff735e00 TP:  0000000000000001
T0:  0000000010000000 T1:  0000000000000037 T2:  ffffffffffffffff
S0:  0000000040400000 S1:  0000000000000200 A0:  0000000000000003
A1:  0000080000008000 A2:  0000000010100000 A3:  0000000040400000
A4:  0000000000000026 A5:  0000000000000000 A6:  00000000101000e7
A7:  0000000000000000 S2:  0000080000008000 S3:  0000000040600000
S4:  0000000040400000 S5:  0000000000000000 S6:  0000000000000026
S7:  00fffffffffff000 S8:  0000000040404000 S9:  0000000000001000
S10: 0000000040400ab0 S11: 0000000000200000 T3:  0000000000000023
T4:  000000004600f43a T5:  000000004600d000 T6:  000000004600cfff

Code: 879b 0277 d7b3 00f6 f793 1ff7 078e 95be (b023 0105)


resetting ...
reset not supported yet
### ERROR ### Please RESET the board ###
```

# NuttX Logs

## NuttX Star64 Binary Loader Log

```text
Starting kernel ...

clk u5_dw_i2c_clk_core already disabled
clk u5_dw_i2c_clk_apb already disabled
123067DFHBCqemu_rv_kernel_mappings: map I/O regions
qemu_rv_kernel_mappings: map kernel text
qemu_rv_kernel_mappings: map kernel data
qemu_rv_kernel_mappings: connect the L1 and L2 page tables
qemu_rv_kernel_mappings: map the page pool
qemu_rv_mm_init: mmu_enable: satp=1077956608
Inx_start: Entry
elf_initialize: Registering ELF
uart_register: Registering /dev/console
uart_register: Registering /dev/ttyS0
work_start_lowpri: Starting low-priority kernel worker thread(s)
board_late_initialize: 
nx_start_application: Starting init task: /system/bin/init
load_absmodule: Loading /system/bin/init
elf_loadbinary: Loading file: /system/bin/init
elf_init: filename: /system/bin/init loadinfo: 0x4040c638
elf_read: Read 64 bytes from offset 0
elf_dumploadinfo: LOAD_INFO:
elf_dumploadinfo:   textalloc:    00000000
elf_dumploadinfo:   dataalloc:    00000000
elf_dumploadinfo:   textsize:     0
elf_dumploadinfo:   datasize:     0
elf_dumploadinfo:   textalign:    0
elf_dumploadinfo:   dataalign:    0
elf_dumploadinfo:   filelen:      3289528
elf_dumploadinfo:   symtabidx:    0
elf_dumploadinfo:   strtabidx:    0
elf_dumploadinfo: ELF Header:
elf_dumploadinfo:   e_ident:      7f 45 4c 46
elf_dumploadinfo:   e_type:       0001
elf_dumploadinfo:   e_machine:    00f3
elf_dumploadinfo:   e_version:    00000001
elf_dumploadinfo:   e_entry:      0000004a
elf_dumploadinfo:   e_phoff:      0
elf_dumploadinfo:   e_shoff:      3286264
elf_dumploadinfo:   e_flags:      00000001
elf_dumploadinfo:   e_ehsize:     64
elf_dumploadinfo:   e_phentsize:  0
elf_dumploadinfo:   e_phnum:      0
elf_dumploadinfo:   e_shentsize:  64
elf_dumploadinfo:   e_shnum:      51
elf_dumploadinfo:   e_shstrndx:   50
elf_load: loadinfo: 0x4040c638
elf_read: Read 3264 bytes from offset 3286264
elf_loadfile: Loaded sections:
elf_read: Read 39900 bytes from offset 64
elf_loadfile: 1. 00000000->c0000000
elf_read: Read 45804 bytes from offset 39968
elf_loadfile: 3. 00009be0->c0009be0
elf_read: Read 9 bytes from offset 85776
elf_loadfile: 5. 00000000->c0014ed0
elf_read: Read 3 bytes from offset 85792
elf_loadfile: 6. 00000000->c0014ee0
elf_read: Read 3 bytes from offset 85800
elf_loadfile: 7. 00000000->c0014ee8
elf_read: Read 2 bytes from offset 85808
elf_loadfile: 8. 00000000->c0014ef0
elf_read: Read 2 bytes from offset 85816
...
elf_read: Read 24 bytes from offset 1313160
elf_symvalue: Other: 00005c88+c0000000=c0005c88
elf_read: Read 24 bytes from offset 1313352
elf_symvalue: Other: 00005c82+c0000000=c0005c82
elf_read: Read 24 bytes from offset 1313376
elf_symvalue: Other: 00005c72+c0000000=c0005c72
elf_read: Read 24 bytes from offset 1313400
elf_symvalue: Other: 00005c60+c0000000=c0005c60
elf_read: Read 24 bytes from offset 1313424
elf_symvalue: Other: 00005c78+c0000000=c0005c78
elf_read: Read 24 bytes from offset 1313448
elf_symvalue: Other: 00005c66+c0000000=c0005c66
elf_read: Read 24 bytes from offset 1313472
elf_symvalue: Other: 00005c6c+c0000000=c0005c6c
elf_read: Read 24 bytes from offset 1313496
elf_symvalue: Other: 00005d70+c0000000=c0005d70
elf_read: Read 24 bytes from offset 1312896
elf_symvalue: Other: 000019d0+c0009be0=c000b5b0
elf_read: Read 24 bytes from offset 1313232
elf_symvalue: Other: 00005d5a+c0000000=c0005d5a
elf_read: Read 24 bytes from offset 1313520
elf_symvalue: Other: 00005cf8+c0000000=c0005cf8
elf_read: Read 24 bytes from offset 1313544
elf_symvalue: Other: 00005d76+c0000000=c0005d76
elf_read: Read 24 bytes from offset 1313568
elf_symvalue: Other: 00005d4c+c0000000=c0005d4c
elf_read: Read 24 bytes from offset 1313592
elf_symvalue: Other: 00005d52+c0000000=c0005d52
elf_read: Read 24 bytes from offset 1313616
elf_symvalue: Other: 00005d56+c0000000=c0005d56
elf_read: Read 24 bytes from offset 1961968
elf_read: Read 24 bytes from offset 1781688
elf_symvalue: Other: 00000000+c0101028=c0101028
up_relocateadd: RISCV_64 at c0101028 [00000000] to sym=0x4040a850 st_value=c0101028
load_absmodule: Successfully loaded module /system/bin/init
binfmt_dumpmodule: Module:
binfmt_dumpmodule:   entrypt:   0xc000004a
binfmt_dumpmodule:   mapped:    0 size=0
binfmt_dumpmodule:   alloc:     0 0 0
binfmt_dumpmodule:   addrenv:   0x40409f60
binfmt_dumpmodule:   stacksize: 2048
binfmt_dumpmodule:   unload:    0
exec_module: Executing /system/bin/init
binfmt_copyargv: args=0 argsize=0
binfmt_copyargv: args=2 argsize=23
exec_module: Initialize the user heap (heapsize=528384)
nx_start_application: ret=3
up_exit: TCB=0x404088d0 exiting
nx_start: CPU0: Beginning Idle Loop
```

## NuttX QEMU Binary Loader Log

```text
elf_symvalue: Other: 00005d76+c0000000=c0005d76
elf_read: Read 24 bytes from offset 1302760
elf_symvalue: Other: 00005d4c+c0000000=c0005d4c
elf_read: Read 24 bytes from offset 1302784
elf_symvalue: Other: 00005d52+c0000000=c0005d52
elf_read: Read 24 bytes from offset 1302808
elf_symvalue: Other: 00005d56+c0000000=c0005d56
elf_read: Read 24 bytes from offset 1951160
elf_read: Read 24 bytes from offset 1770880
elf_symvalue: Other: 00000000+c0101028=c0101028
up_relocateadd: RISCV_64 at c0101028 [00000000] to sym=0x8020a850 st_value=c0101028
load_absmodule: Successfully loaded module /system/bin/init
binfmt_dumpmodule: Module:
binfmt_dumpmodule:   entrypt:   0xc000004a
binfmt_dumpmodule:   mapped:    0 size=0
binfmt_dumpmodule:   alloc:     0 0 0
binfmt_dumpmodule:   addrenv:   0x80209f60
binfmt_dumpmodule:   stacksize: 2048
binfmt_dumpmodule:   unload:    0
exec_module: Executing /system/bin/init
binfmt_copyargv: args=0 argsize=0
binfmt_copyargv: args=2 argsize=23
exec_module: Initialize the user heap (heapsize=528384)
up_exit: TCB=0x802088d0 exiting

NuttShell (NSH) NuttX-12.0.3
nsh> nx_start: CPU0: Beginning Idle Loop
```

## NuttX Star64 Memory Management Log

```text
mm_free: Freeing 0x4040aa10
mm_free: Freeing 0x4040a9d0
mm_free: Freeing 0x4040a990
mm_free: Freeing 0x4040a950
mm_free: Freeing 0x4040a890
mm_malloc: Allocated 0x4040c810, size 6160
mm_malloc: Allocated 0x4040a890, size 64
mm_free: Freeing 0x4040c810
mm_free: Freeing 0x4040a890
mm_free: Freeing 0x40409290
mm_free: Freeing 0x40409fa0
mm_free: Freeing 0x40409250
mm_malloc: Allocated 0x40409250, size 368
mm_malloc: Allocated 0x404093c0, size 64
mm_initialize: Heap: name=(null), start=0xc0200000 size=528384
mm_addregion: [(null)] Region 1: base=0xc0200298 size=527712
mm_malloc: Allocated 0x4040a890, size 3088
mm_malloc: Allocated 0x4040b4a0, size 304
mm_malloc: Allocated 0x4040b5d0, size 32
mm_malloc: Allocated 0xc02002c0, size 624
mm_malloc: Allocated 0xc0200530, size 32
mm_malloc: Allocated 0xc0200550, size 32
mm_malloc: Allocated 0xc0200570, size 32
mm_malloc: Allocated 0x4040b5f0, size 32
mm_malloc: Allocated 0x4040b610, size 160
mm_malloc: Allocated 0xc0200590, size 19472
mm_free: Freeing 0x404093c0
nx_start_application: ret=3
mm_free: Freeing 0x40408b90
mm_free: Freeing 0x40408e80
mm_free: Freeing 0x40408e60
mm_free: Freeing 0x40408e40
mm_free: Freeing 0x40408e20
mm_free: Freeing 0x40408e00
mm_free: Freeing 0x40408b70
mm_free: Freeing 0x40408a40
up_exit: TCB=0x404088d0 exiting
mm_free: Freeing 0x4040c000
mm_free: Freeing 0x404088d0
mm_malloc: Allocated 0xc0200590, size 848
nx_start: CPU0: Beginning Idle Loop
```

## NuttX QEMU Memory Management Log

```text
mm_free: Freeing 0x8020aa80
mm_free: Freeing 0x8020aa40
mm_free: Freeing 0x8020a9c0
mm_free: Freeing 0x8020a980
mm_free: Freeing 0x8020a940
mm_free: Freeing 0x8020a900
mm_free: Freeing 0x8020a840
mm_malloc: Allocated 0x8020c810, size 6160
mm_malloc: Allocated 0x8020a840, size 64
mm_free: Freeing 0x8020c810
mm_free: Freeing 0x8020a840
mm_free: Freeing 0x80209290
mm_free: Freeing 0x8020a810
mm_free: Freeing 0x80209250
mm_malloc: Allocated 0x80209250, size 368
mm_malloc: Allocated 0x802093c0, size 64
mm_initialize: Heap: name=(null), start=0xc0200000 size=528384
mm_addregion: [(null)] Region 1: base=0xc0200298 size=527712
mm_malloc: Allocated 0x8020a810, size 3088
mm_malloc: Allocated 0x80209400, size 304
mm_malloc: Allocated 0x80209fe0, size 32
mm_malloc: Allocated 0xc02002c0, size 624
mm_malloc: Allocated 0xc0200530, size 32
mm_malloc: Allocated 0xc0200550, size 32
mm_malloc: Allocated 0xc0200570, size 32
mm_malloc: Allocated 0x80209530, size 32
mm_malloc: Allocated 0x80209550, size 160
mm_malloc: Allocated 0xc0200590, size 19472
mm_free: Freeing 0x802093c0
mm_free: Freeing 0x80208b90
mm_free: Freeing 0x80208e80
mm_free: Freeing 0x80208e60
mm_free: Freeing 0x80208e40
mm_free: Freeing 0x80208e20
mm_free: Freeing 0x80208e00
mm_free: Freeing 0x80208b70
mm_free: Freeing 0x80208a40
up_exit: TCB=0x802088d0 exiting
mm_free: Freeing 0x8020c000
mm_free: Freeing 0x802088d0

NuttShell (NSH) NuttX-12.0.3
nsh> nx_start: CPU0: Beginning Idle Loop
```

## NuttX Star64 NSH Assertion Log

No Console Output!

```text
clk u5_dw_i2c_clk_core already disabled
clk u5_dw_i2c_clk_apb already disabled
123067DFHBCInx_start: Entry
uart_register: Registering /dev/console
uart_register: Registering /dev/ttyS0
work_start_lowpri: Starting low-priority kernel worker thread(s)
board_late_initialize: 
nx_start_application: Starting init task: /system/bin/init
elf_symname: Symbol has no name
elf_symvalue: SHN_UNDEF: Failed to get symbol name: -3
elf_relocateadd: Section 2 reloc 1: Undefined symbol[0] has no name: -3
nx_start_application: ret=3
up_exit: TCB=0x404088d0 exiting
_assert: Current Version: NuttX  12.0.3 46c1a0f Jul 27 2023 19:31:45 risc-v
_assert: Assertion failed (_Bool)0: at file: nsh_main.c:54 task: /system/bin/init 0xc000001a
up_dump_register: EPC: 000000004020fffc
up_dump_register: A0: 0000000040401610 A1: 0000000000000036 A2: 00000000c0000e58 A3: 0000000000000000
up_dump_register: A4: 0000000000000000 A5: 0000000000000000 A6: 0000000000000036 A7: 00000000c0000e68
up_dump_register: T0: 0000000040211e9e T1: 00000000c000042c T2: 0000000000000000 T3: 0000000000000000
up_dump_register: T4: 0000000000000000 T5: 0000000000000000 T6: 0000000000000000
up_dump_register: S0: 0000000000000000 S1: 0000000040409a60 S2: 0000000040401748 S3: 00000000c0000e58
up_dump_register: S4: 00000000c0000e68 S5: 0000000000000036 S6: 0000000000000000 S7: 0000000000000000
up_dump_register: S8: 0000000000000000 S9: 0000000000000000 S10: 0000000000000000 S11: 0000000000000000
up_dump_register: SP: 000000004040b1d8 FP: 0000000000000000 TP: 0000000000000000 RA: 000000004020fffc
dump_stack: Kernel Stack:
dump_stack:   base: 0x4040a810
dump_stack:   size: 00003072
dump_stack:     sp: 0x4040b1d8
stack_dump: 0x4040b1c0: 40409a60 00000000 00000000 00000000 4021021c 00000000 40406cf8 00000000
stack_dump: 0x4040b1e0: 00000219 00010000 c00003ee 00000000 00000000 00000000 4020029a 00000000
stack_dump: 0x4040b200: 7474754e 00000058 c000080e 00000000 c0202b90 00000000 ffffff83 ffffffff
stack_dump: 0x4040b220: 00000000 00000000 402126ce 00000000 c000042c 2e323100 00332e30 00000000
stack_dump: 0x4040b240: c02003d8 00000000 363403d0 30613163 754a2066 3732206c 32303220 39312033
stack_dump: 0x4040b260: 3a31333a 00003534 00000000 00000000 00007fff 00000000 00000001 73697200
stack_dump: 0x4040b280: 00762d63 00000000 00000000 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x4040b2a0: 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x4040b2c0: 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x4040b2e0: 40211eb0 00000000 00000000 00000000 402086f4 00000000 c000007c 00000000
stack_dump: 0x4040b300: 00040020 00000002 402086dc 00000000 c000007c 00000000 4040b308 00000000
stack_dump: 0x4040b320: 00000000 00000000 00000000 00000000 402126ce 00000000 c000042c 00000000
stack_dump: 0x4040b340: 00000000 00000000 00000000 00000000 00000000 00000000 00000001 00000000
stack_dump: 0x4040b360: c0000e68 00000000 00000036 00000000 c0000e58 00000000 00000000 00000000
stack_dump: 0x4040b380: c0000e58 00000000 00000036 00000000 c0000e68 00000000 00000000 00000000
stack_dump: 0x4040b3a0: 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x4040b3c0: 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x4040b3e0: 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000
up_exit: TCB=0x40409a60 exiting
nx_start: CPU0: Beginning Idle Loop
```

## NuttX QEMU NSH Assertion Log

Console Output OK

```text
ABCnx_start: Entry
uart_register: Registering /dev/console
uart_register: Registering /dev/ttyS0
work_start_lowpri: Starting low-priority kernel worker thread(s)
board_late_initialize: 
nx_start_application: Starting init task: /system/bin/init
elf_symname: Symbol has no name
elf_symvalue: SHN_UNDEF: Failed to get symbol name: -3
elf_relocateadd: Section 2 reloc 1: Undefined symbol[0] has no name: -3
up_exit: TCB=0x802088d0 exiting
***main
_assert: Current Version: NuttX  12.0.3 3c99d2b-dirty Jul 27 2023 19:27:52 risc-v
_assert: Assertion failed (_Bool)0: at file: nsh_main.c:54 task: /system/bin/init 0xc000001a
up_dump_register: EPC: 0000000080001e82
up_dump_register: A0: 0000000080200f10 A1: 0000000000000036 A2: 00000000c0000e58 A3: 0000000000000000
up_dump_register: A4: 0000000000000000 A5: 0000000000000000 A6: 0000000000000036 A7: 00000000c0000e68
up_dump_register: T0: 0000000080006d36 T1: 00000000c000042c T2: 0000000000000000 T3: 0000000000000000
up_dump_register: T4: 0000000000000000 T5: 0000000000000000 T6: 0000000000000000
up_dump_register: S0: 0000000000000000 S1: 0000000080209a60 S2: 0000000080201750 S3: 00000000c0000e58
up_dump_register: S4: 00000000c0000e68 S5: 0000000000000036 S6: 0000000000000000 S7: 0000000000000000
up_dump_register: S8: 0000000000000000 S9: 0000000000000000 S10: 0000000000000000 S11: 0000000000000000
up_dump_register: SP: 000000008020b1d8 FP: 0000000000000000 TP: 0000000000000000 RA: 0000000080001e82
dump_stack: Kernel Stack:
dump_stack:   base: 0x8020a810
dump_stack:   size: 00003072
dump_stack:     sp: 0x8020b1d8
stack_dump: 0x8020b1c0: 80209a60 00000000 00000000 00000000 800020a2 00000000 80206cf8 00000000
stack_dump: 0x8020b1e0: 00000219 00010000 c00003ee 00000000 00000000 00000000 80000592 00000000
stack_dump: 0x8020b200: 7474754e 00000058 c000080e 00000000 c0202b90 00000000 c0200430 00000000
stack_dump: 0x8020b220: 00000000 00000000 80007566 00000000 c000042c 2e323100 00332e30 00000000
stack_dump: 0x8020b240: c02003d8 00000000 633303d0 32643939 69642d62 20797472 206c754a 32203732
stack_dump: 0x8020b260: 20333230 323a3931 32353a37 00000000 00007fff 00000000 00000001 73697200
stack_dump: 0x8020b280: 00762d63 00000000 00000000 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x8020b2a0: 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x8020b2c0: 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x8020b2e0: 80006d48 00000000 00000000 00000000 80001264 00000000 c000007c 00000000
stack_dump: 0x8020b300: 00040020 00000002 8000124c 00000000 c000007c 00000000 8020b308 00000000
stack_dump: 0x8020b320: 00000000 00000000 00000000 00000000 80007566 00000000 c000042c 00000000
stack_dump: 0x8020b340: 00000000 00000000 00000000 00000000 00000000 00000000 00000001 00000000
stack_dump: 0x8020b360: c0000e68 00000000 00000036 00000000 c0000e58 00000000 00000000 00000000
stack_dump: 0x8020b380: c0000e58 00000000 00000036 00000000 c0000e68 00000000 00000000 00000000
stack_dump: 0x8020b3a0: 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x8020b3c0: 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000
stack_dump: 0x8020b3e0: 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000
up_exit: TCB=0x80209a60 exiting
nx_start: CPU0: Beginning Idle Loop
```

## NuttX Star64 Console Output Log

Console Output is stuck

```text
clk u5_dw_i2c_clk_core already disabled
clk u5_dw_i2c_clk_apb already disabled
123067DFHBCInx_start: Entry
uart_register: Registering /dev/console
uart_register: Registering /dev/ttyS0
work_start_lowpri: Starting low-priority kernel worker thread(s)
board_late_initialize: 
nx_start_application: Starting init task: /system/bin/init
elf_symname: Symbol has no name
elf_symvalue: SHN_UNDEF: Failed to get symbol name: -3
elf_relocateadd: Section 2 reloc 2: Undefined symbol[0] has no name: -3
nx_start_application: ret=3
up_exit: TCB=0x404088d0 exiting
uart_write (0xc0200428):
0000  2a 2a 2a 6d 61 69 6e 0a                          ***main.        
uart_write (0xc000a610):
0000  0a 4e 75 74 74 53 68 65 6c 6c 20 28 4e 53 48 29  .NuttShell (NSH)
0010  20 4e 75 74 74 58 2d 31 32 2e 30 2e 33 0a         NuttX-12.0.3.  
uart_write (0xc0015340):
0000  6e 73 68 3e 20                                   nsh>            
uart_write (0xc0015318):
0000  1b 5b 4b                                         .[K             
nx_start: CPU0: Beginning Idle Loop
```
