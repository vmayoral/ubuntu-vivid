Ubuntu vivid kernel for Erle-Brain
=========================

```bash
ARCH=arm ./scripts/kconfig/merge_config.sh arch/arm/configs/omap2plus_defconfig arch/arm/configs/snappy/*.config
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- uImage dtbs -j4
```
