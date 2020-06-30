# rtl8821CU
[![Build Status](https://travis-ci.org/whitebatman2/rtl8821CU.svg?branch=master)](https://travis-ci.org/whitebatman2/rtl8821CU)

This is a fork from the whitebatman2/rtl8821CU library.
Compilation error "gcc: error: -mfloat-abi=soft and -mfloat-abi=hard may not be used together" which occurs during compilation on ARM devices is fixed in this repository.

Tested in following environments.
```
Kernal 4.19.62-sunxi, Ubuntu 18.04.3 boinic.
Linux raspberrypi 4.19.97-v7+ armv7l GNU/Linux
```
Drivers for rtl8811CU and rtl8821CU Wi-Fi chipsets. This repository is based on soruce code found on a CD shipped with a rtl8811CU based card. It's updated to build on newer kernel versions.

## Build and install with DKMS

DKMS is a system which will automatically recompile and install a kernel module when a new kernel gets installed or updated. To make use of DKMS, install the dkms package, which on Debian (based) systems is done like this:

    apt-get install dkms

To make use of the DKMS feature with this project, do the following:

    DRV_NAME=rtl8821CU
    DRV_VERSION=5.2.5.3
    sudo mkdir /usr/src/${DRV_NAME}-${DRV_VERSION}
    git archive master | sudo tar -x -C /usr/src/${DRV_NAME}-${DRV_VERSION}
    sudo dkms add -m ${DRV_NAME} -v ${DRV_VERSION}
    sudo dkms build -m ${DRV_NAME} -v ${DRV_VERSION}
    sudo dkms install -m ${DRV_NAME} -v ${DRV_VERSION}

If you later on want to remove it again, do the following:

    DRV_NAME=rtl8821CU
    DRV_VERSION=5.2.5.3
    sudo dkms remove ${DRV_NAME}/${DRV_VERSION} --all

## Build and install without DKMS
First, makesure the kernel headers are installed
RaspberryPi -> `sudo apt install raspberrypi-kernel-headers`

Use following commands in source directory:
```
make
sudo make install
sudo modprobe 8821cu
```

### Checking installed driver
If you successfully install the driver, the driver is installed on `/lib/modules/<linux version>/kernel/drivers/net/wireless`. Check the driver with the `ls` command:
```
ls /lib/modules/$(uname -r)/kernel/drivers/net/wireless
```
Make sure `8821cu.ko` file present on that directory
