# Introduction to LiteX
The LiteX framework provides a toolchain infrastructure to create FPGA Cores/SoCs, to explore various digital design architectures and create full [FPGA based systems](https://github.com/enjoy-digital/litex/wiki/Projects). Efabless [caravel management soc](https://github.com/efabless/caravel_mgmt_soc_litex) was also delivered from LiteX.  

More [introduction of LiteX](https://github.com/enjoy-digital/litex#welcome-to-litex).

## LiteX Lab Purpose
* Run Linux OS on VexRiscv soc with Verilator RTL simulator
* Port VexRiscv soc to [Xilinx kv260 board](https://github.com/litex-hub/litex-boards#-boards-list)

## LiteX Lab Prerequisites
* Ubuntu 20.04+
* Verilator version >= 4.2xx
* RISC-V toolchain
* Linux/OpenSBI image
* LiteX 
* OpenOCD

## Hardware Recommendation
* Physical machine with latest 8GB+ memory
* Virtual machine with latest 8GB+ memory can run but very slowly

## Offical Installation Reference
* https://github.com/enjoy-digital/litex#quick-start-guide
* https://github.com/litex-hub/linux-on-litex-vexriscv

## Run Linux OS on VexRiscv soc with Verilator RTL simulator

Install basic tools and dependencies
```
sudo apt update
sudo apt install make build-essential device-tree-compiler wget git python3-setuptools python3-pip -y
sudo apt-get install libsdl2-dev -y
sudo apt install libevent-dev libjson-c-dev -y
```
[Install basic tools and dependencies.log](https://github.com/bol-edu/litex-lab/files/11359134/Install.basic.tools.and.dependencies.log)

Compile and install latest Verilator
```
sudo apt install autoconf flex bison help2man -y
git clone https://github.com/verilator/verilator
cd verilator
git pull
autoconf
export VERILATOR_ROOT=`pwd`
./configure
make -j `nproc`
sudo make install
```
[Compile and install latest Verilator.log](https://github.com/bol-edu/litex-lab/files/11359135/Compile.and.install.latest.Verilator.log)
 
Install litex python3 dependencies
```
cd ~
python3 -m pip install ninja
python3 -m pip install meson==0.59
export PATH=$PATH:~/.local/bin
```
[Install litex python3 dependencies.log](https://github.com/bol-edu/litex-lab/files/11359136/Install.litex.python3.dependencies.log)

Install and run litex
```
git clone https://github.com/litex-hub/linux-on-litex-vexriscv
cd linux-on-litex-vexriscv
wget https://raw.githubusercontent.com/enjoy-digital/litex/master/litex_setup.py
chmod +x litex_setup.py
./litex_setup.py --init --install --user --config=full
./litex_setup.py --update
sudo ./litex_setup.py --gcc=riscv (enter y)
~/litex-boards/litex_boards/targets/xilinx_kv260.py
wget -O linux_2022_03_23.zip  https://github.com/litex-hub/linux-on-litex-vexriscv/files/8331338/linux_2022_03_23.zip
unzip linux_2022_03_23.zip -d ./images (enter y)
./sim.py (take a long time)
```
[Install and run litex.log](https://github.com/bol-edu/litex-lab/files/11359202/Install.and.run.litex.log)

```console
buildroot login: root
                   __   _
                  / /  (_)__  __ ____ __
                 / /__/ / _ \/ // /\ \ /
                /____/_/_//_/\_,_//_\_\
                      / _ \/ _ \
   __   _ __      _  _\___/_//_/         ___  _
  / /  (_) /____ | |/_/__| | / /____ __ / _ \(_)__ _____  __
 / /__/ / __/ -_)>  </___/ |/ / -_) \ // , _/ (_-</ __/ |/ /
/____/_/\__/\__/_/|_|____|___/\__/_\_\/_/|_/_/___/\__/|___/
                  / __/  |/  / _ \
                 _\ \/ /|_/ / ___/
                /___/_/  /_/_/
  32-bit RISC-V Linux running on LiteX / VexRiscv-SMP.

login[70]: root login on 'console'
root@buildroot:~# ls /
bin      init     linuxrc  opt      run      tmp
dev      lib      media    proc     sbin     usr
etc      lib32    mnt      root     sys      var
root@buildroot:~# help
Built-in commands:
------------------
        . : [ [[ alias bg break cd chdir command continue echo eval exec
        exit export false fg getopts hash help history jobs kill let
        local printf pwd read readonly return set shift source test times
        trap true type ulimit umask unalias unset wait
root@buildroot:~#
```
## Port VexRiscv soc to Xilinx kv260 board

Install OpenOCD (needed for hardware test)
```
sudo apt install libtool automake pkg-config libusb-1.0-0-dev 
git clone https://github.com/ntfreak/openocd.git
cd openocd
./bootstrap
./configure --enable-ftdi
sudo make install
```
[Install OpenOCD.log](https://github.com/bol-edu/litex-lab/files/11359212/Install.OpenOCD.log)

Build the kv260 bitstream
```
ToDo..
```
