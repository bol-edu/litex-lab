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

## Setup Environment for LiteX

Install basic tools and dependencies
```
sudo apt update
sudo apt install make build-essential device-tree-compiler wget git python3-setuptools python3-pip -y
sudo apt-get install libsdl2-dev -y
sudo apt install libevent-dev libjson-c-dev -y
```
[Install basic tools and dependencies.log](https://github.com/bol-edu/litex-lab/files/11359080/Install.basic.tools.and.dependencies.log)
 
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
[Compile and install latest Verilator.log](https://github.com/bol-edu/litex-lab/files/11359083/Compile.and.install.latest.Verilator.log)
 
Install litex python3 dependencies
```
cd ~
python3 -m pip install ninja
python3 -m pip install meson==0.59
export PATH=$PATH:~/.local/bin
```
[Install litex python3 dependencies.log](https://github.com/bol-edu/litex-lab/files/11359085/Install.litex.python3.dependencies.log)

## Install and run litex
```
git clone https://github.com/litex-hub/linux-on-litex-vexriscv
cd linux-on-litex-vexriscv
wget https://raw.githubusercontent.com/enjoy-digital/litex/master/litex_setup.py
chmod +x litex_setup.py
./litex_setup.py --init --install --user --config=full
./litex_setup.py --update
sudo ./litex_setup.py --gcc=riscv (enter yes)
~/litex-boards/litex_boards/targets/xilinx_kv260.py
wget -O linux_2022_03_23.zip  https://github.com/litex-hub/linux-on-litex-vexriscv/files/8331338/linux_2022_03_23.zip
unzip linux_2022_03_23.zip -d ./images (enter yes)
./sim.py
```
[Install and run litex.log](https://github.com/bol-edu/litex-lab/files/11359122/Install.and.run.litex.log)

