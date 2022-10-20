使用*buildroot*默认配置*raspberrypi3_64_defconfig*直接编译的出的镜像文件大小居然高达153M...

**tiny_raspi**用于编译生成一个可以运行的最小内核.

**编译**

```
git clone https://github.com/calinyara/tiny_raspi.git
cd tiny_raspi
git clone git://git.buildroot.net/buildroot
mkdir build
mkdir buildroot_dl
cd build
make BR2_EXTERNAL=../tiny_raspi_buildroot/ O=$PWD -C ../buildroot/ tiny_raspberrypi3_64_defconfig
make -j4
```

**QEMU运行**

```
qemu-system-aarch64 -M raspi3b -kernel ./images/Image -dtb ./images/bcm2710-rpi-3-b.dtb -initrd ./images/rootfs.cpio.gz -m 1024 -nographic -append "init=/bin/sh console=ttyAMA0,115200"
```

**参考**

- [**编译一个最小可用Linux内核**](https://calinyara.github.io/technology/2022/10/16/tiny-linux-kernel.html)
