# Apache NuttX RTOS for Pine64 Star64 64-bit RISC-V SBC (StarFive JH7110)

Read the article...

-   ["64-bit RISC-V with Apache NuttX Real-Time Operating System"](https://lupyuen.github.io/articles/riscv)

# Linux Images for Star64

Let's examine the Linux Images for Star64 SBC, to see how U-Boot Bootloader is configured.

According to [Software Releases for Star64](https://wiki.pine64.org/wiki/STAR64#Software_releases), we have...

1.  [Yocto Images](https://github.com/Fishwaldo/meta-pine64) at [pine64.my-ho.st](https://pine64.my-ho.st:8443/)

    Let's inspect [star64-image-minimal](https://pine64.my-ho.st:8443/star64-image-minimal-star64-1.2.wic.bz2)

1.  [Armbian Images](https://www.armbian.com/star64/)

    Let's inspect [Armbian 23.8 Lunar (Minimal)](https://github.com/armbianro/os/releases/download/23.8.0-trunk.56/Armbian_23.8.0-trunk.56_Star64_lunar_edge_5.15.0_minimal.img.xz)

# Armbian Image for Star64

TODO

Uncompress the .xz, mount the .img file on macOS.

# Yocto Image for Star64

Let's inspect the Yocto Image for Star64: [star64-image-minimal](https://pine64.my-ho.st:8443/star64-image-minimal-star64-1.2.wic.bz2)

Uncompress the .bz2, rename as .img. Balena Etcher won't work with .bz2 files!

Write the .img to a microSD Card with Balena Etcher. Insert the microSD Card into a Linux Machine. (Like Pinebook Pro)

We'll see 4 used partitions...

-   spl (2 MB): ???

-   uboot (4 MB): U-Boot Bootloader

-   boot (380 MB): Boot Configuration for U-Boot

-   root (686 MB): Linux Filesystem

Plus 2 unused partitions. (Why?)

![Yocto Image for Star64](https://lupyuen.github.io/images/star64-yocto.png)

TODO

# TODO
