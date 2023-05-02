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
/ /  (_) /____ | |/_/
      / /__/ / __/ -_)>  <
     /____/_/\__/\__/_/|_|
   Build your hardware, easily!

 (c) Copyright 2012-2023 Enjoy-Digital
 (c) Copyright 2007-2015 M-Labs

 BIOS built on Apr 29 2023 12:55:42
 BIOS CRC passed (e36842e7)

 LiteX git sha1: 34ec22f8

--=============== SoC ==================--
CPU:            VexRiscv SMP-LINUX @ 100MHz
BUS:            WISHBONE 32-bit @ 4GiB
CSR:            32-bit data
ROM:            64.0KiB
SRAM:           8.0KiB
SDRAM:          64.0MiB 32-bit @ 100MT/s (CL-2 CWL-2)
MAIN-RAM:       64.0MiB

--========== Initialization ============--
Initializing SDRAM @0x40000000...
Switching SDRAM to software control.
Switching SDRAM to hardware control.

--============== Boot ==================--
Booting from serial...
Press Q or ESC to abort boot completely.
sL5DdSMmkekro
Timeout
Executing booted program at 0x40f00000

--============= Liftoff! ===============--

OpenSBI v0.8-1-gecf7701
   ____                    _____ ____ _____
  / __ \                  / ____|  _ \_   _|
 | |  | |_ __   ___ _ __ | (___ | |_) || |
 | |  | | '_ \ / _ \ '_ \ \___ \|  _ < | |
 | |__| | |_) |  __/ | | |____) | |_) || |_
  \____/| .__/ \___|_| |_|_____/|____/_____|
        | |
        |_|

Platform Name       : LiteX / VexRiscv-SMP
Platform Features   : timer,mfdeleg
Platform HART Count : 8
Boot HART ID        : 0
Boot HART ISA       : rv32imas
BOOT HART Features  : time
BOOT HART PMP Count : 0
Firmware Base       : 0x40f00000
Firmware Size       : 124 KB
Runtime SBI Version : 0.2

