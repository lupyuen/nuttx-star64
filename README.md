![Pine64 Star64 64-bit RISC-V SBC](https://lupyuen.github.io/images/star64-title.jpg)

# Apache NuttX RTOS for Pine64 Star64 64-bit RISC-V SBC (StarFive JH7110)

Read the articles...

-   ["Inspecting the RISC-V Linux Images for Star64 SBC"](https://lupyuen.github.io/articles/star64)

-   ["64-bit RISC-V with Apache NuttX Real-Time Operating System"](https://lupyuen.github.io/articles/riscv)

-   ["Rolling to RISC-V"](https://lupyuen.github.io/articles/pinephone2#rolling-to-risc-v)

Let's port Apache NuttX RTOS to [Pine64 Star64](https://wiki.pine64.org/wiki/STAR64) 64-bit RISC-V SBC!

(Based on [StarFive JH7110 SoC](https://doc-en.rvspace.org/Doc_Center/jh7110.html))

Hopefully NuttX will run on Pine64 PineTab-V, which is also based on StarFive JH7110 SoC.

# Linux Images for Star64

Let's examine the Linux Images for Star64 SBC, to see how U-Boot Bootloader is configured. (We'll boot NuttX later with U-Boot)

According to [Software Releases for Star64](https://wiki.pine64.org/wiki/STAR64#Software_releases), we have...

-   [Yocto Images](https://github.com/Fishwaldo/meta-pine64) at [pine64.my-ho.st](https://pine64.my-ho.st:8443/)

    Let's inspect [star64-image-minimal](https://pine64.my-ho.st:8443/star64-image-minimal-star64-1.2.wic.bz2)

-   [Armbian Images](https://www.armbian.com/star64/)

    Let's inspect [Armbian 23.8 Lunar (Minimal)](https://github.com/armbianro/os/releases/download/23.8.0-trunk.56/Armbian_23.8.0-trunk.56_Star64_lunar_edge_5.15.0_minimal.img.xz)

Current state of RISC-V Linux: [Linux on RISC-V (2022)](https://docs.google.com/presentation/d/1A0A6DnGyXR_MPpeg7QunQbv_yePPqid_uRswQe8Sj8M/edit#slide=id.p)

# Armbian Image for Star64

Let's inspect the Armbian Image for Star64: [Armbian 23.8 Lunar (Minimal)](https://github.com/armbianro/os/releases/download/23.8.0-trunk.56/Armbian_23.8.0-trunk.56_Star64_lunar_edge_5.15.0_minimal.img.xz)

Uncompress the .xz, mount the .img file on Linux / macOS / Windows as an ISO Volume.

The image contains 1 used partition: `armbi_root` (612 MB) that contains the Linux Root Filesystem.

Plus one unused partition (4 MB) at the top. (Partition Table)

![Armbian Image for Star64](https://lupyuen.github.io/images/star64-armbian.png)

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

[`kernel_addr_r`](https://u-boot.readthedocs.io/en/latest/develop/bootstd.html#environment-variables) says that Linux Kernel will be loaded at `0x4400` `0000`...

```text
kernel_addr_r=0x44000000
```

(Yocto Image boots Linux Kernel at a different address, see next section)

This probably means that U-Boot Bootloader is loaded at `0x4000` `0000`.

U-Boot Bootloader will also read the options from `armbi_root/boot/extlinux/extlinux.conf`...

```text
label Armbian
  kernel /boot/Image
  initrd /boot/uInitrd
  fdt /boot/dtb/starfive/jh7110-star64-pine64.dtb
  append root=UUID=99f62df4-be35-475c-99ef-2ba3f74fe6b5 console=ttyS0,115200n8 console=tty0 earlycon=sbi rootflags=data=writeback stmmaceth=chain_mode:1 rw rw no_console_suspend consoleblank=0 fsck.fix=yes fsck.repair=yes net.ifnames=0 splash plymouth.ignore-serial-consoles
```

This says that U-Boot will load the Linux Kernel from `armbi_root/boot/Image`

Which is sym-linked to `armbi_root/boot/vmlinuz-5.15.0-starfive2`

But the Flattened Device Tree (FDT) is missing! `/boot/dtb/starfive/jh7110-star64-pine64.dtb`

Which will fail the Armbian boot. (As we'll see later)

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

Here are the files in `armbi_root/boot`...

```text
→ ls -l /Volumes/armbi_root/boot
total 94416
lrwxrwxrwx  1 Luppy  staff        24 Jun 21 13:59 Image -> vmlinuz-5.15.0-starfive2
-rw-r--r--  1 Luppy  staff   4276712 Jun 21 12:16 System.map-5.15.0-starfive2
-rw-r--r--  1 Luppy  staff      1536 Jun 21 14:00 armbian_first_run.txt.template
-rw-r--r--  1 Luppy  staff     38518 Jun 21 14:00 boot.bmp
-rw-r--r--  1 Luppy  staff    144938 Jun 21 12:16 config-5.15.0-starfive2
lrwxrwxrwx  1 Luppy  staff        20 Jun 21 13:59 dtb -> dtb-5.15.0-starfive2
drwxr-xr-x  1 Luppy  staff         0 Jun 21 13:59 dtb-5.15.0-starfive2
drwxrwxr-x  1 Luppy  staff         0 Jun 21 13:58 extlinux
lrwxrwxrwx  1 Luppy  staff        27 Jun 21 13:59 initrd.img -> initrd.img-5.15.0-starfive2
-rw-r--r--  1 Luppy  staff  10911474 Jun 21 14:01 initrd.img-5.15.0-starfive2
lrwxrwxrwx  1 Luppy  staff        27 Jun 21 13:59 initrd.img.old -> initrd.img-5.15.0-starfive2
-rw-rw-r--  1 Luppy  staff       341 Jun 21 14:00 uEnv.txt
lrwxrwxrwx  1 Luppy  staff        24 Jun 21 14:01 uInitrd -> uInitrd-5.15.0-starfive2
-rw-r--r--  1 Luppy  staff  10911538 Jun 21 14:01 uInitrd-5.15.0-starfive2
lrwxrwxrwx  1 Luppy  staff        24 Jun 21 13:59 vmlinuz -> vmlinuz-5.15.0-starfive2
-rw-r--r--  1 Luppy  staff  22040576 Jun 21 12:16 vmlinuz-5.15.0-starfive2
lrwxrwxrwx  1 Luppy  staff        24 Jun 21 13:59 vmlinuz.old -> vmlinuz-5.15.0-starfive2
```

TODO: Explain `boot/uInitrd` RAM Disk

# Yocto Image for Star64

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

[`kernel_addr_r`](https://u-boot.readthedocs.io/en/latest/develop/bootstd.html#environment-variables) says that Linux Kernel will be loaded at `0x4020` `0000`...

```text
# boot Linux flat or compressed 'Image' stored at 'kernel_addr_r'
kernel_addr_r=0x40200000
```

(Different from Armbian: `0x4400` `0000`)

Yocto boots from the [Flat Image Tree (FIT)](https://u-boot.readthedocs.io/en/latest/usage/fit/index.html#): `boot/fitImage`

Yocto's `root/boot` looks different from Armbian...

```text
$ ls -l /run/media/luppy/root/boot
total 24376
lrwxrwxrwx 1 root root       17 Mar  9  2018 fitImage -> fitImage-5.15.107
-rw-r--r-- 1 root root  9807808 Mar  9  2018 fitImage-5.15.107
-rw-r--r-- 1 root root 15151064 Mar  9  2018 fitImage-initramfs-5.15.107
```

# Boot NuttX with U-Boot Bootloader

_Will we boot NuttX with Armbian or Yocto settings? `0x4400` `0000` or `0x4020` `0000`?_

Armbian looks simpler, since it uses a plain Linux Kernel Image File `Image`. (Instead of Yocto's complicated Flat Image Tree)

Hence we'll overwrite Armbian's `armbi_root/boot/Image` by the NuttX Kernel Image.

We'll compile NuttX Kernel to boot at `0x4400` `0000`.

NuttX Kernel will begin with a RISC-V Linux Header. (See next section)

We'll use a Temporary File for the Flattened Device Tree (FDT) since it's missing from Armbian.

# Inside the Armbian Kernel Image

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

Let's decompile the Kernel Image...

TODO: Explain MZ and the funny RISC-V instruction at the top

# Decompile Armbian Kernel Image with Ghidra

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

To access the Serial Console, we connect a [USB Serial Adapter](https://pine64.com/product/serial-console-woodpecker-edition/) to Star64...

According to [Star64 Schematic](https://files.pine64.org/doc/star64/Star64_Schematic_V1.1_20230504.pdf), UART0 TX and RX (GPIO 5 and 6) are connected to the Pi GPIO Header (Pins 8 and 10).

Thus we connect these pins...

| Star64 GPIO Header | [USB Serial Adapter](https://pine64.com/product/serial-console-woodpecker-edition/) | Wire Colour |
|:----:|:----:|:----|
| Pin 6 (GND) | GND | Brown
| Pin 8 (TX) | RX | Red
| Pin 10 (RX) | TX | Orange

On our computer, connect to the USB Serial Port at 115.2 kbps...

```bash
screen /dev/ttyUSB0 115200
```

Power up Star64. The DIP Switches for GPIO 0 and 1 default to Low and Low, so Star64 should boot from Flash Memory, which has the U-Boot Bootloader inside.

[(DIP Switch Labels are inverted: __"ON"__ actually means __"Low"__)](https://wiki.pine64.org/wiki/STAR64#Prototype_Bringup_Notes)

We'll see this U-Boot Bootloader Log...

TODO: Explain [OpenSBI](https://www.thegoodpenguin.co.uk/blog/an-overview-of-opensbi/)

# Star64 U-Boot Bootloader Log

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

# UART Output on Star64

TODO

UART0 is at 0x00_1000_0000

[System Memory Map](https://doc-en.rvspace.org/JH7110/TRM/JH7110_TRM/system_memory_map.html)

Register base address "0x10000000" and range "0x10000"

[UART Device Tree](https://doc-en.rvspace.org/VisionFive2/DG_UART/JH7110_SDK/general_uart_controller.html)

[UART Datasheet](https://doc-en.rvspace.org/JH7110/Datasheet/JH7110_DS/uart.html)

[u16550_send](https://github.com/apache/nuttx/blob/master/drivers/serial/uart_16550.c#L1539-L1553)

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

[u16550_serialout](https://github.com/apache/nuttx/blob/master/drivers/serial/uart_16550.c#L610-L624)

[UART_THR_OFFSET](https://github.com/apache/nuttx/blob/dc69b108b8e0547ecf6990207526c27aceaf1e2e/include/nuttx/serial/uart_16550.h#L172-L200) is 0

```c
#define UART_THR_INCR          0 /* (DLAB =0) Transmit Holding Register */
#define UART_THR_OFFSET        (CONFIG_16550_REGINCR*UART_THR_INCR)
```

So we can transmit to UART0 by writing to `0x1000` `0000`. How convenient!

# NuttX on Star64

TODO: Test printing in QEMU

TODO: Embed Linux Kernel Header in QEMU

TODO: Set Kernel Start Address

TODO: Set UART Base Address
