# Zephyr on LiteX-VexRiscv

## Cloning the repository

```sh
$ git clone https://github.com/antmicro/zephyr.git
$ git checkout litex-vexriscv
```

## Building the application

### Prerequisites

In order to build a sample application, the Zephyr SDK has to be installed in the system.
To install the Zephyr SDK, do the following:

```sh
$ wget https://github.com/zephyrproject-rtos/meta-zephyr-sdk/releases/download/0.10.0/zephyr-sdk-0.10.0-setup.run
$ chmod +x zephyr-sdk-0.10.0-setup.run
$ ./zephyr-sdk-0.10.0-setup.run
```

Zephyr itself requires some additional tools to be installed in the system. Follow the [Zephyr documentation](http://docs.zephyrproject.org/getting_started/installation_linux.html) for requirements.

Required python3 packages can be installed with:
```sh
$ pip3 install -r scripts/requiements.txt

### Building

To build the application you need to setup a build environment.
To do this, source the `zephyr-env.sh` file from the `zephyr` directory.
```sh
$ source zephyr-env.sh
```
Additionally, three environment variables have to be set before building the app:

```sh
$ export ZEPHYR_TOOLCHAIN_VARIANT="zephyr"
$ export ZEPHYR_SDK_INSTALL_DIR="/opt/zephyr-sdk" #assuming default sdk install directory
$ export BOARD="arty_litex_vexriscv"
```

The next step is to create a make environment:
```sh
$ cd samples/synchronization/
$ mkdir -p build && cd build
$ cmake ../

```

To build the application, simply run `make`:

```sh
$ make -j`nproc`
```

The resulting binary is located in the `build/zephyr` directory under `zephyr.bin`.

## Binary deployment

Zephyr has been tested on system generated from the [Antmicro's fork](https://github.com/antmicro/litex/tree/vexriscv-zephyr) of the LiteX repository.
The binary can be loaded with serial port using `flterm`:

```sh
flterm --port /dev/ttyUSB0 --kernel <path_to_zephyr.bin> --kernel-addr 0x40000000
```