MIDELEG : 0x00000222
MEDELEG : 0x0000b101
[    0.000000] Linux version 5.14.0 (florent@panda) (riscv32-buildroot-linux-gnu-gcc.br_real (Buildroot 2021.08-381-g279167ee8d) 10.3.0, GNU ld (GNU Binutils) 2.36.1) #1 SMP Tue Sep 21 12:57:31 CEST 2021
[    0.000000] earlycon: liteuart0 at I/O port 0x0 (options '')
[    0.000000] Malformed early option 'console'
[    0.000000] earlycon: liteuart0 at MMIO 0xf0001000 (options '')
[    0.000000] printk: bootconsole [liteuart0] enabled
[    0.000000] Zone ranges:
[    0.000000]   Normal   [mem 0x0000000040000000-0x0000000043ffffff]
[    0.000000] Movable zone start for each node
[    0.000000] Early memory node ranges
[    0.000000]   node   0: [mem 0x0000000040000000-0x0000000043ffffff]
[    0.000000] Initmem setup node 0 [mem 0x0000000040000000-0x0000000043ffffff]
[    0.000000] SBI specification v0.2 detected
[    0.000000] SBI implementation ID=0x1 Version=0x8
[    0.000000] SBI TIME extension detected
[    0.000000] SBI IPI extension detected
[    0.000000] SBI RFENCE extension detected
[    0.000000] SBI v0.2 HSM extension detected
[    0.000000] riscv: ISA extensions aimp
[    0.000000] riscv: ELF capabilities aim
[    0.000000] percpu: Embedded 8 pages/cpu s11340 r0 d21428 u32768
[    0.000000] Built 1 zonelists, mobility grouping on.  Total pages: 16256
[    0.000000] Kernel command line: console=liteuart earlycon=liteuart,0xf0001000 rootwait root=/dev/ram0
[    0.000000] Dentry cache hash table entries: 8192 (order: 3, 32768 bytes, linear)
[    0.000000] Inode-cache hash table entries: 4096 (order: 2, 16384 bytes, linear)
[    0.000000] Sorting __ex_table...
[    0.000000] mem auto-init: stack:off, heap alloc:off, heap free:off
[    0.000000] Memory: 48644K/65536K available (5685K kernel code, 572K rwdata, 883K rodata, 209K init, 221K bss, 16892K reserved, 0K cma-reserved)
[    0.000000] SLUB: HWalign=64, Order=0-3, MinObjects=0, CPUs=1, Nodes=1
[    0.000000] rcu: Hierarchical RCU implementation.
[    0.000000] rcu:     RCU restricting CPUs from NR_CPUS=8 to nr_cpu_ids=1.
[    0.000000] rcu: RCU calculated value of scheduler-enlistment delay is 25 jiffies.
[    0.000000] rcu: Adjusting geometry for rcu_fanout_leaf=16, nr_cpu_ids=1
[    0.000000] NR_IRQS: 64, nr_irqs: 64, preallocated irqs: 0
[    0.000000] riscv-intc: 32 local interrupts mapped
[    0.000000] plic: interrupt-controller@f0c00000: mapped 32 interrupts with 1 handlers for 2 contexts.
[    0.000000] random: get_random_bytes called from start_kernel+0x4ac/0x63c with crng_init=0
[    0.000000] riscv_timer_init_dt: Registering clocksource cpuid [0] hartid [0]
[    0.000000] clocksource: riscv_clocksource: mask: 0xffffffffffffffff max_cycles: 0x171024e7e0, max_idle_ns: 440795205315 ns
[    0.000017] sched_clock: 64 bits at 100MHz, resolution 10ns, wraps every 4398046511100ns
[    0.002164] Console: colour dummy device 80x25
[    0.003097] Calibrating delay loop (skipped), value calculated using timer frequency.. 200.00 BogoMIPS (lpj=400000)
[    0.004634] pid_max: default: 32768 minimum: 301
[    0.008055] Mount-cache hash table entries: 1024 (order: 0, 4096 bytes, linear)
[    0.009092] Mountpoint-cache hash table entries: 1024 (order: 0, 4096 bytes, linear)
[    0.029602] ASID allocator using 9 bits (512 entries)
[    0.032202] rcu: Hierarchical SRCU implementation.
[    0.037673] smp: Bringing up secondary CPUs ...
[    0.038235] smp: Brought up 1 node, 1 CPU
[    0.043649] devtmpfs: initialized
[    0.067172] clocksource: jiffies: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 7645041785100000 ns
[    0.068496] futex hash table entries: 256 (order: 2, 16384 bytes, linear)
[    0.076186] NET: Registered PF_NETLINK/PF_ROUTE protocol family
[    0.219368] pps_core: LinuxPPS API ver. 1 registered
[    0.219903] pps_core: Software ver. 5.3.6 - Copyright 2005-2007 Rodolfo Giometti <giometti@linux.it>
[    0.221322] PTP clock support registered
[    0.224488] FPGA manager framework
[    0.237864] clocksource: Switched to clocksource riscv_clocksource
[    0.388310] NET: Registered PF_INET protocol family
[    0.390444] IP idents hash table entries: 2048 (order: 2, 16384 bytes, linear)
[    0.397993] tcp_listen_portaddr_hash hash table entries: 512 (order: 0, 6144 bytes, linear)
[    0.399314] TCP established hash table entries: 1024 (order: 0, 4096 bytes, linear)
[    0.400543] TCP bind hash table entries: 1024 (order: 1, 8192 bytes, linear)
[    0.401753] TCP: Hash tables configured (established 1024 bind 1024)
[    0.403182] UDP hash table entries: 256 (order: 1, 8192 bytes, linear)
[    0.404274] UDP-Lite hash table entries: 256 (order: 1, 8192 bytes, linear)
[    0.422111] Unpacking initramfs...
[    0.457924] workingset: timestamp_bits=30 max_order=14 bucket_order=0
[    0.665012] io scheduler mq-deadline registered
[    0.665874] io scheduler kyber registered
[    0.914509] LiteX SoC Controller driver initialized
[    4.159431] Freeing initrd memory: 8192K
[    4.663497] f0001000.serial: ttyLXU0 at MMIO 0x0 (irq = 0, base_baud = 0) is a liteuart
[    4.664780] printk: console [liteuart0] enabled
[    4.664780] printk: console [liteuart0] enabled
[    4.665718] printk: bootconsole [liteuart0] disabled
[    4.665718] printk: bootconsole [liteuart0] disabled
[    4.686406] i2c_dev: i2c /dev entries driver
[    4.723480] NET: Registered PF_INET6 protocol family
[    4.736993] Segment Routing with IPv6
[    4.738084] In-situ OAM (IOAM) with IPv6
[    4.739621] sit: IPv6, IPv4 and MPLS over IPv4 tunneling driver
[    4.752560] NET: Registered PF_PACKET protocol family
[    4.764135] Freeing unused kernel image (initmem) memory: 204K
[    4.764911] Kernel memory protection not selected by kernel config.
[    4.766185] Run /init as init process
Starting syslogd: OK
Starting klogd: OK
Running sysctl: OK
Saving random seed: [    6.822677] random: dd: uninitialized urandom read (512 bytes read)
OK
Starting network: OK

Welcome to Buildroot
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
sudo apt install libtool automake pkg-config libusb-1.0-0-dev -y
git clone https://github.com/ntfreak/openocd.git
cd openocd
./bootstrap
./configure --enable-ftdi
sudo make install
```
[Install OpenOCD.log](https://github.com/bol-edu/litex-lab/files/11359260/Install.OpenOCD.log)

Build the kv260 bitstream
```
ToDo..
```
