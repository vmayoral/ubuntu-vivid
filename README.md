Ubuntu vivid kernel for Erle-Brain
=========================
Instructions on how to get the Ubuntu kernels working on our brain.

## Dependencies:
```
sudo apt-get install fakeroot build-essential kexec-tools kernel-wedge gcc-arm-linux-gnueabihf
sudo apt-get install gcc-arm-linux-gnueabihf libncurses5 libncurses5-dev libelf-dev 
sudo apt-get install asciidoc binutils-dev
sudo apt-get build-dep linux
```

## Compiling the kernel
```
ARCH=arm ./scripts/kconfig/merge_config.sh arch/arm/configs/erlerbrain_3.8_defconfig arch/arm/configs/snappy/*.config
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- uImage dtbs -j4
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- modules -j4
sudo make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- INSTALL_MOD_PATH=/media/victor/system-a modules_install
sudo cp arch/arm/boot/zImage /media/victor/system-boot/a/vmlinuz
```

## Generation of headers and image of the kernel
```bash
export $(dpkg-architecture -aarmhf); export CROSS_COMPILE=arm-linux-gnueabihf-
fakeroot debian/rules clean
fakeroot debian/rules binary-generic
```

Sources originally from git://kernel.ubuntu.com/ubuntu/ubuntu-vivid.git
