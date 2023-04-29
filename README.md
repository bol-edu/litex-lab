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
* Install basic tools and dependencies
* Compile and install latest Verilator
* Install litex python3 dependencies

Install basic tools and dependencies
```
sudo apt update
sudo apt install make build-essential device-tree-compiler wget git python3-setuptools python3-pip -y
sudo apt-get install libsdl2-dev -y
sudo apt install libevent-dev libjson-c-dev -y
```
```console
kevin@kevin:~$ sudo apt update
Hit:1 http://tw.archive.ubuntu.com/ubuntu focal InRelease
Get:2 http://tw.archive.ubuntu.com/ubuntu focal-updates InRelease [114 kB]
Get:3 http://tw.archive.ubuntu.com/ubuntu focal-backports InRelease [108 kB]
Get:4 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 DEP-11 Metadata [275 kB]
Get:5 http://tw.archive.ubuntu.com/ubuntu focal-updates/universe amd64 DEP-11 Metadata [410 kB]
Get:6 http://tw.archive.ubuntu.com/ubuntu focal-updates/multiverse amd64 DEP-11 Metadata [944 B]
Get:7 http://tw.archive.ubuntu.com/ubuntu focal-backports/main amd64 DEP-11 Metadata [7980 B]
Get:8 http://tw.archive.ubuntu.com/ubuntu focal-backports/universe amd64 DEP-11 Metadata [30.5 kB]
Get:9 http://security.ubuntu.com/ubuntu focal-security InRelease [114 kB]
Fetched 1060 kB in 2s (545 kB/s)
Reading package lists... Done
Building dependency tree
Reading state information... Done
98 packages can be upgraded. Run 'apt list --upgradable' to see them.
kevin@kevin:~$ sudo apt install make build-essential device-tree-compiler wget git python3-setuptools python3-pip -y
Reading package lists... Done
Building dependency tree
Reading state information... Done
wget is already the newest version (1.20.3-1ubuntu2).
wget set to manually installed.
The following additional packages will be installed:
  binutils binutils-common binutils-x86-64-linux-gnu dpkg-dev fakeroot g++ g++-9 gcc gcc-9 git-man libalgorithm-diff-perl libalgorithm-diff-xs-perl
  libalgorithm-merge-perl libasan5 libbinutils libc-dev-bin libc6-dev libcrypt-dev libctf-nobfd0 libctf0 liberror-perl libexpat1-dev libfakeroot libfdt1
  libgcc-9-dev libitm1 liblsan0 libpython3-dev libpython3.8 libpython3.8-dev libpython3.8-minimal libpython3.8-stdlib libquadmath0 libstdc++-9-dev libtsan0
  libubsan1 linux-libc-dev manpages-dev python-pip-whl python3-dev python3-distutils python3-wheel python3.8 python3.8-dev python3.8-minimal zlib1g-dev
Suggested packages:
  binutils-doc debian-keyring g++-multilib g++-9-multilib gcc-9-doc gcc-multilib autoconf automake libtool flex bison gcc-doc gcc-9-multilib gcc-9-locales
  git-daemon-run | git-daemon-sysvinit git-doc git-el git-email git-gui gitk gitweb git-cvs git-mediawiki git-svn glibc-doc libstdc++-9-doc make-doc
  python-setuptools-doc python3.8-venv python3.8-doc binfmt-support
The following NEW packages will be installed:
  binutils binutils-common binutils-x86-64-linux-gnu build-essential device-tree-compiler dpkg-dev fakeroot g++ g++-9 gcc gcc-9 git git-man
  libalgorithm-diff-perl libalgorithm-diff-xs-perl libalgorithm-merge-perl libasan5 libbinutils libc-dev-bin libc6-dev libcrypt-dev libctf-nobfd0 libctf0
  liberror-perl libexpat1-dev libfakeroot libfdt1 libgcc-9-dev libitm1 liblsan0 libpython3-dev libpython3.8-dev libquadmath0 libstdc++-9-dev libtsan0
  libubsan1 linux-libc-dev make manpages-dev python-pip-whl python3-dev python3-distutils python3-pip python3-setuptools python3-wheel python3.8-dev
  zlib1g-dev
The following packages will be upgraded:
  libpython3.8 libpython3.8-minimal libpython3.8-stdlib python3.8 python3.8-minimal
5 upgraded, 47 newly installed, 0 to remove and 93 not upgraded.
Need to get 49.8 MB/56.1 MB of archives.
After this operation, 238 MB of additional disk space will be used.
Get:1 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 binutils-common amd64 2.34-6ubuntu1.4 [207 kB]
Get:2 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libbinutils amd64 2.34-6ubuntu1.4 [474 kB]
Get:3 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libctf-nobfd0 amd64 2.34-6ubuntu1.4 [47.2 kB]
Get:4 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libctf0 amd64 2.34-6ubuntu1.4 [46.6 kB]
Get:5 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 binutils-x86-64-linux-gnu amd64 2.34-6ubuntu1.4 [1613 kB]
Get:6 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 binutils amd64 2.34-6ubuntu1.4 [3380 B]
Get:7 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libc-dev-bin amd64 2.31-0ubuntu9.9 [71.8 kB]
Get:8 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 linux-libc-dev amd64 5.4.0-148.165 [1120 kB]
Get:9 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libcrypt-dev amd64 1:4.4.10-10ubuntu4 [104 kB]
Get:10 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libc6-dev amd64 2.31-0ubuntu9.9 [2519 kB]
Get:11 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libitm1 amd64 10.3.0-1ubuntu1~20.04 [26.2 kB]
Get:12 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libasan5 amd64 9.4.0-1ubuntu1~20.04.1 [2751 kB]
Get:13 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 liblsan0 amd64 10.3.0-1ubuntu1~20.04 [835 kB]
Get:14 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libtsan0 amd64 10.3.0-1ubuntu1~20.04 [2009 kB]
Get:15 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libubsan1 amd64 10.3.0-1ubuntu1~20.04 [784 kB]
Get:16 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libquadmath0 amd64 10.3.0-1ubuntu1~20.04 [146 kB]
Get:17 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libgcc-9-dev amd64 9.4.0-1ubuntu1~20.04.1 [2359 kB]
Get:18 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 gcc-9 amd64 9.4.0-1ubuntu1~20.04.1 [8274 kB]
Get:19 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 gcc amd64 4:9.3.0-1ubuntu2 [5208 B]
Get:20 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libstdc++-9-dev amd64 9.4.0-1ubuntu1~20.04.1 [1722 kB]
Get:21 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 g++-9 amd64 9.4.0-1ubuntu1~20.04.1 [8420 kB]
Get:22 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 g++ amd64 4:9.3.0-1ubuntu2 [1604 B]
Get:23 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 make amd64 4.2.1-1.2 [162 kB]
Get:24 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 dpkg-dev all 1.19.7ubuntu3.2 [679 kB]
Get:25 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 build-essential amd64 12.8ubuntu1.1 [4664 B]
Get:26 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libfakeroot amd64 1.24-1 [25.7 kB]
Get:27 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 fakeroot amd64 1.24-1 [62.6 kB]
Get:28 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 liberror-perl all 0.17029-1 [26.5 kB]
Get:29 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 git-man all 1:2.25.1-1ubuntu3.10 [887 kB]
Get:30 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 git amd64 1:2.25.1-1ubuntu3.10 [4534 kB]
Get:31 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libalgorithm-diff-perl all 1.19.03-2 [46.6 kB]
Get:32 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libalgorithm-diff-xs-perl amd64 0.04-6 [11.3 kB]
Get:33 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libalgorithm-merge-perl all 0.08-3 [12.0 kB]
Get:34 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libexpat1-dev amd64 2.2.9-1ubuntu0.6 [116 kB]
Get:35 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libpython3.8-dev amd64 3.8.10-0ubuntu1~20.04.7 [3953 kB]
Get:36 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libpython3-dev amd64 3.8.2-0ubuntu2 [7236 B]
Get:37 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 manpages-dev all 5.05-1 [2266 kB]
Get:38 http://tw.archive.ubuntu.com/ubuntu focal-updates/universe amd64 python-pip-whl all 20.0.2-5ubuntu1.8 [1805 kB]
Get:39 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 zlib1g-dev amd64 1:1.2.11.dfsg-2ubuntu1.5 [155 kB]
Get:40 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 python3.8-dev amd64 3.8.10-0ubuntu1~20.04.7 [514 kB]
Get:41 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 python3-distutils all 3.8.10-0ubuntu1~20.04 [141 kB]
Get:42 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 python3-dev amd64 3.8.2-0ubuntu2 [1212 B]
Get:43 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 python3-setuptools all 45.2.0-1ubuntu0.1 [330 kB]
Get:44 http://tw.archive.ubuntu.com/ubuntu focal-updates/universe amd64 python3-wheel all 0.34.2-1ubuntu0.1 [23.9 kB]
Get:45 http://tw.archive.ubuntu.com/ubuntu focal-updates/universe amd64 python3-pip all 20.0.2-5ubuntu1.8 [231 kB]
Get:46 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libfdt1 amd64 1.5.1-1 [18.8 kB]
Get:47 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 device-tree-compiler amd64 1.5.1-1 [247 kB]
Fetched 49.8 MB in 2s (23.3 MB/s)
Extracting templates from packages: 100%
(Reading database ... 182403 files and directories currently installed.)
Preparing to unpack .../00-libpython3.8_3.8.10-0ubuntu1~20.04.7_amd64.deb ...
Unpacking libpython3.8:amd64 (3.8.10-0ubuntu1~20.04.7) over (3.8.10-0ubuntu1~20.04.6) ...
Preparing to unpack .../01-python3.8_3.8.10-0ubuntu1~20.04.7_amd64.deb ...
Unpacking python3.8 (3.8.10-0ubuntu1~20.04.7) over (3.8.10-0ubuntu1~20.04.6) ...
Preparing to unpack .../02-libpython3.8-stdlib_3.8.10-0ubuntu1~20.04.7_amd64.deb ...
Unpacking libpython3.8-stdlib:amd64 (3.8.10-0ubuntu1~20.04.7) over (3.8.10-0ubuntu1~20.04.6) ...
Preparing to unpack .../03-python3.8-minimal_3.8.10-0ubuntu1~20.04.7_amd64.deb ...
Unpacking python3.8-minimal (3.8.10-0ubuntu1~20.04.7) over (3.8.10-0ubuntu1~20.04.6) ...
Preparing to unpack .../04-libpython3.8-minimal_3.8.10-0ubuntu1~20.04.7_amd64.deb ...
Unpacking libpython3.8-minimal:amd64 (3.8.10-0ubuntu1~20.04.7) over (3.8.10-0ubuntu1~20.04.6) ...
Selecting previously unselected package binutils-common:amd64.
Preparing to unpack .../05-binutils-common_2.34-6ubuntu1.4_amd64.deb ...
Unpacking binutils-common:amd64 (2.34-6ubuntu1.4) ...
Selecting previously unselected package libbinutils:amd64.
Preparing to unpack .../06-libbinutils_2.34-6ubuntu1.4_amd64.deb ...
Unpacking libbinutils:amd64 (2.34-6ubuntu1.4) ...
Selecting previously unselected package libctf-nobfd0:amd64.
Preparing to unpack .../07-libctf-nobfd0_2.34-6ubuntu1.4_amd64.deb ...
Unpacking libctf-nobfd0:amd64 (2.34-6ubuntu1.4) ...
Selecting previously unselected package libctf0:amd64.
Preparing to unpack .../08-libctf0_2.34-6ubuntu1.4_amd64.deb ...
Unpacking libctf0:amd64 (2.34-6ubuntu1.4) ...
Selecting previously unselected package binutils-x86-64-linux-gnu.
Preparing to unpack .../09-binutils-x86-64-linux-gnu_2.34-6ubuntu1.4_amd64.deb ...
Unpacking binutils-x86-64-linux-gnu (2.34-6ubuntu1.4) ...
Selecting previously unselected package binutils.
Preparing to unpack .../10-binutils_2.34-6ubuntu1.4_amd64.deb ...
Unpacking binutils (2.34-6ubuntu1.4) ...
Selecting previously unselected package libc-dev-bin.
Preparing to unpack .../11-libc-dev-bin_2.31-0ubuntu9.9_amd64.deb ...
Unpacking libc-dev-bin (2.31-0ubuntu9.9) ...
Selecting previously unselected package linux-libc-dev:amd64.
Preparing to unpack .../12-linux-libc-dev_5.4.0-148.165_amd64.deb ...
Unpacking linux-libc-dev:amd64 (5.4.0-148.165) ...
Selecting previously unselected package libcrypt-dev:amd64.
Preparing to unpack .../13-libcrypt-dev_1%3a4.4.10-10ubuntu4_amd64.deb ...
Unpacking libcrypt-dev:amd64 (1:4.4.10-10ubuntu4) ...
Selecting previously unselected package libc6-dev:amd64.
Preparing to unpack .../14-libc6-dev_2.31-0ubuntu9.9_amd64.deb ...
Unpacking libc6-dev:amd64 (2.31-0ubuntu9.9) ...
Selecting previously unselected package libitm1:amd64.
Preparing to unpack .../15-libitm1_10.3.0-1ubuntu1~20.04_amd64.deb ...
Unpacking libitm1:amd64 (10.3.0-1ubuntu1~20.04) ...
Selecting previously unselected package libasan5:amd64.
Preparing to unpack .../16-libasan5_9.4.0-1ubuntu1~20.04.1_amd64.deb ...
Unpacking libasan5:amd64 (9.4.0-1ubuntu1~20.04.1) ...
Selecting previously unselected package liblsan0:amd64.
Preparing to unpack .../17-liblsan0_10.3.0-1ubuntu1~20.04_amd64.deb ...
Unpacking liblsan0:amd64 (10.3.0-1ubuntu1~20.04) ...
Selecting previously unselected package libtsan0:amd64.
Preparing to unpack .../18-libtsan0_10.3.0-1ubuntu1~20.04_amd64.deb ...
Unpacking libtsan0:amd64 (10.3.0-1ubuntu1~20.04) ...
Selecting previously unselected package libubsan1:amd64.
Preparing to unpack .../19-libubsan1_10.3.0-1ubuntu1~20.04_amd64.deb ...
Unpacking libubsan1:amd64 (10.3.0-1ubuntu1~20.04) ...
Selecting previously unselected package libquadmath0:amd64.
Preparing to unpack .../20-libquadmath0_10.3.0-1ubuntu1~20.04_amd64.deb ...
Unpacking libquadmath0:amd64 (10.3.0-1ubuntu1~20.04) ...
Selecting previously unselected package libgcc-9-dev:amd64.
Preparing to unpack .../21-libgcc-9-dev_9.4.0-1ubuntu1~20.04.1_amd64.deb ...
Unpacking libgcc-9-dev:amd64 (9.4.0-1ubuntu1~20.04.1) ...
Selecting previously unselected package gcc-9.
Preparing to unpack .../22-gcc-9_9.4.0-1ubuntu1~20.04.1_amd64.deb ...
Unpacking gcc-9 (9.4.0-1ubuntu1~20.04.1) ...
Selecting previously unselected package gcc.
Preparing to unpack .../23-gcc_4%3a9.3.0-1ubuntu2_amd64.deb ...
Unpacking gcc (4:9.3.0-1ubuntu2) ...
Selecting previously unselected package libstdc++-9-dev:amd64.
Preparing to unpack .../24-libstdc++-9-dev_9.4.0-1ubuntu1~20.04.1_amd64.deb ...
Unpacking libstdc++-9-dev:amd64 (9.4.0-1ubuntu1~20.04.1) ...
Selecting previously unselected package g++-9.
Preparing to unpack .../25-g++-9_9.4.0-1ubuntu1~20.04.1_amd64.deb ...
Unpacking g++-9 (9.4.0-1ubuntu1~20.04.1) ...
Selecting previously unselected package g++.
Preparing to unpack .../26-g++_4%3a9.3.0-1ubuntu2_amd64.deb ...
Unpacking g++ (4:9.3.0-1ubuntu2) ...
Selecting previously unselected package make.
Preparing to unpack .../27-make_4.2.1-1.2_amd64.deb ...
Unpacking make (4.2.1-1.2) ...
Selecting previously unselected package dpkg-dev.
Preparing to unpack .../28-dpkg-dev_1.19.7ubuntu3.2_all.deb ...
Unpacking dpkg-dev (1.19.7ubuntu3.2) ...
Selecting previously unselected package build-essential.
Preparing to unpack .../29-build-essential_12.8ubuntu1.1_amd64.deb ...
Unpacking build-essential (12.8ubuntu1.1) ...
Selecting previously unselected package libfakeroot:amd64.
Preparing to unpack .../30-libfakeroot_1.24-1_amd64.deb ...
Unpacking libfakeroot:amd64 (1.24-1) ...
Selecting previously unselected package fakeroot.
Preparing to unpack .../31-fakeroot_1.24-1_amd64.deb ...
Unpacking fakeroot (1.24-1) ...
Selecting previously unselected package liberror-perl.
Preparing to unpack .../32-liberror-perl_0.17029-1_all.deb ...
Unpacking liberror-perl (0.17029-1) ...
Selecting previously unselected package git-man.
Preparing to unpack .../33-git-man_1%3a2.25.1-1ubuntu3.10_all.deb ...
Unpacking git-man (1:2.25.1-1ubuntu3.10) ...
Selecting previously unselected package git.
Preparing to unpack .../34-git_1%3a2.25.1-1ubuntu3.10_amd64.deb ...
Unpacking git (1:2.25.1-1ubuntu3.10) ...
Selecting previously unselected package libalgorithm-diff-perl.
Preparing to unpack .../35-libalgorithm-diff-perl_1.19.03-2_all.deb ...
Unpacking libalgorithm-diff-perl (1.19.03-2) ...
Selecting previously unselected package libalgorithm-diff-xs-perl.
Preparing to unpack .../36-libalgorithm-diff-xs-perl_0.04-6_amd64.deb ...
Unpacking libalgorithm-diff-xs-perl (0.04-6) ...
Selecting previously unselected package libalgorithm-merge-perl.
Preparing to unpack .../37-libalgorithm-merge-perl_0.08-3_all.deb ...
Unpacking libalgorithm-merge-perl (0.08-3) ...
Selecting previously unselected package libexpat1-dev:amd64.
Preparing to unpack .../38-libexpat1-dev_2.2.9-1ubuntu0.6_amd64.deb ...
Unpacking libexpat1-dev:amd64 (2.2.9-1ubuntu0.6) ...
Selecting previously unselected package libpython3.8-dev:amd64.
Preparing to unpack .../39-libpython3.8-dev_3.8.10-0ubuntu1~20.04.7_amd64.deb ...
Unpacking libpython3.8-dev:amd64 (3.8.10-0ubuntu1~20.04.7) ...
Selecting previously unselected package libpython3-dev:amd64.
Preparing to unpack .../40-libpython3-dev_3.8.2-0ubuntu2_amd64.deb ...
Unpacking libpython3-dev:amd64 (3.8.2-0ubuntu2) ...
Selecting previously unselected package manpages-dev.
Preparing to unpack .../41-manpages-dev_5.05-1_all.deb ...
Unpacking manpages-dev (5.05-1) ...
Selecting previously unselected package python-pip-whl.
Preparing to unpack .../42-python-pip-whl_20.0.2-5ubuntu1.8_all.deb ...
Unpacking python-pip-whl (20.0.2-5ubuntu1.8) ...
Selecting previously unselected package zlib1g-dev:amd64.
Preparing to unpack .../43-zlib1g-dev_1%3a1.2.11.dfsg-2ubuntu1.5_amd64.deb ...
Unpacking zlib1g-dev:amd64 (1:1.2.11.dfsg-2ubuntu1.5) ...
Selecting previously unselected package python3.8-dev.
Preparing to unpack .../44-python3.8-dev_3.8.10-0ubuntu1~20.04.7_amd64.deb ...
Unpacking python3.8-dev (3.8.10-0ubuntu1~20.04.7) ...
Selecting previously unselected package python3-distutils.
Preparing to unpack .../45-python3-distutils_3.8.10-0ubuntu1~20.04_all.deb ...
Unpacking python3-distutils (3.8.10-0ubuntu1~20.04) ...
Selecting previously unselected package python3-dev.
Preparing to unpack .../46-python3-dev_3.8.2-0ubuntu2_amd64.deb ...
Unpacking python3-dev (3.8.2-0ubuntu2) ...
Selecting previously unselected package python3-setuptools.
Preparing to unpack .../47-python3-setuptools_45.2.0-1ubuntu0.1_all.deb ...
Unpacking python3-setuptools (45.2.0-1ubuntu0.1) ...
Selecting previously unselected package python3-wheel.
Preparing to unpack .../48-python3-wheel_0.34.2-1ubuntu0.1_all.deb ...
Unpacking python3-wheel (0.34.2-1ubuntu0.1) ...
Selecting previously unselected package python3-pip.
Preparing to unpack .../49-python3-pip_20.0.2-5ubuntu1.8_all.deb ...
Unpacking python3-pip (20.0.2-5ubuntu1.8) ...
Selecting previously unselected package libfdt1:amd64.
Preparing to unpack .../50-libfdt1_1.5.1-1_amd64.deb ...
Unpacking libfdt1:amd64 (1.5.1-1) ...
Selecting previously unselected package device-tree-compiler.
Preparing to unpack .../51-device-tree-compiler_1.5.1-1_amd64.deb ...
Unpacking device-tree-compiler (1.5.1-1) ...
Setting up python3-distutils (3.8.10-0ubuntu1~20.04) ...
Setting up manpages-dev (5.05-1) ...
Setting up libpython3.8-minimal:amd64 (3.8.10-0ubuntu1~20.04.7) ...
Setting up python3-setuptools (45.2.0-1ubuntu0.1) ...
Setting up libalgorithm-diff-perl (1.19.03-2) ...
Setting up binutils-common:amd64 (2.34-6ubuntu1.4) ...
Setting up linux-libc-dev:amd64 (5.4.0-148.165) ...
Setting up libctf-nobfd0:amd64 (2.34-6ubuntu1.4) ...
Setting up libfdt1:amd64 (1.5.1-1) ...
Setting up python3-wheel (0.34.2-1ubuntu0.1) ...
Setting up libfakeroot:amd64 (1.24-1) ...
Setting up fakeroot (1.24-1) ...
update-alternatives: using /usr/bin/fakeroot-sysv to provide /usr/bin/fakeroot (fakeroot) in auto mode
Setting up liberror-perl (0.17029-1) ...
Setting up libasan5:amd64 (9.4.0-1ubuntu1~20.04.1) ...
Setting up make (4.2.1-1.2) ...
Setting up libquadmath0:amd64 (10.3.0-1ubuntu1~20.04) ...
Setting up device-tree-compiler (1.5.1-1) ...
Setting up libubsan1:amd64 (10.3.0-1ubuntu1~20.04) ...
Setting up python3.8-minimal (3.8.10-0ubuntu1~20.04.7) ...
Setting up libcrypt-dev:amd64 (1:4.4.10-10ubuntu4) ...
Setting up git-man (1:2.25.1-1ubuntu3.10) ...
Setting up python-pip-whl (20.0.2-5ubuntu1.8) ...
Setting up libbinutils:amd64 (2.34-6ubuntu1.4) ...
Setting up libpython3.8-stdlib:amd64 (3.8.10-0ubuntu1~20.04.7) ...
Setting up libc-dev-bin (2.31-0ubuntu9.9) ...
Setting up python3.8 (3.8.10-0ubuntu1~20.04.7) ...
Setting up libalgorithm-diff-xs-perl (0.04-6) ...
Setting up liblsan0:amd64 (10.3.0-1ubuntu1~20.04) ...
Setting up libitm1:amd64 (10.3.0-1ubuntu1~20.04) ...
Setting up libalgorithm-merge-perl (0.08-3) ...
Setting up libtsan0:amd64 (10.3.0-1ubuntu1~20.04) ...
Setting up libctf0:amd64 (2.34-6ubuntu1.4) ...
Setting up libgcc-9-dev:amd64 (9.4.0-1ubuntu1~20.04.1) ...
Setting up libpython3.8:amd64 (3.8.10-0ubuntu1~20.04.7) ...
Setting up git (1:2.25.1-1ubuntu3.10) ...
Setting up python3-pip (20.0.2-5ubuntu1.8) ...
Setting up libc6-dev:amd64 (2.31-0ubuntu9.9) ...
Setting up binutils-x86-64-linux-gnu (2.34-6ubuntu1.4) ...
Setting up libstdc++-9-dev:amd64 (9.4.0-1ubuntu1~20.04.1) ...
Setting up binutils (2.34-6ubuntu1.4) ...
Setting up dpkg-dev (1.19.7ubuntu3.2) ...
Setting up libexpat1-dev:amd64 (2.2.9-1ubuntu0.6) ...
Setting up libpython3.8-dev:amd64 (3.8.10-0ubuntu1~20.04.7) ...
Setting up zlib1g-dev:amd64 (1:1.2.11.dfsg-2ubuntu1.5) ...
Setting up gcc-9 (9.4.0-1ubuntu1~20.04.1) ...
Setting up libpython3-dev:amd64 (3.8.2-0ubuntu2) ...
Setting up gcc (4:9.3.0-1ubuntu2) ...
Setting up g++-9 (9.4.0-1ubuntu1~20.04.1) ...
Setting up python3.8-dev (3.8.10-0ubuntu1~20.04.7) ...
Setting up g++ (4:9.3.0-1ubuntu2) ...
update-alternatives: using /usr/bin/g++ to provide /usr/bin/c++ (c++) in auto mode
Setting up build-essential (12.8ubuntu1.1) ...
Setting up python3-dev (3.8.2-0ubuntu2) ...
Processing triggers for mime-support (3.64ubuntu1) ...
Processing triggers for gnome-menus (3.36.0-1ubuntu1) ...
Processing triggers for libc-bin (2.31-0ubuntu9.9) ...
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for desktop-file-utils (0.24-1ubuntu3) ...
kevin@kevin:~$ sudo apt-get install libsdl2-dev -y
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
  libasound2-dev libblkid-dev libdbus-1-dev libegl-dev libegl1-mesa-dev libffi-dev libgl-dev libgl1-mesa-dev libgles-dev libgles1 libgles2-mesa-dev
  libglib2.0-dev libglib2.0-dev-bin libglu1-mesa-dev libglvnd-dev libglx-dev libibus-1.0-dev libice-dev libmount-dev libopengl-dev libpcre16-3 libpcre2-16-0
  libpcre2-dev libpcre2-posix2 libpcre3-dev libpcre32-3 libpcrecpp0v5 libpthread-stubs0-dev libpulse-dev libsdl2-2.0-0 libselinux1-dev libsepol1-dev
  libsm-dev libsndio-dev libsndio7.0 libudev-dev libwayland-bin libwayland-dev libx11-dev libxau-dev libxcb1-dev libxcursor-dev libxdmcp-dev libxext-dev
  libxfixes-dev libxi-dev libxinerama-dev libxkbcommon-dev libxrandr-dev libxrender-dev libxss-dev libxt-dev libxv-dev libxxf86vm-dev uuid-dev
  x11proto-core-dev x11proto-dev x11proto-input-dev x11proto-randr-dev x11proto-scrnsaver-dev x11proto-xext-dev x11proto-xf86vidmode-dev
  x11proto-xinerama-dev xorg-sgml-doctools xtrans-dev
Suggested packages:
  libasound2-doc libgirepository1.0-dev libglib2.0-doc libxml2-utils libice-doc libsm-doc sndiod libwayland-doc libx11-doc libxcb-doc libxext-doc libxt-doc
The following NEW packages will be installed:
  libasound2-dev libblkid-dev libdbus-1-dev libegl-dev libegl1-mesa-dev libffi-dev libgl-dev libgl1-mesa-dev libgles-dev libgles1 libgles2-mesa-dev
  libglib2.0-dev libglib2.0-dev-bin libglu1-mesa-dev libglvnd-dev libglx-dev libibus-1.0-dev libice-dev libmount-dev libopengl-dev libpcre16-3 libpcre2-16-0
  libpcre2-dev libpcre2-posix2 libpcre3-dev libpcre32-3 libpcrecpp0v5 libpthread-stubs0-dev libpulse-dev libsdl2-2.0-0 libsdl2-dev libselinux1-dev
  libsepol1-dev libsm-dev libsndio-dev libsndio7.0 libudev-dev libwayland-bin libwayland-dev libx11-dev libxau-dev libxcb1-dev libxcursor-dev libxdmcp-dev
  libxext-dev libxfixes-dev libxi-dev libxinerama-dev libxkbcommon-dev libxrandr-dev libxrender-dev libxss-dev libxt-dev libxv-dev libxxf86vm-dev uuid-dev
  x11proto-core-dev x11proto-dev x11proto-input-dev x11proto-randr-dev x11proto-scrnsaver-dev x11proto-xext-dev x11proto-xf86vidmode-dev
  x11proto-xinerama-dev xorg-sgml-doctools xtrans-dev
0 upgraded, 66 newly installed, 0 to remove and 93 not upgraded.
Need to get 8841 kB of archives.
After this operation, 47.5 MB of additional disk space will be used.
Get:1 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libasound2-dev amd64 1.2.2-2.1ubuntu2.5 [104 kB]
Get:2 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libdbus-1-dev amd64 1.12.16-2ubuntu2.3 [167 kB]
Get:3 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 xorg-sgml-doctools all 1:1.11-1 [12.9 kB]
Get:4 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 x11proto-dev all 2019.2-1ubuntu1 [594 kB]
Get:5 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 x11proto-core-dev all 2019.2-1ubuntu1 [2620 B]
Get:6 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libxau-dev amd64 1:1.0.9-0ubuntu1 [9552 B]
Get:7 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libxdmcp-dev amd64 1:1.1.3-0ubuntu1 [25.3 kB]
Get:8 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 xtrans-dev all 1.4.0-1 [68.9 kB]
Get:9 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libpthread-stubs0-dev amd64 0.4-1 [5384 B]
Get:10 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libxcb1-dev amd64 1.14-2 [80.5 kB]
Get:11 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libx11-dev amd64 2:1.6.9-2ubuntu1.2 [647 kB]
Get:12 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libglx-dev amd64 1.3.2-1~ubuntu0.20.04.2 [14.0 kB]
Get:13 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libgl-dev amd64 1.3.2-1~ubuntu0.20.04.2 [97.8 kB]
Get:14 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libegl-dev amd64 1.3.2-1~ubuntu0.20.04.2 [17.2 kB]
Get:15 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libgles1 amd64 1.3.2-1~ubuntu0.20.04.2 [10.3 kB]
Get:16 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libgles-dev amd64 1.3.2-1~ubuntu0.20.04.2 [47.9 kB]
Get:17 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libopengl-dev amd64 1.3.2-1~ubuntu0.20.04.2 [3584 B]
Get:18 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libglvnd-dev amd64 1.3.2-1~ubuntu0.20.04.2 [11.6 kB]
Get:19 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libegl1-mesa-dev amd64 21.2.6-0ubuntu0.1~20.04.2 [7760 B]
Get:20 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libgles2-mesa-dev amd64 21.2.6-0ubuntu0.1~20.04.2 [6424 B]
Get:21 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libffi-dev amd64 3.3-4 [57.0 kB]
Get:22 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libglib2.0-dev-bin amd64 2.64.6-1~ubuntu20.04.4 [109 kB]
Get:23 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 uuid-dev amd64 2.34-0.1ubuntu9.3 [33.6 kB]
Get:24 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libblkid-dev amd64 2.34-0.1ubuntu9.3 [167 kB]
Get:25 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libmount-dev amd64 2.34-0.1ubuntu9.3 [176 kB]
Get:26 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libpcre16-3 amd64 2:8.39-12ubuntu0.1 [150 kB]
Get:27 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libpcre32-3 amd64 2:8.39-12ubuntu0.1 [140 kB]
Get:28 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libpcrecpp0v5 amd64 2:8.39-12ubuntu0.1 [15.5 kB]
Get:29 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libpcre3-dev amd64 2:8.39-12ubuntu0.1 [540 kB]
Get:30 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libsepol1-dev amd64 3.0-1ubuntu0.1 [325 kB]
Get:31 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libpcre2-16-0 amd64 10.34-7ubuntu0.1 [181 kB]
Get:32 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libpcre2-posix2 amd64 10.34-7ubuntu0.1 [5988 B]
Get:33 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libpcre2-dev amd64 10.34-7ubuntu0.1 [672 kB]
Get:34 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libselinux1-dev amd64 3.0-1build2 [151 kB]
Get:35 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libglib2.0-dev amd64 2.64.6-1~ubuntu20.04.4 [1506 kB]
Get:36 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libgl1-mesa-dev amd64 21.2.6-0ubuntu0.1~20.04.2 [6420 B]
Get:37 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libglu1-mesa-dev amd64 9.0.1-1build1 [207 kB]
Get:38 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libibus-1.0-dev amd64 1.5.22-2ubuntu2.1 [179 kB]
Get:39 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libice-dev amd64 2:1.0.10-0ubuntu1 [47.8 kB]
Get:40 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libpulse-dev amd64 1:13.99.1-1ubuntu3.13 [72.5 kB]
Get:41 http://tw.archive.ubuntu.com/ubuntu focal/universe amd64 libsdl2-2.0-0 amd64 2.0.10+dfsg1-3 [407 kB]
Get:42 http://tw.archive.ubuntu.com/ubuntu focal/universe amd64 libsndio7.0 amd64 1.5.0-3 [24.5 kB]
Get:43 http://tw.archive.ubuntu.com/ubuntu focal/universe amd64 libsndio-dev amd64 1.5.0-3 [13.6 kB]
Get:44 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libudev-dev amd64 245.4-4ubuntu3.21 [19.7 kB]
Get:45 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libwayland-bin amd64 1.18.0-1ubuntu0.1 [20.2 kB]
Get:46 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libwayland-dev amd64 1.18.0-1ubuntu0.1 [64.6 kB]
Get:47 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libxrender-dev amd64 1:0.9.10-1 [24.9 kB]
Get:48 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libxfixes-dev amd64 1:5.0.3-2 [11.4 kB]
Get:49 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libxcursor-dev amd64 1:1.2.0-2 [26.5 kB]
Get:50 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 x11proto-xext-dev all 2019.2-1ubuntu1 [2616 B]
Get:51 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libxext-dev amd64 2:1.3.4-0ubuntu1 [82.2 kB]
Get:52 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 x11proto-input-dev all 2019.2-1ubuntu1 [2628 B]
Get:53 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libxi-dev amd64 2:1.7.10-0ubuntu1 [187 kB]
Get:54 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 x11proto-xinerama-dev all 2019.2-1ubuntu1 [2628 B]
Get:55 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libxinerama-dev amd64 2:1.1.4-2 [7896 B]
Get:56 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libxkbcommon-dev amd64 0.10.0-1 [45.4 kB]
Get:57 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 x11proto-randr-dev all 2019.2-1ubuntu1 [2620 B]
Get:58 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libxrandr-dev amd64 2:1.5.2-0ubuntu1 [25.0 kB]
Get:59 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 x11proto-scrnsaver-dev all 2019.2-1ubuntu1 [2624 B]
Get:60 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libxss-dev amd64 1:1.2.3-1 [11.9 kB]
Get:61 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libsm-dev amd64 2:1.2.3-1 [17.0 kB]
Get:62 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libxt-dev amd64 1:1.1.5-1 [395 kB]
Get:63 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libxv-dev amd64 2:1.0.11-1 [32.5 kB]
Get:64 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 x11proto-xf86vidmode-dev all 2019.2-1ubuntu1 [2624 B]
Get:65 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libxxf86vm-dev amd64 1:1.1.4-1build1 [13.3 kB]
Get:66 http://tw.archive.ubuntu.com/ubuntu focal/universe amd64 libsdl2-dev amd64 2.0.10+dfsg1-3 [718 kB]
Fetched 8841 kB in 1s (16.9 MB/s)
Extracting templates from packages: 100%
Selecting previously unselected package libasound2-dev:amd64.
(Reading database ... 189469 files and directories currently installed.)
Preparing to unpack .../00-libasound2-dev_1.2.2-2.1ubuntu2.5_amd64.deb ...
Unpacking libasound2-dev:amd64 (1.2.2-2.1ubuntu2.5) ...
Selecting previously unselected package libdbus-1-dev:amd64.
Preparing to unpack .../01-libdbus-1-dev_1.12.16-2ubuntu2.3_amd64.deb ...
Unpacking libdbus-1-dev:amd64 (1.12.16-2ubuntu2.3) ...
Selecting previously unselected package xorg-sgml-doctools.
Preparing to unpack .../02-xorg-sgml-doctools_1%3a1.11-1_all.deb ...
Unpacking xorg-sgml-doctools (1:1.11-1) ...
Selecting previously unselected package x11proto-dev.
Preparing to unpack .../03-x11proto-dev_2019.2-1ubuntu1_all.deb ...
Unpacking x11proto-dev (2019.2-1ubuntu1) ...
Selecting previously unselected package x11proto-core-dev.
Preparing to unpack .../04-x11proto-core-dev_2019.2-1ubuntu1_all.deb ...
Unpacking x11proto-core-dev (2019.2-1ubuntu1) ...
Selecting previously unselected package libxau-dev:amd64.
Preparing to unpack .../05-libxau-dev_1%3a1.0.9-0ubuntu1_amd64.deb ...
Unpacking libxau-dev:amd64 (1:1.0.9-0ubuntu1) ...
Selecting previously unselected package libxdmcp-dev:amd64.
Preparing to unpack .../06-libxdmcp-dev_1%3a1.1.3-0ubuntu1_amd64.deb ...
Unpacking libxdmcp-dev:amd64 (1:1.1.3-0ubuntu1) ...
Selecting previously unselected package xtrans-dev.
Preparing to unpack .../07-xtrans-dev_1.4.0-1_all.deb ...
Unpacking xtrans-dev (1.4.0-1) ...
Selecting previously unselected package libpthread-stubs0-dev:amd64.
Preparing to unpack .../08-libpthread-stubs0-dev_0.4-1_amd64.deb ...
Unpacking libpthread-stubs0-dev:amd64 (0.4-1) ...
Selecting previously unselected package libxcb1-dev:amd64.
Preparing to unpack .../09-libxcb1-dev_1.14-2_amd64.deb ...
Unpacking libxcb1-dev:amd64 (1.14-2) ...
Selecting previously unselected package libx11-dev:amd64.
Preparing to unpack .../10-libx11-dev_2%3a1.6.9-2ubuntu1.2_amd64.deb ...
Unpacking libx11-dev:amd64 (2:1.6.9-2ubuntu1.2) ...
Selecting previously unselected package libglx-dev:amd64.
Preparing to unpack .../11-libglx-dev_1.3.2-1~ubuntu0.20.04.2_amd64.deb ...
Unpacking libglx-dev:amd64 (1.3.2-1~ubuntu0.20.04.2) ...
Selecting previously unselected package libgl-dev:amd64.
Preparing to unpack .../12-libgl-dev_1.3.2-1~ubuntu0.20.04.2_amd64.deb ...
Unpacking libgl-dev:amd64 (1.3.2-1~ubuntu0.20.04.2) ...
Selecting previously unselected package libegl-dev:amd64.
Preparing to unpack .../13-libegl-dev_1.3.2-1~ubuntu0.20.04.2_amd64.deb ...
Unpacking libegl-dev:amd64 (1.3.2-1~ubuntu0.20.04.2) ...
Selecting previously unselected package libgles1:amd64.
Preparing to unpack .../14-libgles1_1.3.2-1~ubuntu0.20.04.2_amd64.deb ...
Unpacking libgles1:amd64 (1.3.2-1~ubuntu0.20.04.2) ...
Selecting previously unselected package libgles-dev:amd64.
Preparing to unpack .../15-libgles-dev_1.3.2-1~ubuntu0.20.04.2_amd64.deb ...
Unpacking libgles-dev:amd64 (1.3.2-1~ubuntu0.20.04.2) ...
Selecting previously unselected package libopengl-dev:amd64.
Preparing to unpack .../16-libopengl-dev_1.3.2-1~ubuntu0.20.04.2_amd64.deb ...
Unpacking libopengl-dev:amd64 (1.3.2-1~ubuntu0.20.04.2) ...
Selecting previously unselected package libglvnd-dev:amd64.
Preparing to unpack .../17-libglvnd-dev_1.3.2-1~ubuntu0.20.04.2_amd64.deb ...
Unpacking libglvnd-dev:amd64 (1.3.2-1~ubuntu0.20.04.2) ...
Selecting previously unselected package libegl1-mesa-dev:amd64.
Preparing to unpack .../18-libegl1-mesa-dev_21.2.6-0ubuntu0.1~20.04.2_amd64.deb ...
Unpacking libegl1-mesa-dev:amd64 (21.2.6-0ubuntu0.1~20.04.2) ...
Selecting previously unselected package libgles2-mesa-dev:amd64.
Preparing to unpack .../19-libgles2-mesa-dev_21.2.6-0ubuntu0.1~20.04.2_amd64.deb ...
Unpacking libgles2-mesa-dev:amd64 (21.2.6-0ubuntu0.1~20.04.2) ...
Selecting previously unselected package libffi-dev:amd64.
Preparing to unpack .../20-libffi-dev_3.3-4_amd64.deb ...
Unpacking libffi-dev:amd64 (3.3-4) ...
Selecting previously unselected package libglib2.0-dev-bin.
Preparing to unpack .../21-libglib2.0-dev-bin_2.64.6-1~ubuntu20.04.4_amd64.deb ...
Unpacking libglib2.0-dev-bin (2.64.6-1~ubuntu20.04.4) ...
Selecting previously unselected package uuid-dev:amd64.
Preparing to unpack .../22-uuid-dev_2.34-0.1ubuntu9.3_amd64.deb ...
Unpacking uuid-dev:amd64 (2.34-0.1ubuntu9.3) ...
Selecting previously unselected package libblkid-dev:amd64.
Preparing to unpack .../23-libblkid-dev_2.34-0.1ubuntu9.3_amd64.deb ...
Unpacking libblkid-dev:amd64 (2.34-0.1ubuntu9.3) ...
Selecting previously unselected package libmount-dev:amd64.
Preparing to unpack .../24-libmount-dev_2.34-0.1ubuntu9.3_amd64.deb ...
Unpacking libmount-dev:amd64 (2.34-0.1ubuntu9.3) ...
Selecting previously unselected package libpcre16-3:amd64.
Preparing to unpack .../25-libpcre16-3_2%3a8.39-12ubuntu0.1_amd64.deb ...
Unpacking libpcre16-3:amd64 (2:8.39-12ubuntu0.1) ...
Selecting previously unselected package libpcre32-3:amd64.
Preparing to unpack .../26-libpcre32-3_2%3a8.39-12ubuntu0.1_amd64.deb ...
Unpacking libpcre32-3:amd64 (2:8.39-12ubuntu0.1) ...
Selecting previously unselected package libpcrecpp0v5:amd64.
Preparing to unpack .../27-libpcrecpp0v5_2%3a8.39-12ubuntu0.1_amd64.deb ...
Unpacking libpcrecpp0v5:amd64 (2:8.39-12ubuntu0.1) ...
Selecting previously unselected package libpcre3-dev:amd64.
Preparing to unpack .../28-libpcre3-dev_2%3a8.39-12ubuntu0.1_amd64.deb ...
Unpacking libpcre3-dev:amd64 (2:8.39-12ubuntu0.1) ...
Selecting previously unselected package libsepol1-dev:amd64.
Preparing to unpack .../29-libsepol1-dev_3.0-1ubuntu0.1_amd64.deb ...
Unpacking libsepol1-dev:amd64 (3.0-1ubuntu0.1) ...
Selecting previously unselected package libpcre2-16-0:amd64.
Preparing to unpack .../30-libpcre2-16-0_10.34-7ubuntu0.1_amd64.deb ...
Unpacking libpcre2-16-0:amd64 (10.34-7ubuntu0.1) ...
Selecting previously unselected package libpcre2-posix2:amd64.
Preparing to unpack .../31-libpcre2-posix2_10.34-7ubuntu0.1_amd64.deb ...
Unpacking libpcre2-posix2:amd64 (10.34-7ubuntu0.1) ...
Selecting previously unselected package libpcre2-dev:amd64.
Preparing to unpack .../32-libpcre2-dev_10.34-7ubuntu0.1_amd64.deb ...
Unpacking libpcre2-dev:amd64 (10.34-7ubuntu0.1) ...
Selecting previously unselected package libselinux1-dev:amd64.
Preparing to unpack .../33-libselinux1-dev_3.0-1build2_amd64.deb ...
Unpacking libselinux1-dev:amd64 (3.0-1build2) ...
Selecting previously unselected package libglib2.0-dev:amd64.
Preparing to unpack .../34-libglib2.0-dev_2.64.6-1~ubuntu20.04.4_amd64.deb ...
Unpacking libglib2.0-dev:amd64 (2.64.6-1~ubuntu20.04.4) ...
Selecting previously unselected package libgl1-mesa-dev:amd64.
Preparing to unpack .../35-libgl1-mesa-dev_21.2.6-0ubuntu0.1~20.04.2_amd64.deb ...
Unpacking libgl1-mesa-dev:amd64 (21.2.6-0ubuntu0.1~20.04.2) ...
Selecting previously unselected package libglu1-mesa-dev:amd64.
Preparing to unpack .../36-libglu1-mesa-dev_9.0.1-1build1_amd64.deb ...
Unpacking libglu1-mesa-dev:amd64 (9.0.1-1build1) ...
Selecting previously unselected package libibus-1.0-dev:amd64.
Preparing to unpack .../37-libibus-1.0-dev_1.5.22-2ubuntu2.1_amd64.deb ...
Unpacking libibus-1.0-dev:amd64 (1.5.22-2ubuntu2.1) ...
Selecting previously unselected package libice-dev:amd64.
Preparing to unpack .../38-libice-dev_2%3a1.0.10-0ubuntu1_amd64.deb ...
Unpacking libice-dev:amd64 (2:1.0.10-0ubuntu1) ...
Selecting previously unselected package libpulse-dev:amd64.
Preparing to unpack .../39-libpulse-dev_1%3a13.99.1-1ubuntu3.13_amd64.deb ...
Unpacking libpulse-dev:amd64 (1:13.99.1-1ubuntu3.13) ...
Selecting previously unselected package libsdl2-2.0-0:amd64.
Preparing to unpack .../40-libsdl2-2.0-0_2.0.10+dfsg1-3_amd64.deb ...
Unpacking libsdl2-2.0-0:amd64 (2.0.10+dfsg1-3) ...
Selecting previously unselected package libsndio7.0:amd64.
Preparing to unpack .../41-libsndio7.0_1.5.0-3_amd64.deb ...
Unpacking libsndio7.0:amd64 (1.5.0-3) ...
Selecting previously unselected package libsndio-dev:amd64.
Preparing to unpack .../42-libsndio-dev_1.5.0-3_amd64.deb ...
Unpacking libsndio-dev:amd64 (1.5.0-3) ...
Selecting previously unselected package libudev-dev:amd64.
Preparing to unpack .../43-libudev-dev_245.4-4ubuntu3.21_amd64.deb ...
Unpacking libudev-dev:amd64 (245.4-4ubuntu3.21) ...
Selecting previously unselected package libwayland-bin.
Preparing to unpack .../44-libwayland-bin_1.18.0-1ubuntu0.1_amd64.deb ...
Unpacking libwayland-bin (1.18.0-1ubuntu0.1) ...
Selecting previously unselected package libwayland-dev:amd64.
Preparing to unpack .../45-libwayland-dev_1.18.0-1ubuntu0.1_amd64.deb ...
Unpacking libwayland-dev:amd64 (1.18.0-1ubuntu0.1) ...
Selecting previously unselected package libxrender-dev:amd64.
Preparing to unpack .../46-libxrender-dev_1%3a0.9.10-1_amd64.deb ...
Unpacking libxrender-dev:amd64 (1:0.9.10-1) ...
Selecting previously unselected package libxfixes-dev:amd64.
Preparing to unpack .../47-libxfixes-dev_1%3a5.0.3-2_amd64.deb ...
Unpacking libxfixes-dev:amd64 (1:5.0.3-2) ...
Selecting previously unselected package libxcursor-dev:amd64.
Preparing to unpack .../48-libxcursor-dev_1%3a1.2.0-2_amd64.deb ...
Unpacking libxcursor-dev:amd64 (1:1.2.0-2) ...
Selecting previously unselected package x11proto-xext-dev.
Preparing to unpack .../49-x11proto-xext-dev_2019.2-1ubuntu1_all.deb ...
Unpacking x11proto-xext-dev (2019.2-1ubuntu1) ...
Selecting previously unselected package libxext-dev:amd64.
Preparing to unpack .../50-libxext-dev_2%3a1.3.4-0ubuntu1_amd64.deb ...
Unpacking libxext-dev:amd64 (2:1.3.4-0ubuntu1) ...
Selecting previously unselected package x11proto-input-dev.
Preparing to unpack .../51-x11proto-input-dev_2019.2-1ubuntu1_all.deb ...
Unpacking x11proto-input-dev (2019.2-1ubuntu1) ...
Selecting previously unselected package libxi-dev:amd64.
Preparing to unpack .../52-libxi-dev_2%3a1.7.10-0ubuntu1_amd64.deb ...
Unpacking libxi-dev:amd64 (2:1.7.10-0ubuntu1) ...
Selecting previously unselected package x11proto-xinerama-dev.
Preparing to unpack .../53-x11proto-xinerama-dev_2019.2-1ubuntu1_all.deb ...
Unpacking x11proto-xinerama-dev (2019.2-1ubuntu1) ...
Selecting previously unselected package libxinerama-dev:amd64.
Preparing to unpack .../54-libxinerama-dev_2%3a1.1.4-2_amd64.deb ...
Unpacking libxinerama-dev:amd64 (2:1.1.4-2) ...
Selecting previously unselected package libxkbcommon-dev:amd64.
Preparing to unpack .../55-libxkbcommon-dev_0.10.0-1_amd64.deb ...
Unpacking libxkbcommon-dev:amd64 (0.10.0-1) ...
Selecting previously unselected package x11proto-randr-dev.
Preparing to unpack .../56-x11proto-randr-dev_2019.2-1ubuntu1_all.deb ...
Unpacking x11proto-randr-dev (2019.2-1ubuntu1) ...
Selecting previously unselected package libxrandr-dev:amd64.
Preparing to unpack .../57-libxrandr-dev_2%3a1.5.2-0ubuntu1_amd64.deb ...
Unpacking libxrandr-dev:amd64 (2:1.5.2-0ubuntu1) ...
Selecting previously unselected package x11proto-scrnsaver-dev.
Preparing to unpack .../58-x11proto-scrnsaver-dev_2019.2-1ubuntu1_all.deb ...
Unpacking x11proto-scrnsaver-dev (2019.2-1ubuntu1) ...
Selecting previously unselected package libxss-dev:amd64.
Preparing to unpack .../59-libxss-dev_1%3a1.2.3-1_amd64.deb ...
Unpacking libxss-dev:amd64 (1:1.2.3-1) ...
Selecting previously unselected package libsm-dev:amd64.
Preparing to unpack .../60-libsm-dev_2%3a1.2.3-1_amd64.deb ...
Unpacking libsm-dev:amd64 (2:1.2.3-1) ...
Selecting previously unselected package libxt-dev:amd64.
Preparing to unpack .../61-libxt-dev_1%3a1.1.5-1_amd64.deb ...
Unpacking libxt-dev:amd64 (1:1.1.5-1) ...
Selecting previously unselected package libxv-dev:amd64.
Preparing to unpack .../62-libxv-dev_2%3a1.0.11-1_amd64.deb ...
Unpacking libxv-dev:amd64 (2:1.0.11-1) ...
Selecting previously unselected package x11proto-xf86vidmode-dev.
Preparing to unpack .../63-x11proto-xf86vidmode-dev_2019.2-1ubuntu1_all.deb ...
Unpacking x11proto-xf86vidmode-dev (2019.2-1ubuntu1) ...
Selecting previously unselected package libxxf86vm-dev:amd64.
Preparing to unpack .../64-libxxf86vm-dev_1%3a1.1.4-1build1_amd64.deb ...
Unpacking libxxf86vm-dev:amd64 (1:1.1.4-1build1) ...
Selecting previously unselected package libsdl2-dev:amd64.
Preparing to unpack .../65-libsdl2-dev_2.0.10+dfsg1-3_amd64.deb ...
Unpacking libsdl2-dev:amd64 (2.0.10+dfsg1-3) ...
Setting up libpcrecpp0v5:amd64 (2:8.39-12ubuntu0.1) ...
Setting up libglib2.0-dev-bin (2.64.6-1~ubuntu20.04.4) ...
Setting up libpcre16-3:amd64 (2:8.39-12ubuntu0.1) ...
Setting up libxkbcommon-dev:amd64 (0.10.0-1) ...
Setting up libsepol1-dev:amd64 (3.0-1ubuntu0.1) ...
Setting up libffi-dev:amd64 (3.3-4) ...
Setting up libpthread-stubs0-dev:amd64 (0.4-1) ...
Setting up libpcre2-16-0:amd64 (10.34-7ubuntu0.1) ...
Setting up xtrans-dev (1.4.0-1) ...
Setting up libwayland-bin (1.18.0-1ubuntu0.1) ...
Setting up libdbus-1-dev:amd64 (1.12.16-2ubuntu2.3) ...
Setting up uuid-dev:amd64 (2.34-0.1ubuntu9.3) ...
Setting up libgles1:amd64 (1.3.2-1~ubuntu0.20.04.2) ...
Setting up libpcre32-3:amd64 (2:8.39-12ubuntu0.1) ...
Setting up libudev-dev:amd64 (245.4-4ubuntu3.21) ...
Setting up libpcre2-posix2:amd64 (10.34-7ubuntu0.1) ...
Setting up libsndio7.0:amd64 (1.5.0-3) ...
Setting up xorg-sgml-doctools (1:1.11-1) ...
Setting up libopengl-dev:amd64 (1.3.2-1~ubuntu0.20.04.2) ...
Setting up libasound2-dev:amd64 (1.2.2-2.1ubuntu2.5) ...
Setting up libsdl2-2.0-0:amd64 (2.0.10+dfsg1-3) ...
Setting up libblkid-dev:amd64 (2.34-0.1ubuntu9.3) ...
Setting up libsndio-dev:amd64 (1.5.0-3) ...
Setting up libpcre2-dev:amd64 (10.34-7ubuntu0.1) ...
Setting up libselinux1-dev:amd64 (3.0-1build2) ...
Setting up libpcre3-dev:amd64 (2:8.39-12ubuntu0.1) ...
Setting up libwayland-dev:amd64 (1.18.0-1ubuntu0.1) ...
Setting up libmount-dev:amd64 (2.34-0.1ubuntu9.3) ...
Setting up libglib2.0-dev:amd64 (2.64.6-1~ubuntu20.04.4) ...
Processing triggers for sgml-base (1.29.1) ...
Processing triggers for install-info (6.7.0.dfsg.2-5) ...
Setting up x11proto-dev (2019.2-1ubuntu1) ...
Setting up libxau-dev:amd64 (1:1.0.9-0ubuntu1) ...
Setting up libice-dev:amd64 (2:1.0.10-0ubuntu1) ...
Setting up libsm-dev:amd64 (2:1.2.3-1) ...
Processing triggers for libglib2.0-0:amd64 (2.64.6-1~ubuntu20.04.4) ...
Setting up x11proto-randr-dev (2019.2-1ubuntu1) ...
Processing triggers for libc-bin (2.31-0ubuntu9.9) ...
Processing triggers for man-db (2.9.1-1) ...
Setting up x11proto-xinerama-dev (2019.2-1ubuntu1) ...
Setting up libibus-1.0-dev:amd64 (1.5.22-2ubuntu2.1) ...
Setting up libxdmcp-dev:amd64 (1:1.1.3-0ubuntu1) ...
Setting up x11proto-core-dev (2019.2-1ubuntu1) ...
Setting up x11proto-input-dev (2019.2-1ubuntu1) ...
Setting up libpulse-dev:amd64 (1:13.99.1-1ubuntu3.13) ...
Setting up x11proto-xf86vidmode-dev (2019.2-1ubuntu1) ...
Setting up x11proto-xext-dev (2019.2-1ubuntu1) ...
Setting up x11proto-scrnsaver-dev (2019.2-1ubuntu1) ...
Setting up libxcb1-dev:amd64 (1.14-2) ...
Setting up libx11-dev:amd64 (2:1.6.9-2ubuntu1.2) ...
Setting up libxfixes-dev:amd64 (1:5.0.3-2) ...
Setting up libxt-dev:amd64 (1:1.1.5-1) ...
Setting up libxext-dev:amd64 (2:1.3.4-0ubuntu1) ...
Setting up libglx-dev:amd64 (1.3.2-1~ubuntu0.20.04.2) ...
Setting up libxi-dev:amd64 (2:1.7.10-0ubuntu1) ...
Setting up libxrender-dev:amd64 (1:0.9.10-1) ...
Setting up libgl-dev:amd64 (1.3.2-1~ubuntu0.20.04.2) ...
Setting up libegl-dev:amd64 (1.3.2-1~ubuntu0.20.04.2) ...
Setting up libxcursor-dev:amd64 (1:1.2.0-2) ...
Setting up libxxf86vm-dev:amd64 (1:1.1.4-1build1) ...
Setting up libxss-dev:amd64 (1:1.2.3-1) ...
Setting up libxv-dev:amd64 (2:1.0.11-1) ...
Setting up libxrandr-dev:amd64 (2:1.5.2-0ubuntu1) ...
Setting up libglu1-mesa-dev:amd64 (9.0.1-1build1) ...
Setting up libxinerama-dev:amd64 (2:1.1.4-2) ...
Setting up libgles-dev:amd64 (1.3.2-1~ubuntu0.20.04.2) ...
Setting up libglvnd-dev:amd64 (1.3.2-1~ubuntu0.20.04.2) ...
Setting up libgl1-mesa-dev:amd64 (21.2.6-0ubuntu0.1~20.04.2) ...
Setting up libegl1-mesa-dev:amd64 (21.2.6-0ubuntu0.1~20.04.2) ...
Setting up libgles2-mesa-dev:amd64 (21.2.6-0ubuntu0.1~20.04.2) ...
Setting up libsdl2-dev:amd64 (2.0.10+dfsg1-3) ...
kevin@kevin:~$ sudo apt install libevent-dev libjson-c-dev -y
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
  libevent-core-2.1-7 libevent-extra-2.1-7 libevent-openssl-2.1-7 libevent-pthreads-2.1-7
The following NEW packages will be installed:
  libevent-core-2.1-7 libevent-dev libevent-extra-2.1-7 libevent-openssl-2.1-7 libevent-pthreads-2.1-7 libjson-c-dev
0 upgraded, 6 newly installed, 0 to remove and 93 not upgraded.
Need to get 479 kB of archives.
After this operation, 2563 kB of additional disk space will be used.
Get:1 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libevent-core-2.1-7 amd64 2.1.11-stable-1 [89.1 kB]
Get:2 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libevent-extra-2.1-7 amd64 2.1.11-stable-1 [60.0 kB]
Get:3 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libevent-pthreads-2.1-7 amd64 2.1.11-stable-1 [7372 B]
Get:4 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libevent-openssl-2.1-7 amd64 2.1.11-stable-1 [14.3 kB]
Get:5 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libevent-dev amd64 2.1.11-stable-1 [261 kB]
Get:6 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 libjson-c-dev amd64 0.13.1+dfsg-7ubuntu0.3 [46.9 kB]
Fetched 479 kB in 0s (3090 kB/s)
Selecting previously unselected package libevent-core-2.1-7:amd64.
(Reading database ... 191997 files and directories currently installed.)
Preparing to unpack .../0-libevent-core-2.1-7_2.1.11-stable-1_amd64.deb ...
Unpacking libevent-core-2.1-7:amd64 (2.1.11-stable-1) ...
Selecting previously unselected package libevent-extra-2.1-7:amd64.
Preparing to unpack .../1-libevent-extra-2.1-7_2.1.11-stable-1_amd64.deb ...
Unpacking libevent-extra-2.1-7:amd64 (2.1.11-stable-1) ...
Selecting previously unselected package libevent-pthreads-2.1-7:amd64.
Preparing to unpack .../2-libevent-pthreads-2.1-7_2.1.11-stable-1_amd64.deb ...
Unpacking libevent-pthreads-2.1-7:amd64 (2.1.11-stable-1) ...
Selecting previously unselected package libevent-openssl-2.1-7:amd64.
Preparing to unpack .../3-libevent-openssl-2.1-7_2.1.11-stable-1_amd64.deb ...
Unpacking libevent-openssl-2.1-7:amd64 (2.1.11-stable-1) ...
Selecting previously unselected package libevent-dev.
Preparing to unpack .../4-libevent-dev_2.1.11-stable-1_amd64.deb ...
Unpacking libevent-dev (2.1.11-stable-1) ...
Selecting previously unselected package libjson-c-dev:amd64.
Preparing to unpack .../5-libjson-c-dev_0.13.1+dfsg-7ubuntu0.3_amd64.deb ...
Unpacking libjson-c-dev:amd64 (0.13.1+dfsg-7ubuntu0.3) ...
Setting up libjson-c-dev:amd64 (0.13.1+dfsg-7ubuntu0.3) ...
Setting up libevent-core-2.1-7:amd64 (2.1.11-stable-1) ...
Setting up libevent-pthreads-2.1-7:amd64 (2.1.11-stable-1) ...
Setting up libevent-extra-2.1-7:amd64 (2.1.11-stable-1) ...
Setting up libevent-openssl-2.1-7:amd64 (2.1.11-stable-1) ...
Setting up libevent-dev (2.1.11-stable-1) ...
Processing triggers for libc-bin (2.31-0ubuntu9.9) ...
```

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
```console
kevin@kevin:~$ sudo apt install autoconf flex bison help2man -y
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
  automake autotools-dev libfl-dev libfl2 libsigsegv2 m4
Suggested packages:
  autoconf-archive gnu-standards autoconf-doc libtool gettext bison-doc flex-doc m4-doc
The following NEW packages will be installed:
  autoconf automake autotools-dev bison flex help2man libfl-dev libfl2 libsigsegv2 m4
0 upgraded, 10 newly installed, 0 to remove and 93 not upgraded.
Need to get 2260 kB of archives.
After this operation, 7714 kB of additional disk space will be used.
Get:1 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libsigsegv2 amd64 2.12-2 [13.9 kB]
Get:2 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 m4 amd64 1.4.18-4 [199 kB]
Get:3 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 flex amd64 2.6.4-6.2 [317 kB]
Get:4 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 autoconf all 2.69-11.1 [321 kB]
Get:5 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 autotools-dev all 20180224.1 [39.6 kB]
Get:6 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 automake all 1:1.16.1-4ubuntu6 [522 kB]
Get:7 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 bison amd64 2:3.5.1+dfsg-1 [657 kB]
Get:8 http://tw.archive.ubuntu.com/ubuntu focal/universe amd64 help2man amd64 1.47.13 [173 kB]
Get:9 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libfl2 amd64 2.6.4-6.2 [11.5 kB]
Get:10 http://tw.archive.ubuntu.com/ubuntu focal/main amd64 libfl-dev amd64 2.6.4-6.2 [6316 B]
Fetched 2260 kB in 0s (7885 kB/s)
Selecting previously unselected package libsigsegv2:amd64.
(Reading database ... 192106 files and directories currently installed.)
Preparing to unpack .../0-libsigsegv2_2.12-2_amd64.deb ...
Unpacking libsigsegv2:amd64 (2.12-2) ...
Selecting previously unselected package m4.
Preparing to unpack .../1-m4_1.4.18-4_amd64.deb ...
Unpacking m4 (1.4.18-4) ...
Selecting previously unselected package flex.
Preparing to unpack .../2-flex_2.6.4-6.2_amd64.deb ...
Unpacking flex (2.6.4-6.2) ...
Selecting previously unselected package autoconf.
Preparing to unpack .../3-autoconf_2.69-11.1_all.deb ...
Unpacking autoconf (2.69-11.1) ...
Selecting previously unselected package autotools-dev.
Preparing to unpack .../4-autotools-dev_20180224.1_all.deb ...
Unpacking autotools-dev (20180224.1) ...
Selecting previously unselected package automake.
Preparing to unpack .../5-automake_1%3a1.16.1-4ubuntu6_all.deb ...
Unpacking automake (1:1.16.1-4ubuntu6) ...
Selecting previously unselected package bison.
Preparing to unpack .../6-bison_2%3a3.5.1+dfsg-1_amd64.deb ...
Unpacking bison (2:3.5.1+dfsg-1) ...
Selecting previously unselected package help2man.
Preparing to unpack .../7-help2man_1.47.13_amd64.deb ...
Unpacking help2man (1.47.13) ...
Selecting previously unselected package libfl2:amd64.
Preparing to unpack .../8-libfl2_2.6.4-6.2_amd64.deb ...
Unpacking libfl2:amd64 (2.6.4-6.2) ...
Selecting previously unselected package libfl-dev:amd64.
Preparing to unpack .../9-libfl-dev_2.6.4-6.2_amd64.deb ...
Unpacking libfl-dev:amd64 (2.6.4-6.2) ...
Setting up help2man (1.47.13) ...
Setting up autotools-dev (20180224.1) ...
Setting up libsigsegv2:amd64 (2.12-2) ...
Setting up libfl2:amd64 (2.6.4-6.2) ...
Setting up m4 (1.4.18-4) ...
Setting up autoconf (2.69-11.1) ...
Setting up bison (2:3.5.1+dfsg-1) ...
update-alternatives: using /usr/bin/bison.yacc to provide /usr/bin/yacc (yacc) in auto mode
Setting up automake (1:1.16.1-4ubuntu6) ...
update-alternatives: using /usr/bin/automake-1.16 to provide /usr/bin/automake (automake) in auto mode
Setting up flex (2.6.4-6.2) ...
Setting up libfl-dev:amd64 (2.6.4-6.2) ...
Processing triggers for libc-bin (2.31-0ubuntu9.9) ...
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for install-info (6.7.0.dfsg.2-5) ...
kevin@kevin:~$ git clone https://github.com/verilator/verilator
Cloning into 'verilator'...
remote: Enumerating objects: 73132, done.
remote: Counting objects: 100% (856/856), done.
remote: Compressing objects: 100% (383/383), done.
remote: Total 73132 (delta 532), reused 739 (delta 473), pack-reused 72276
Receiving objects: 100% (73132/73132), 35.89 MiB | 15.74 MiB/s, done.
Resolving deltas: 100% (62560/62560), done.
kevin@kevin:~$ cd verilator/
kevin@kevin:~/verilator$ git pull
Already up to date.
kevin@kevin:~/verilator$ autoconf
kevin@kevin:~/verilator$ export VERILATOR_ROOT=`pwd`
kevin@kevin:~/verilator$ ./configure
configuring for Verilator 5.009 devel
checking whether to perform partial static linking of Verilator binary... yes
checking whether to use tcmalloc... check
checking whether to use -m32... no
checking whether to build for coverage collection... no
checking whether to use hardcoded paths... yes
checking whether to show and stop on compilation warnings... no
checking whether to run long tests... no
checking for gcc... gcc
checking whether the C compiler works... yes
checking for C compiler default output file name... a.out
checking for suffix of executables...
checking whether we are cross compiling... no
checking for suffix of object files... o
checking whether we are using the GNU C compiler... yes
checking whether gcc accepts -g... yes
checking for gcc option to accept ISO C89... none needed
checking for g++... g++
checking whether we are using the GNU C++ compiler... yes
checking whether g++ accepts -g... yes
checking for a BSD-compatible install... /usr/bin/install -c
compiler is g++ --version = g++ (Ubuntu 9.4.0-1ubuntu1~20.04.1) 9.4.0
checking that C++ compiler can compile simple program... yes
checking for ar... ar
checking for perl... /usr/bin/perl
checking for python3... /usr/bin/python3
checking for flex... /usr/bin/flex
/usr/bin/flex --version = flex 2.6.4
checking for bison... /usr/bin/bison
/usr/bin/bison --version = bison (GNU Bison) 3.5.1
checking for ccache... no
checking how to run the C++ preprocessor... g++ -E
checking for grep that handles long lines and -e... /usr/bin/grep
checking for egrep... /usr/bin/grep -E
checking for ANSI C header files... yes
checking for sys/types.h... yes
checking for sys/stat.h... yes
checking for stdlib.h... yes
checking for string.h... yes
checking for memory.h... yes
checking for strings.h... yes
checking for inttypes.h... yes
checking for stdint.h... yes
checking for unistd.h... yes
checking for size_t... yes
checking for size_t... (cached) yes
checking for inline... inline
checking whether g++ accepts -pg... yes
checking whether g++ accepts -std=gnu++17... yes
checking whether g++ accepts -Wextra... yes
checking whether g++ accepts -Wfloat-conversion... yes
checking whether g++ accepts -Wlogical-op... yes
checking whether g++ accepts -Wthread-safety... no
checking whether g++ accepts -fcoroutines-ts... no
checking whether coroutines are supported by g++... no
checking whether g++ accepts -Qunused-arguments... no
checking whether g++ accepts -faligned-new... yes
checking whether g++ accepts -Wno-unused-parameter... yes
checking whether g++ accepts -Wno-shadow... yes
checking whether g++ accepts -Wno-char-subscripts... yes
checking whether g++ accepts -Wno-null-conversion... no
checking whether g++ accepts -Wno-parentheses-equality... no
checking whether g++ accepts -Wno-unused... yes
checking whether g++ accepts -Og... yes
checking whether g++ accepts -ggdb... yes
checking whether g++ accepts -gz... yes
checking whether g++ linker accepts -gz... yes
checking whether g++ accepts -faligned-new... yes
checking whether g++ accepts -fbracket-depth=4096... no
checking whether g++ accepts -fcf-protection=none... yes
checking whether g++ accepts -mno-cet... no
checking whether g++ accepts -Qunused-arguments... no
checking whether g++ accepts -Wno-bool-operation... yes
checking whether g++ accepts -Wno-tautological-bitwise-compare... no
checking whether g++ accepts -Wno-parentheses-equality... no
checking whether g++ accepts -Wno-sign-compare... yes
checking whether g++ accepts -Wno-uninitialized... yes
checking whether g++ accepts -Wno-unused-but-set-variable... yes
checking whether g++ accepts -Wno-unused-parameter... yes
checking whether g++ accepts -Wno-unused-variable... yes
checking whether g++ accepts -Wno-shadow... yes
checking whether g++ linker accepts -mt... no
checking whether g++ linker accepts -pthread... yes
checking whether g++ linker accepts -lpthread... yes
checking whether g++ linker accepts -latomic... yes
checking whether g++ linker accepts -static-libgcc... yes
checking whether g++ linker accepts -static-libstdc++... yes
checking whether g++ linker accepts -Xlinker -gc-sections... yes
checking whether g++ linker accepts -lpthread... yes
checking whether g++ linker accepts -lbcrypt... no
checking whether g++ linker accepts -lpsapi... no
checking whether g++ linker accepts -l:libtcmalloc_minimal.a... no
checking whether g++ supports C++11... yes
checking for struct stat.st_mtim.tv_nsec... yes
checking whether SystemC is found (in system path)... no
configure: creating ./config.status
config.status: creating Makefile
config.status: creating src/Makefile
config.status: creating src/Makefile_obj
config.status: creating include/verilated.mk
config.status: creating include/verilated_config.h
config.status: creating verilator.pc
config.status: creating verilator-config.cmake
config.status: creating verilator-config-version.cmake
config.status: creating src/config_build.h

Now type 'make' (or sometimes 'gmake') to build Verilator.

kevin@kevin:~/verilator$ make -j `nproc`
pod2man bin/verilator verilator.1
------------------------------------------------------------
pod2man bin/verilator_coverage verilator_coverage.1
help2man --no-info --no-discard-stderr --version-string=- bin/verilator_gantt -o verilator_gantt.1
help2man --no-info --no-discard-stderr --version-string=- bin/verilator_profcfunc -o verilator_profcfunc.1
making verilator in src
make -C src
make[1]: Entering directory '/home/kevin/verilator/src'
mkdir -p obj_dbg
/usr/bin/python3 ./config_rev . >config_rev.h
mkdir -p obj_opt
make -C obj_dbg -j 1  TGT=../../bin/verilator_bin_dbg VL_DEBUG=1 -f ../Makefile_obj serial
make -C obj_dbg       TGT=../../bin/verilator_coverage_bin_dbg VL_DEBUG=1 VL_VLCOV=1 -f ../Makefile_obj serial_vlcov
make -C obj_opt -j 1  TGT=../../bin/verilator_bin -f ../Makefile_obj serial
make[2]: Entering directory '/home/kevin/verilator/src'
make[2]: warning: -j1 forced in submake: resetting jobserver mode.
make[2]: Entering directory '/home/kevin/verilator/src'
make[2]: warning: -j1 forced in submake: resetting jobserver mode.
/usr/bin/python3 ../astgen -I .. --astdef V3AstNodeDType.h --astdef V3AstNodeExpr.h --astdef V3AstNodeOther.h --dfgdef V3DfgVertices.h --classes
make[2]: Entering directory '/home/kevin/verilator/src/obj_dbg'
/usr/bin/python3 ../vlcovgen --srcdir ..
/usr/bin/python3 ../astgen -I .. --astdef V3AstNodeDType.h --astdef V3AstNodeExpr.h --astdef V3AstNodeOther.h --dfgdef V3DfgVertices.h --classes
touch vlcovgen.d
make[2]: Leaving directory '/home/kevin/verilator/src/obj_dbg'
make -C obj_dbg       TGT=../../bin/verilator_coverage_bin_dbg VL_DEBUG=1 VL_VLCOV=1 -f ../Makefile_obj
make[2]: Entering directory '/home/kevin/verilator/src/obj_dbg'
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../VlcMain.cpp -o VlcMain.o
      Compile flags:  g++ -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC="" -DDEFENV_SYSTEMC_ARCH="" -DDEFENV_SYSTEMC_INCLUDE="" -DDEFENV_SYSTEMC_LIBDIR="" -DDEFENV_VERILATOR_ROOT="/home/kevin/verilator"
If you get errors from verilog.y below, try upgrading bison to version 1.875 or newer.
/usr/bin/python3 ../bisonpre --yacc /usr/bin/bison -d -v -o V3ParseBison.c ../verilog.y
  edit ../verilog.y V3ParseBison_pretmp.y
If you get errors from verilog.y below, try upgrading bison to version 1.875 or newer.
/usr/bin/python3 ../bisonpre --yacc /usr/bin/bison -d -v -o V3ParseBison.c ../verilog.y
  edit ../verilog.y V3ParseBison_pretmp.y
  /usr/bin/bison -d -v --report=itemset --report=lookahead -b V3ParseBison_pretmp -o V3ParseBison_pretmp.c V3ParseBison_pretmp.y
  /usr/bin/bison -d -v --report=itemset --report=lookahead -b V3ParseBison_pretmp -o V3ParseBison_pretmp.c V3ParseBison_pretmp.y
  edit V3ParseBison_pretmp.output V3ParseBison.output
  edit V3ParseBison_pretmp.output V3ParseBison.output
      Linking ../../bin/verilator_coverage_bin_dbg...
g++  -gz -static-libgcc -static-libstdc++ -Xlinker -gc-sections -o ../../bin/verilator_coverage_bin_dbg VlcMain.o   -lpthread -lm
make[2]: Leaving directory '/home/kevin/verilator/src/obj_dbg'
  edit V3ParseBison_pretmp.c V3ParseBison.c
  edit V3ParseBison_pretmp.c V3ParseBison.c
  edit V3ParseBison_pretmp.h V3ParseBison.h
make[2]: Leaving directory '/home/kevin/verilator/src/obj_dbg'
make -C obj_dbg       TGT=../../bin/verilator_bin_dbg VL_DEBUG=1 -f ../Makefile_obj
make[2]: Entering directory '/home/kevin/verilator/src/obj_dbg'
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../Verilator.cpp -o Verilator.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Active.cpp -o V3Active.o
      Compile flags:  g++ -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC="" -DDEFENV_SYSTEMC_ARCH="" -DDEFENV_SYSTEMC_INCLUDE="" -DDEFENV_SYSTEMC_LIBDIR="" -DDEFENV_VERILATOR_ROOT="/home/kevin/verilator"
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3ActiveTop.cpp -o V3ActiveTop.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Assert.cpp -o V3Assert.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3AssertPre.cpp -o V3AssertPre.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Ast.cpp -o V3Ast.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3AstNodes.cpp -o V3AstNodes.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Begin.cpp -o V3Begin.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Branch.cpp -o V3Branch.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Broken.cpp -o V3Broken.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3CCtors.cpp -o V3CCtors.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3CUse.cpp -o V3CUse.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Case.cpp -o V3Case.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Cast.cpp -o V3Cast.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Class.cpp -o V3Class.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Clean.cpp -o V3Clean.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Clock.cpp -o V3Clock.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Combine.cpp -o V3Combine.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Common.cpp -o V3Common.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Config.cpp -o V3Config.o
/usr/bin/python3 ../astgen -I .. --astdef V3AstNodeDType.h --astdef V3AstNodeExpr.h --astdef V3AstNodeOther.h --dfgdef V3DfgVertices.h V3Const.cpp
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Coverage.cpp -o V3Coverage.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3CoverageJoin.cpp -o V3CoverageJoin.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Dead.cpp -o V3Dead.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Delayed.cpp -o V3Delayed.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Depth.cpp -o V3Depth.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3DepthBlock.cpp -o V3DepthBlock.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Descope.cpp -o V3Descope.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Dfg.cpp -o V3Dfg.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3DfgAstToDfg.cpp -o V3DfgAstToDfg.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3DfgDecomposition.cpp -o V3DfgDecomposition.o
  edit V3ParseBison_pretmp.h V3ParseBison.h
make[2]: Leaving directory '/home/kevin/verilator/src/obj_opt'
make -C obj_opt       TGT=../../bin/verilator_bin -f ../Makefile_obj
make[2]: Entering directory '/home/kevin/verilator/src/obj_opt'
      Compile flags:  g++ -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC="" -DDEFENV_SYSTEMC_ARCH="" -DDEFENV_SYSTEMC_INCLUDE="" -DDEFENV_SYSTEMC_LIBDIR="" -DDEFENV_VERILATOR_ROOT="/home/kevin/verilator"
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../Verilator.cpp -o Verilator.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Active.cpp -o V3Active.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3ActiveTop.cpp -o V3ActiveTop.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3DfgDfgToAst.cpp -o V3DfgDfgToAst.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3DfgOptimizer.cpp -o V3DfgOptimizer.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Assert.cpp -o V3Assert.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3DfgPasses.cpp -o V3DfgPasses.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3DfgPeephole.cpp -o V3DfgPeephole.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3DupFinder.cpp -o V3DupFinder.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3AssertPre.cpp -o V3AssertPre.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Ast.cpp -o V3Ast.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3AstNodes.cpp -o V3AstNodes.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Begin.cpp -o V3Begin.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Branch.cpp -o V3Branch.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Broken.cpp -o V3Broken.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3CCtors.cpp -o V3CCtors.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3EmitCBase.cpp -o V3EmitCBase.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3EmitCConstPool.cpp -o V3EmitCConstPool.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3CUse.cpp -o V3CUse.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Case.cpp -o V3Case.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3EmitCFunc.cpp -o V3EmitCFunc.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3EmitCHeaders.cpp -o V3EmitCHeaders.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Cast.cpp -o V3Cast.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3EmitCImp.cpp -o V3EmitCImp.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Class.cpp -o V3Class.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Clean.cpp -o V3Clean.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Clock.cpp -o V3Clock.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Combine.cpp -o V3Combine.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Common.cpp -o V3Common.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3EmitCInlines.cpp -o V3EmitCInlines.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3EmitCMain.cpp -o V3EmitCMain.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Config.cpp -o V3Config.o
/usr/bin/python3 ../astgen -I .. --astdef V3AstNodeDType.h --astdef V3AstNodeExpr.h --astdef V3AstNodeOther.h --dfgdef V3DfgVertices.h V3Const.cpp
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3EmitCMake.cpp -o V3EmitCMake.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Coverage.cpp -o V3Coverage.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3CoverageJoin.cpp -o V3CoverageJoin.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Dead.cpp -o V3Dead.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Delayed.cpp -o V3Delayed.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Depth.cpp -o V3Depth.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3DepthBlock.cpp -o V3DepthBlock.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Descope.cpp -o V3Descope.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Dfg.cpp -o V3Dfg.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3DfgAstToDfg.cpp -o V3DfgAstToDfg.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3DfgDecomposition.cpp -o V3DfgDecomposition.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3DfgDfgToAst.cpp -o V3DfgDfgToAst.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3EmitCModel.cpp -o V3EmitCModel.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3DfgOptimizer.cpp -o V3DfgOptimizer.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3EmitCSyms.cpp -o V3EmitCSyms.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3EmitMk.cpp -o V3EmitMk.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3EmitV.cpp -o V3EmitV.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3EmitXml.cpp -o V3EmitXml.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3DfgPasses.cpp -o V3DfgPasses.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3DfgPeephole.cpp -o V3DfgPeephole.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3DupFinder.cpp -o V3DupFinder.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Error.cpp -o V3Error.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3EmitCBase.cpp -o V3EmitCBase.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3EmitCConstPool.cpp -o V3EmitCConstPool.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3EmitCFunc.cpp -o V3EmitCFunc.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3EmitCHeaders.cpp -o V3EmitCHeaders.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3EmitCImp.cpp -o V3EmitCImp.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3EmitCInlines.cpp -o V3EmitCInlines.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3EmitCMain.cpp -o V3EmitCMain.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3EmitCMake.cpp -o V3EmitCMake.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3EmitCModel.cpp -o V3EmitCModel.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3EmitCSyms.cpp -o V3EmitCSyms.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3EmitMk.cpp -o V3EmitMk.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Expand.cpp -o V3Expand.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3EmitV.cpp -o V3EmitV.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3EmitXml.cpp -o V3EmitXml.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Error.cpp -o V3Error.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Expand.cpp -o V3Expand.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3File.cpp -o V3File.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3File.cpp -o V3File.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3FileLine.cpp -o V3FileLine.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Force.cpp -o V3Force.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Gate.cpp -o V3Gate.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3FileLine.cpp -o V3FileLine.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Force.cpp -o V3Force.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Gate.cpp -o V3Gate.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Global.cpp -o V3Global.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Global.cpp -o V3Global.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Graph.cpp -o V3Graph.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3GraphAcyc.cpp -o V3GraphAcyc.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Graph.cpp -o V3Graph.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3GraphAlg.cpp -o V3GraphAlg.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3GraphPathChecker.cpp -o V3GraphPathChecker.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3GraphAcyc.cpp -o V3GraphAcyc.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3GraphTest.cpp -o V3GraphTest.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Hash.cpp -o V3Hash.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Hasher.cpp -o V3Hasher.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3HierBlock.cpp -o V3HierBlock.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Inline.cpp -o V3Inline.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Inst.cpp -o V3Inst.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3InstrCount.cpp -o V3InstrCount.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Life.cpp -o V3Life.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3LifePost.cpp -o V3LifePost.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3LinkCells.cpp -o V3LinkCells.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3LinkDot.cpp -o V3LinkDot.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3LinkInc.cpp -o V3LinkInc.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3LinkJump.cpp -o V3LinkJump.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3LinkLValue.cpp -o V3LinkLValue.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3LinkLevel.cpp -o V3LinkLevel.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3LinkParse.cpp -o V3LinkParse.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3GraphAlg.cpp -o V3GraphAlg.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3GraphPathChecker.cpp -o V3GraphPathChecker.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3LinkResolve.cpp -o V3LinkResolve.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Localize.cpp -o V3Localize.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3MergeCond.cpp -o V3MergeCond.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Name.cpp -o V3Name.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3GraphTest.cpp -o V3GraphTest.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Hash.cpp -o V3Hash.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Number.cpp -o V3Number.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Hasher.cpp -o V3Hasher.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3HierBlock.cpp -o V3HierBlock.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3OptionParser.cpp -o V3OptionParser.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Options.cpp -o V3Options.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Inline.cpp -o V3Inline.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Order.cpp -o V3Order.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Os.cpp -o V3Os.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Param.cpp -o V3Param.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -Wno-char-subscripts -Wno-unused -c ../V3ParseGrammar.cpp -o V3ParseGrammar.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Inst.cpp -o V3Inst.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -Wno-char-subscripts -Wno-unused -c ../V3ParseImp.cpp -o V3ParseImp.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3InstrCount.cpp -o V3InstrCount.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Life.cpp -o V3Life.o
/usr/bin/flex --version
flex 2.6.4
/usr/bin/flex -d -oV3Lexer_pregen.yy.cpp ../verilog.l
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Partition.cpp -o V3Partition.o
/usr/bin/flex --version
flex 2.6.4
/usr/bin/flex -d -oV3PreLex_pregen.yy.cpp ../V3PreLex.l
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3PreShell.cpp -o V3PreShell.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Premit.cpp -o V3Premit.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3ProtectLib.cpp -o V3ProtectLib.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3LifePost.cpp -o V3LifePost.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Randomize.cpp -o V3Randomize.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Reloop.cpp -o V3Reloop.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Sched.cpp -o V3Sched.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3SchedAcyclic.cpp -o V3SchedAcyclic.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3SchedPartition.cpp -o V3SchedPartition.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3SchedReplicate.cpp -o V3SchedReplicate.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3SchedTiming.cpp -o V3SchedTiming.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3LinkCells.cpp -o V3LinkCells.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3LinkDot.cpp -o V3LinkDot.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3LinkInc.cpp -o V3LinkInc.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Scope.cpp -o V3Scope.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Scoreboard.cpp -o V3Scoreboard.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Slice.cpp -o V3Slice.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Split.cpp -o V3Split.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3LinkJump.cpp -o V3LinkJump.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3SplitAs.cpp -o V3SplitAs.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3SplitVar.cpp -o V3SplitVar.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Stats.cpp -o V3Stats.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3StatsReport.cpp -o V3StatsReport.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3LinkLValue.cpp -o V3LinkLValue.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3String.cpp -o V3String.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3LinkLevel.cpp -o V3LinkLevel.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Subst.cpp -o V3Subst.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3LinkParse.cpp -o V3LinkParse.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3TSP.cpp -o V3TSP.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Table.cpp -o V3Table.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3LinkResolve.cpp -o V3LinkResolve.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Task.cpp -o V3Task.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3ThreadPool.cpp -o V3ThreadPool.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Timing.cpp -o V3Timing.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Trace.cpp -o V3Trace.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3TraceDecl.cpp -o V3TraceDecl.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Tristate.cpp -o V3Tristate.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Undriven.cpp -o V3Undriven.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Localize.cpp -o V3Localize.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Unknown.cpp -o V3Unknown.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Unroll.cpp -o V3Unroll.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3VariableOrder.cpp -o V3VariableOrder.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Waiver.cpp -o V3Waiver.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3MergeCond.cpp -o V3MergeCond.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Width.cpp -o V3Width.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3WidthSel.cpp -o V3WidthSel.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c V3Const__gen.cpp -o V3Const__gen.o
/usr/bin/python3 ../flexfix V3Lexer <V3Lexer_pregen.yy.cpp >V3Lexer.yy.cpp
/usr/bin/python3 ../flexfix V3PreLex <V3PreLex_pregen.yy.cpp >V3PreLex.yy.cpp
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -Wno-char-subscripts -Wno-unused -c ../V3ParseLex.cpp -o V3ParseLex.o
g++   -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -Wno-char-subscripts -Wno-unused -c ../V3PreProc.cpp -o V3PreProc.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Name.cpp -o V3Name.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Number.cpp -o V3Number.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3OptionParser.cpp -o V3OptionParser.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Options.cpp -o V3Options.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Order.cpp -o V3Order.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Os.cpp -o V3Os.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Param.cpp -o V3Param.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -Wno-char-subscripts -Wno-unused -c ../V3ParseGrammar.cpp -o V3ParseGrammar.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -Wno-char-subscripts -Wno-unused -c ../V3ParseImp.cpp -o V3ParseImp.o
/usr/bin/flex --version
flex 2.6.4
/usr/bin/flex -d -oV3Lexer_pregen.yy.cpp ../verilog.l
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Partition.cpp -o V3Partition.o
/usr/bin/flex --version
flex 2.6.4
/usr/bin/flex -d -oV3PreLex_pregen.yy.cpp ../V3PreLex.l
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3PreShell.cpp -o V3PreShell.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Premit.cpp -o V3Premit.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3ProtectLib.cpp -o V3ProtectLib.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Randomize.cpp -o V3Randomize.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Reloop.cpp -o V3Reloop.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Sched.cpp -o V3Sched.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3SchedAcyclic.cpp -o V3SchedAcyclic.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3SchedPartition.cpp -o V3SchedPartition.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3SchedReplicate.cpp -o V3SchedReplicate.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3SchedTiming.cpp -o V3SchedTiming.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Scope.cpp -o V3Scope.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Scoreboard.cpp -o V3Scoreboard.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Slice.cpp -o V3Slice.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Split.cpp -o V3Split.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3SplitAs.cpp -o V3SplitAs.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3SplitVar.cpp -o V3SplitVar.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Stats.cpp -o V3Stats.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3StatsReport.cpp -o V3StatsReport.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3String.cpp -o V3String.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Subst.cpp -o V3Subst.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3TSP.cpp -o V3TSP.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Table.cpp -o V3Table.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Task.cpp -o V3Task.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3ThreadPool.cpp -o V3ThreadPool.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Timing.cpp -o V3Timing.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Trace.cpp -o V3Trace.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3TraceDecl.cpp -o V3TraceDecl.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Tristate.cpp -o V3Tristate.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Undriven.cpp -o V3Undriven.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Unknown.cpp -o V3Unknown.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Unroll.cpp -o V3Unroll.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3VariableOrder.cpp -o V3VariableOrder.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Waiver.cpp -o V3Waiver.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3Width.cpp -o V3Width.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c ../V3WidthSel.cpp -o V3WidthSel.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -c V3Const__gen.cpp -o V3Const__gen.o
/usr/bin/python3 ../flexfix V3Lexer <V3Lexer_pregen.yy.cpp >V3Lexer.yy.cpp
/usr/bin/python3 ../flexfix V3PreLex <V3PreLex_pregen.yy.cpp >V3PreLex.yy.cpp
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -Wno-char-subscripts -Wno-unused -c ../V3PreProc.cpp -o V3PreProc.o
g++   -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP  -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC=\"\" -DDEFENV_SYSTEMC_ARCH=\"\" -DDEFENV_SYSTEMC_INCLUDE=\"\" -DDEFENV_SYSTEMC_LIBDIR=\"\" -DDEFENV_VERILATOR_ROOT=\"/home/kevin/verilator\" -Wno-char-subscripts -Wno-unused -c ../V3ParseLex.cpp -o V3ParseLex.o
      Linking ../../bin/verilator_bin_dbg...
g++  -gz -static-libgcc -static-libstdc++ -Xlinker -gc-sections -o ../../bin/verilator_bin_dbg Verilator.o V3Active.o V3ActiveTop.o V3Assert.o V3AssertPre.o V3Ast.o V3AstNodes.o V3Begin.o V3Branch.o V3Broken.o V3CCtors.o V3CUse.o V3Case.o V3Cast.o V3Class.o V3Clean.o V3Clock.o V3Combine.o V3Common.o V3Config.o V3Const__gen.o V3Coverage.o V3CoverageJoin.o V3Dead.o V3Delayed.o V3Depth.o V3DepthBlock.o V3Descope.o V3Dfg.o V3DfgAstToDfg.o V3DfgDecomposition.o V3DfgDfgToAst.o V3DfgOptimizer.o V3DfgPasses.o V3DfgPeephole.o V3DupFinder.o V3EmitCBase.o V3EmitCConstPool.o V3EmitCFunc.o V3EmitCHeaders.o V3EmitCImp.o V3EmitCInlines.o V3EmitCMain.o V3EmitCMake.o V3EmitCModel.o V3EmitCSyms.o V3EmitMk.o V3EmitV.o V3EmitXml.o V3Error.o V3Expand.o V3File.o V3FileLine.o V3Force.o V3Gate.o V3Global.o V3Graph.o V3GraphAcyc.o V3GraphAlg.o V3GraphPathChecker.o V3GraphTest.o V3Hash.o V3Hasher.o V3HierBlock.o V3Inline.o V3Inst.o V3InstrCount.o V3Life.o V3LifePost.o V3LinkCells.o V3LinkDot.o V3LinkInc.o V3LinkJump.o V3LinkLValue.o V3LinkLevel.o V3LinkParse.o V3LinkResolve.o V3Localize.o V3MergeCond.o V3Name.o V3Number.o V3OptionParser.o V3Options.o V3Order.o V3Os.o V3Param.o V3ParseGrammar.o V3ParseImp.o V3ParseLex.o V3Partition.o V3PreProc.o V3PreShell.o V3Premit.o V3ProtectLib.o V3Randomize.o V3Reloop.o V3Sched.o V3SchedAcyclic.o V3SchedPartition.o V3SchedReplicate.o V3SchedTiming.o V3Scope.o V3Scoreboard.o V3Slice.o V3Split.o V3SplitAs.o V3SplitVar.o V3Stats.o V3StatsReport.o V3String.o V3Subst.o V3TSP.o V3Table.o V3Task.o V3ThreadPool.o V3Timing.o V3Trace.o V3TraceDecl.o V3Tristate.o V3Undriven.o V3Unknown.o V3Unroll.o V3VariableOrder.o V3Waiver.o V3Width.o V3WidthSel.o   -lpthread -lm
make[2]: Leaving directory '/home/kevin/verilator/src/obj_dbg'
      Linking ../../bin/verilator_bin...
g++  -static-libgcc -static-libstdc++ -Xlinker -gc-sections -o ../../bin/verilator_bin Verilator.o V3Active.o V3ActiveTop.o V3Assert.o V3AssertPre.o V3Ast.o V3AstNodes.o V3Begin.o V3Branch.o V3Broken.o V3CCtors.o V3CUse.o V3Case.o V3Cast.o V3Class.o V3Clean.o V3Clock.o V3Combine.o V3Common.o V3Config.o V3Const__gen.o V3Coverage.o V3CoverageJoin.o V3Dead.o V3Delayed.o V3Depth.o V3DepthBlock.o V3Descope.o V3Dfg.o V3DfgAstToDfg.o V3DfgDecomposition.o V3DfgDfgToAst.o V3DfgOptimizer.o V3DfgPasses.o V3DfgPeephole.o V3DupFinder.o V3EmitCBase.o V3EmitCConstPool.o V3EmitCFunc.o V3EmitCHeaders.o V3EmitCImp.o V3EmitCInlines.o V3EmitCMain.o V3EmitCMake.o V3EmitCModel.o V3EmitCSyms.o V3EmitMk.o V3EmitV.o V3EmitXml.o V3Error.o V3Expand.o V3File.o V3FileLine.o V3Force.o V3Gate.o V3Global.o V3Graph.o V3GraphAcyc.o V3GraphAlg.o V3GraphPathChecker.o V3GraphTest.o V3Hash.o V3Hasher.o V3HierBlock.o V3Inline.o V3Inst.o V3InstrCount.o V3Life.o V3LifePost.o V3LinkCells.o V3LinkDot.o V3LinkInc.o V3LinkJump.o V3LinkLValue.o V3LinkLevel.o V3LinkParse.o V3LinkResolve.o V3Localize.o V3MergeCond.o V3Name.o V3Number.o V3OptionParser.o V3Options.o V3Order.o V3Os.o V3Param.o V3ParseGrammar.o V3ParseImp.o V3ParseLex.o V3Partition.o V3PreProc.o V3PreShell.o V3Premit.o V3ProtectLib.o V3Randomize.o V3Reloop.o V3Sched.o V3SchedAcyclic.o V3SchedPartition.o V3SchedReplicate.o V3SchedTiming.o V3Scope.o V3Scoreboard.o V3Slice.o V3Split.o V3SplitAs.o V3SplitVar.o V3Stats.o V3StatsReport.o V3String.o V3Subst.o V3TSP.o V3Table.o V3Task.o V3ThreadPool.o V3Timing.o V3Trace.o V3TraceDecl.o V3Tristate.o V3Undriven.o V3Unknown.o V3Unroll.o V3VariableOrder.o V3Waiver.o V3Width.o V3WidthSel.o   -lpthread -lm
make[2]: Leaving directory '/home/kevin/verilator/src/obj_opt'
make[1]: Leaving directory '/home/kevin/verilator/src'
Build complete!

Now type 'make test' to test.

kevin@kevin:~/verilator$ sudo make install
------------------------------------------------------------
making verilator in src
make -C src
make[1]: Entering directory '/home/kevin/verilator/src'
make -C obj_dbg -j 1  TGT=../../bin/verilator_bin_dbg VL_DEBUG=1 -f ../Makefile_obj serial
make[2]: Entering directory '/home/kevin/verilator/src/obj_dbg'
make[2]: Nothing to be done for 'serial'.
make[2]: Leaving directory '/home/kevin/verilator/src/obj_dbg'
make -C obj_dbg       TGT=../../bin/verilator_bin_dbg VL_DEBUG=1 -f ../Makefile_obj
make[2]: Entering directory '/home/kevin/verilator/src/obj_dbg'
      Compile flags:  g++ -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC="" -DDEFENV_SYSTEMC_ARCH="" -DDEFENV_SYSTEMC_INCLUDE="" -DDEFENV_SYSTEMC_LIBDIR="" -DDEFENV_VERILATOR_ROOT="/usr/local/share/verilator"
make[2]: Leaving directory '/home/kevin/verilator/src/obj_dbg'
make -C obj_dbg       TGT=../../bin/verilator_coverage_bin_dbg VL_DEBUG=1 VL_VLCOV=1 -f ../Makefile_obj serial_vlcov
make[2]: Entering directory '/home/kevin/verilator/src/obj_dbg'
make[2]: Nothing to be done for 'serial_vlcov'.
make[2]: Leaving directory '/home/kevin/verilator/src/obj_dbg'
make -C obj_dbg       TGT=../../bin/verilator_coverage_bin_dbg VL_DEBUG=1 VL_VLCOV=1 -f ../Makefile_obj
make[2]: Entering directory '/home/kevin/verilator/src/obj_dbg'
      Compile flags:  g++ -Og -ggdb -gz -DVL_DEBUG -D_GLIBCXX_DEBUG -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC="" -DDEFENV_SYSTEMC_ARCH="" -DDEFENV_SYSTEMC_INCLUDE="" -DDEFENV_SYSTEMC_LIBDIR="" -DDEFENV_VERILATOR_ROOT="/usr/local/share/verilator"
make[2]: Leaving directory '/home/kevin/verilator/src/obj_dbg'
make -C obj_opt -j 1  TGT=../../bin/verilator_bin -f ../Makefile_obj serial
make[2]: Entering directory '/home/kevin/verilator/src/obj_opt'
make[2]: Nothing to be done for 'serial'.
make[2]: Leaving directory '/home/kevin/verilator/src/obj_opt'
make -C obj_opt       TGT=../../bin/verilator_bin -f ../Makefile_obj
make[2]: Entering directory '/home/kevin/verilator/src/obj_opt'
      Compile flags:  g++ -O3 -DVERILATOR_INTERNAL_ -MMD -I. -I.. -I.. -I../../include -I../../include -MP -faligned-new -Wno-unused-parameter -Wno-shadow -DDEFENV_SYSTEMC="" -DDEFENV_SYSTEMC_ARCH="" -DDEFENV_SYSTEMC_INCLUDE="" -DDEFENV_SYSTEMC_LIBDIR="" -DDEFENV_VERILATOR_ROOT="/usr/local/share/verilator"
make[2]: Leaving directory '/home/kevin/verilator/src/obj_opt'
make[1]: Leaving directory '/home/kevin/verilator/src'
/bin/sh ./src/mkinstalldirs /usr/local/bin
( cd ./bin ; /usr/bin/install -c verilator /usr/local/bin/verilator )
( cd ./bin ; /usr/bin/install -c verilator_coverage /usr/local/bin/verilator_coverage )
( cd ./bin ; /usr/bin/install -c verilator_gantt /usr/local/bin/verilator_gantt )
( cd ./bin ; /usr/bin/install -c verilator_profcfunc /usr/local/bin/verilator_profcfunc )
( cd bin ; /usr/bin/install -c verilator_bin /usr/local/bin/verilator_bin )
( cd bin ; /usr/bin/install -c verilator_bin_dbg /usr/local/bin/verilator_bin_dbg )
( cd bin ; /usr/bin/install -c verilator_coverage_bin_dbg /usr/local/bin/verilator_coverage_bin_dbg )
/bin/sh ./src/mkinstalldirs /usr/local/share/verilator/bin
mkdir /usr/local/share/verilator
mkdir /usr/local/share/verilator/bin
( cd ./bin ; /usr/bin/install -c verilator_includer /usr/local/share/verilator/bin/verilator_includer )
( cd ./bin ; /usr/bin/install -c verilator_ccache_report /usr/local/share/verilator/bin/verilator_ccache_report )
( cd ./bin ; /usr/bin/install -c verilator_difftree /usr/local/share/verilator/bin/verilator_difftree )
/bin/sh ./src/mkinstalldirs /usr/local/share/man/man1
mkdir /usr/local/share/man/man1
for p in verilator.1 verilator_coverage.1 verilator_gantt.1 verilator_profcfunc.1 ; do \
  /usr/bin/install -c -m 644 $p /usr/local/share/man/man1/$p; \
done
/bin/sh ./src/mkinstalldirs /usr/local/share/verilator/include/gtkwave
mkdir /usr/local/share/verilator/include
mkdir /usr/local/share/verilator/include/gtkwave
/bin/sh ./src/mkinstalldirs /usr/local/share/verilator/include/vltstd
mkdir /usr/local/share/verilator/include/vltstd
for p in include/verilated_config.h include/verilated.mk  ; do \
  /usr/bin/install -c -m 644 $p /usr/local/share/verilator/$p; \
done
cd . \
; for p in include/*.[chv]* include/*.sv include/gtkwave/*.[chv]* include/vltstd/*.[chv]*  ; do \
  /usr/bin/install -c -m 644 $p /usr/local/share/verilator/$p; \
done
/bin/sh ./src/mkinstalldirs /usr/local/share/verilator/examples/make_hello_binary
mkdir /usr/local/share/verilator/examples
mkdir /usr/local/share/verilator/examples/make_hello_binary
/bin/sh ./src/mkinstalldirs /usr/local/share/verilator/examples/make_hello_c
mkdir /usr/local/share/verilator/examples/make_hello_c
/bin/sh ./src/mkinstalldirs /usr/local/share/verilator/examples/make_hello_sc
mkdir /usr/local/share/verilator/examples/make_hello_sc
/bin/sh ./src/mkinstalldirs /usr/local/share/verilator/examples/make_tracing_c
mkdir /usr/local/share/verilator/examples/make_tracing_c
/bin/sh ./src/mkinstalldirs /usr/local/share/verilator/examples/make_tracing_sc
mkdir /usr/local/share/verilator/examples/make_tracing_sc
/bin/sh ./src/mkinstalldirs /usr/local/share/verilator/examples/make_protect_lib
mkdir /usr/local/share/verilator/examples/make_protect_lib
/bin/sh ./src/mkinstalldirs /usr/local/share/verilator/examples/cmake_hello_c
mkdir /usr/local/share/verilator/examples/cmake_hello_c
/bin/sh ./src/mkinstalldirs /usr/local/share/verilator/examples/cmake_hello_sc
mkdir /usr/local/share/verilator/examples/cmake_hello_sc
/bin/sh ./src/mkinstalldirs /usr/local/share/verilator/examples/cmake_tracing_c
mkdir /usr/local/share/verilator/examples/cmake_tracing_c
/bin/sh ./src/mkinstalldirs /usr/local/share/verilator/examples/cmake_tracing_sc
mkdir /usr/local/share/verilator/examples/cmake_tracing_sc
/bin/sh ./src/mkinstalldirs /usr/local/share/verilator/examples/cmake_protect_lib
mkdir /usr/local/share/verilator/examples/cmake_protect_lib
/bin/sh ./src/mkinstalldirs /usr/local/share/verilator/examples/xml_py
mkdir /usr/local/share/verilator/examples/xml_py
cd . \
; for p in examples/*/*.[chv]* examples/*/CMakeLists.txt examples/*/Makefile* examples/*/vl_*  ; do \
  /usr/bin/install -c -m 644 $p /usr/local/share/verilator/$p; \
done
/bin/sh ./src/mkinstalldirs /usr/local/share/pkgconfig
mkdir /usr/local/share/pkgconfig
/usr/bin/install -c -m 644 verilator.pc /usr/local/share/pkgconfig
/usr/bin/install -c -m 644 verilator-config.cmake /usr/local/share/verilator
/usr/bin/install -c -m 644 verilator-config-version.cmake /usr/local/share/verilator

Installed binaries to /usr/local/bin/verilator
Installed man to /usr/local/share/man/man1
Installed examples to /usr/local/share/verilator/examples

For documentation see 'man verilator' or 'verilator --help'
For forums and to report bugs see https://verilator.org
```

Install litex python3 dependencies
```
cd ~
python3 -m pip install ninja
python3 -m pip install meson==0.59
export PATH=$PATH:~/.local/bin
```
```console
kevin@kevin:~/verilator$ cd ~
kevin@kevin:~$ python3 -m pip install ninja
Collecting ninja
  Downloading ninja-1.11.1-py2.py3-none-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (145 kB)
     |████████████████████████████████| 145 kB 1.2 MB/s
Installing collected packages: ninja
  WARNING: The script ninja is installed in '/home/kevin/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
Successfully installed ninja-1.11.1
kevin@kevin:~$ python3 -m pip install meson==0.59
Collecting meson==0.59
  Downloading meson-0.59.0.tar.gz (1.9 MB)
     |████████████████████████████████| 1.9 MB 1.2 MB/s
  Installing build dependencies ... done
  Getting requirements to build wheel ... done
    Preparing wheel metadata ... done
Building wheels for collected packages: meson
  Building wheel for meson (PEP 517) ... done
  Created wheel for meson: filename=meson-0.59.0-py3-none-any.whl size=806970 sha256=5896455dfb37178037a3fb4e2593fb0396346c8a2b9986e35094354419af2d5a
  Stored in directory: /home/kevin/.cache/pip/wheels/40/a1/44/b17f8e03263417243f4af1e1deb7851cbeef292251c7364bc0
Successfully built meson
Installing collected packages: meson
  WARNING: The script meson is installed in '/home/kevin/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
Successfully installed meson-0.59.0
kevin@kevin:~$ export PATH=$PATH:~/.local/bin
```
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
```console
kevin@kevin:~$ git clone https://github.com/litex-hub/linux-on-litex-vexriscv
Cloning into 'linux-on-litex-vexriscv'...
remote: Enumerating objects: 2685, done.
remote: Counting objects: 100% (600/600), done.
remote: Compressing objects: 100% (294/294), done.
remote: Total 2685 (delta 352), reused 430 (delta 295), pack-reused 2085
Receiving objects: 100% (2685/2685), 9.50 MiB | 8.46 MiB/s, done.
Resolving deltas: 100% (1497/1497), done.
kevin@kevin:~$ cd linux-on-litex-vexriscv
kevin@kevin:~/linux-on-litex-vexriscv$ wget https://raw.githubusercontent.com/enjoy-digital/litex/master/litex_setup.py
--2023-04-29 12:48:23--  https://raw.githubusercontent.com/enjoy-digital/litex/master/litex_setup.py
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.108.133, 185.199.110.133, 185.199.111.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.108.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 19112 (19K) [text/plain]
Saving to: ‘litex_setup.py’

litex_setup.py                          100%[=============================================================================>]  18.66K  --.-KB/s    in 0.005s

2023-04-29 12:48:23 (3.66 MB/s) - ‘litex_setup.py’ saved [19112/19112]

kevin@kevin:~/linux-on-litex-vexriscv$ chmod +x litex_setup.py
kevin@kevin:~/linux-on-litex-vexriscv$ ./litex_setup.py --init --install --user --config=full
          __   _ __      _  __
         / /  (_) /____ | |/_/
        / /__/ / __/ -_)>  <
       /____/_/\__/\__/_/|_|
     Build your hardware, easily!
          LiteX Setup utility.

[   0.003] LiteX Setup auto-update...
[   0.496] LiteX Setup is up to date.
[   0.497] Initializing Git repositories...
[   0.497] --------------------------------
[   0.497] Cloning migen Git repository...
Cloning into 'migen'...
remote: Enumerating objects: 12641, done.
remote: Counting objects: 100% (210/210), done.
remote: Compressing objects: 100% (100/100), done.
remote: Total 12641 (delta 142), reused 160 (delta 110), pack-reused 12431
Receiving objects: 100% (12641/12641), 3.09 MiB | 9.22 MiB/s, done.
Resolving deltas: 100% (8222/8222), done.
Already on 'master'
Your branch is up to date with 'origin/master'.
[   1.838] Cloning pythondata-software-picolibc Git repository...
Cloning into 'pythondata-software-picolibc'...
remote: Enumerating objects: 734, done.
remote: Counting objects: 100% (266/266), done.
remote: Compressing objects: 100% (194/194), done.
remote: Total 734 (delta 122), reused 215 (delta 72), pack-reused 468
Receiving objects: 100% (734/734), 132.85 KiB | 1.41 MiB/s, done.
Resolving deltas: 100% (331/331), done.
Submodule 'pythondata_software_picolibc/data' (https://github.com/picolibc/picolibc) registered for path 'pythondata_software_picolibc/data'
Cloning into '/home/kevin/pythondata-software-picolibc/pythondata_software_picolibc/data'...
remote: Enumerating objects: 225975, done.
remote: Counting objects: 100% (165/165), done.
remote: Compressing objects: 100% (103/103), done.
remote: Total 225975 (delta 75), reused 117 (delta 62), pack-reused 225810
Receiving objects: 100% (225975/225975), 134.40 MiB | 16.37 MiB/s, done.
Resolving deltas: 100% (180483/180483), done.
Submodule path 'pythondata_software_picolibc/data': checked out 'f165dc22f1f67e3e8bdc8edf750ff7dc596de2ff'
Already on 'master'
Your branch is up to date with 'origin/master'.
[  25.034] Cloning pythondata-software-compiler_rt Git repository...
Cloning into 'pythondata-software-compiler_rt'...
remote: Enumerating objects: 51970, done.
remote: Counting objects: 100% (93/93), done.
remote: Compressing objects: 100% (73/73), done.
remote: Total 51970 (delta 53), reused 58 (delta 19), pack-reused 51877
Receiving objects: 100% (51970/51970), 8.46 MiB | 11.78 MiB/s, done.
Resolving deltas: 100% (42889/42889), done.
Already on 'master'
Your branch is up to date with 'origin/master'.
[  27.755] Cloning litex Git repository...
Cloning into 'litex'...
remote: Enumerating objects: 61785, done.
remote: Counting objects: 100% (61785/61785), done.
remote: Compressing objects: 100% (17783/17783), done.
remote: Total 61785 (delta 43074), reused 61579 (delta 43006), pack-reused 0
Receiving objects: 100% (61785/61785), 15.50 MiB | 15.13 MiB/s, done.
Resolving deltas: 100% (43074/43074), done.
Already on 'master'
Your branch is up to date with 'origin/master'.
[  30.412] Cloning liteeth Git repository...
Cloning into 'liteeth'...
remote: Enumerating objects: 3241, done.
remote: Counting objects: 100% (973/973), done.
remote: Compressing objects: 100% (172/172), done.
remote: Total 3241 (delta 863), reused 850 (delta 797), pack-reused 2268
Receiving objects: 100% (3241/3241), 1.11 MiB | 5.11 MiB/s, done.
Resolving deltas: 100% (2308/2308), done.
Already on 'master'
Your branch is up to date with 'origin/master'.
[  31.485] Cloning litedram Git repository...
Cloning into 'litedram'...
remote: Enumerating objects: 8253, done.
remote: Counting objects: 100% (8253/8253), done.
remote: Compressing objects: 100% (2126/2126), done.
remote: Total 8253 (delta 6113), reused 8160 (delta 6086), pack-reused 0
Receiving objects: 100% (8253/8253), 3.28 MiB | 9.34 MiB/s, done.
Resolving deltas: 100% (6113/6113), done.
Already on 'master'
Your branch is up to date with 'origin/master'.
[  34.039] Cloning litepcie Git repository...
Cloning into 'litepcie'...
remote: Enumerating objects: 4758, done.
remote: Counting objects: 100% (1025/1025), done.
remote: Compressing objects: 100% (299/299), done.
remote: Total 4758 (delta 744), reused 918 (delta 703), pack-reused 3733
Receiving objects: 100% (4758/4758), 1.46 MiB | 6.40 MiB/s, done.
Resolving deltas: 100% (3225/3225), done.
Already on 'master'
Your branch is up to date with 'origin/master'.
[  35.155] Cloning litesata Git repository...
Cloning into 'litesata'...
remote: Enumerating objects: 2295, done.
remote: Counting objects: 100% (628/628), done.
remote: Compressing objects: 100% (199/199), done.
remote: Total 2295 (delta 436), reused 617 (delta 426), pack-reused 1667
Receiving objects: 100% (2295/2295), 1.13 MiB | 5.01 MiB/s, done.
Resolving deltas: 100% (1521/1521), done.
Already on 'master'
Your branch is up to date with 'origin/master'.
[  36.192] Cloning litesdcard Git repository...
Cloning into 'litesdcard'...
remote: Enumerating objects: 1990, done.
remote: Counting objects: 100% (132/132), done.
remote: Compressing objects: 100% (58/58), done.
remote: Total 1990 (delta 74), reused 124 (delta 72), pack-reused 1858
Receiving objects: 100% (1990/1990), 7.34 MiB | 12.78 MiB/s, done.
Resolving deltas: 100% (1270/1270), done.
Already on 'master'
Your branch is up to date with 'origin/master'.
[  37.646] Cloning liteiclink Git repository...
Cloning into 'liteiclink'...
remote: Enumerating objects: 2419, done.
remote: Counting objects: 100% (135/135), done.
remote: Compressing objects: 100% (90/90), done.
remote: Total 2419 (delta 81), reused 80 (delta 41), pack-reused 2284
Receiving objects: 100% (2419/2419), 547.97 KiB | 3.01 MiB/s, done.
Resolving deltas: 100% (1626/1626), done.
Already on 'master'
Your branch is up to date with 'origin/master'.
[  38.660] Cloning litescope Git repository...
Cloning into 'litescope'...
remote: Enumerating objects: 1219, done.
remote: Counting objects: 100% (55/55), done.
remote: Compressing objects: 100% (37/37), done.
remote: Total 1219 (delta 21), reused 34 (delta 12), pack-reused 1164
Receiving objects: 100% (1219/1219), 589.66 KiB | 3.26 MiB/s, done.
Resolving deltas: 100% (639/639), done.
Already on 'master'
Your branch is up to date with 'origin/master'.
[  39.651] Cloning litejesd204b Git repository...
Cloning into 'litejesd204b'...
remote: Enumerating objects: 1948, done.
remote: Counting objects: 100% (187/187), done.
remote: Compressing objects: 100% (88/88), done.
remote: Total 1948 (delta 106), reused 173 (delta 95), pack-reused 1761
Receiving objects: 100% (1948/1948), 482.85 KiB | 2.77 MiB/s, done.
Resolving deltas: 100% (1290/1290), done.
Already on 'master'
Your branch is up to date with 'origin/master'.
[  40.619] Cloning litespi Git repository...
Cloning into 'litespi'...
remote: Enumerating objects: 854, done.
remote: Counting objects: 100% (247/247), done.
remote: Compressing objects: 100% (111/111), done.
remote: Total 854 (delta 178), reused 169 (delta 133), pack-reused 607
Receiving objects: 100% (854/854), 204.00 KiB | 1.85 MiB/s, done.
Resolving deltas: 100% (529/529), done.
Already on 'master'
Your branch is up to date with 'origin/master'.
[  41.566] Cloning valentyusb Git repository...
Cloning into 'valentyusb'...
remote: Enumerating objects: 3073, done.
remote: Counting objects: 100% (33/33), done.
remote: Compressing objects: 100% (19/19), done.
remote: Total 3073 (delta 14), reused 29 (delta 14), pack-reused 3040
Receiving objects: 100% (3073/3073), 747.23 KiB | 3.79 MiB/s, done.
Resolving deltas: 100% (1989/1989), done.
Branch 'hw_cdc_eptri' set up to track remote branch 'hw_cdc_eptri' from 'origin'.
Switched to a new branch 'hw_cdc_eptri'
[  42.612] Cloning litex-boards Git repository...
Cloning into 'litex-boards'...
remote: Enumerating objects: 13329, done.
remote: Counting objects: 100% (552/552), done.
remote: Compressing objects: 100% (180/180), done.
remote: Total 13329 (delta 407), reused 469 (delta 372), pack-reused 12777
Receiving objects: 100% (13329/13329), 3.62 MiB | 10.29 MiB/s, done.
Resolving deltas: 100% (10367/10367), done.
Already on 'master'
Your branch is up to date with 'origin/master'.
[  44.011] Cloning pythondata-misc-tapcfg Git repository...
Cloning into 'pythondata-misc-tapcfg'...
remote: Enumerating objects: 2874, done.
remote: Counting objects: 100% (296/296), done.
remote: Compressing objects: 100% (104/104), done.
remote: Total 2874 (delta 184), reused 287 (delta 175), pack-reused 2578
Receiving objects: 100% (2874/2874), 647.06 KiB | 3.50 MiB/s, done.
Resolving deltas: 100% (1891/1891), done.
Already on 'master'
Your branch is up to date with 'origin/master'.
[  45.027] Cloning pythondata-misc-usb_ohci Git repository...
Cloning into 'pythondata-misc-usb_ohci'...
remote: Enumerating objects: 19, done.
remote: Counting objects: 100% (19/19), done.
remote: Compressing objects: 100% (12/12), done.
remote: Total 19 (delta 2), reused 19 (delta 2), pack-reused 0
Unpacking objects: 100% (19/19), 43.20 KiB | 465.00 KiB/s, done.
Already on 'master'
Your branch is up to date with 'origin/master'.
[  45.849] Cloning pythondata-cpu-lm32 Git repository...
Cloning into 'pythondata-cpu-lm32'...
remote: Enumerating objects: 820, done.
remote: Counting objects: 100% (76/76), done.
remote: Compressing objects: 100% (23/23), done.
remote: Total 820 (delta 65), reused 62 (delta 53), pack-reused 744
Receiving objects: 100% (820/820), 245.63 KiB | 1.79 MiB/s, done.
Resolving deltas: 100% (474/474), done.
Already on 'master'
Your branch is up to date with 'origin/master'.
[  46.819] Cloning pythondata-cpu-mor1kx Git repository...
Cloning into 'pythondata-cpu-mor1kx'...
remote: Enumerating objects: 4939, done.
remote: Counting objects: 100% (923/923), done.
remote: Compressing objects: 100% (339/339), done.
remote: Total 4939 (delta 526), reused 906 (delta 509), pack-reused 4016
Receiving objects: 100% (4939/4939), 1.84 MiB | 6.54 MiB/s, done.
Resolving deltas: 100% (2853/2853), done.
Already on 'master'
Your branch is up to date with 'origin/master'.
[  48.032] Cloning pythondata-cpu-marocchino Git repository...
Cloning into 'pythondata-cpu-marocchino'...
remote: Enumerating objects: 541, done.
remote: Counting objects: 100% (541/541), done.
remote: Compressing objects: 100% (199/199), done.
remote: Total 541 (delta 316), reused 518 (delta 293), pack-reused 0
Receiving objects: 100% (541/541), 368.30 KiB | 2.63 MiB/s, done.
Resolving deltas: 100% (316/316), done.
Already on 'master'
Your branch is up to date with 'origin/master'.
[  49.024] Cloning pythondata-cpu-microwatt Git repository...
Cloning into 'pythondata-cpu-microwatt'...
remote: Enumerating objects: 11922, done.
remote: Counting objects: 100% (3778/3778), done.
remote: Compressing objects: 100% (1356/1356), done.
remote: Total 11922 (delta 2408), reused 3712 (delta 2345), pack-reused 8144
Receiving objects: 100% (11922/11922), 68.38 MiB | 16.46 MiB/s, done.
Resolving deltas: 100% (7164/7164), done.
Already on 'master'
Your branch is up to date with 'origin/master'.
Note: switching to 'c69953aff92'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at c69953a Merge commit '7d928200b81851c6a0ead589297b357dcdf762f2'
[  56.338] Cloning pythondata-cpu-blackparrot Git repository...
Cloning into 'pythondata-cpu-blackparrot'...
remote: Enumerating objects: 26128, done.
remote: Counting objects: 100% (3365/3365), done.
remote: Compressing objects: 100% (1759/1759), done.
remote: Total 26128 (delta 1520), reused 3334 (delta 1516), pack-reused 22763
Receiving objects: 100% (26128/26128), 25.15 MiB | 15.10 MiB/s, done.
Resolving deltas: 100% (17833/17833), done.
Already on 'master'
Your branch is up to date with 'origin/master'.
[  60.247] Cloning pythondata-cpu-cv32e40p Git repository...
Cloning into 'pythondata-cpu-cv32e40p'...
remote: Enumerating objects: 6242, done.
remote: Counting objects: 100% (228/228), done.
remote: Compressing objects: 100% (72/72), done.
remote: Total 6242 (delta 141), reused 226 (delta 140), pack-reused 6014
Receiving objects: 100% (6242/6242), 3.22 MiB | 10.10 MiB/s, done.
Resolving deltas: 100% (4420/4420), done.
Submodule 'pythondata_cpu_cv32e40p/system_verilog/rtl/fpnew' (https://github.com/antmicro/fpnew.git) registered for path 'pythondata_cpu_cv32e40p/system_verilog/rtl/fpnew'
Submodule 'pythondata_cpu_cv32e40p/system_verilog/rtl/riscv-dbg' (https://github.com/antmicro/riscv-dbg.git) registered for path 'pythondata_cpu_cv32e40p/system_verilog/rtl/riscv-dbg'
Submodule 'pythondata_cpu_cv32e40p/system_verilog/rtl/trace_debugger' (https://github.com/antmicro/trace_debugger.git) registered for path 'pythondata_cpu_cv32e40p/system_verilog/rtl/trace_debugger'
Cloning into '/home/kevin/pythondata-cpu-cv32e40p/pythondata_cpu_cv32e40p/system_verilog/rtl/fpnew'...
remote: Enumerating objects: 1401, done.
remote: Counting objects: 100% (206/206), done.
remote: Compressing objects: 100% (18/18), done.
remote: Total 1401 (delta 195), reused 188 (delta 188), pack-reused 1195
Receiving objects: 100% (1401/1401), 668.81 KiB | 3.61 MiB/s, done.
Resolving deltas: 100% (1004/1004), done.
Cloning into '/home/kevin/pythondata-cpu-cv32e40p/pythondata_cpu_cv32e40p/system_verilog/rtl/riscv-dbg'...
remote: Enumerating objects: 880, done.
remote: Counting objects: 100% (251/251), done.
remote: Compressing objects: 100% (20/20), done.
remote: Total 880 (delta 234), reused 231 (delta 231), pack-reused 629
Receiving objects: 100% (880/880), 309.81 KiB | 2.15 MiB/s, done.
Resolving deltas: 100% (562/562), done.
Cloning into '/home/kevin/pythondata-cpu-cv32e40p/pythondata_cpu_cv32e40p/system_verilog/rtl/trace_debugger'...
remote: Enumerating objects: 2946, done.
remote: Counting objects: 100% (12/12), done.
remote: Compressing objects: 100% (11/11), done.
remote: Total 2946 (delta 4), reused 4 (delta 1), pack-reused 2934
Receiving objects: 100% (2946/2946), 7.04 MiB | 8.31 MiB/s, done.
Resolving deltas: 100% (2061/2061), done.
Submodule path 'pythondata_cpu_cv32e40p/system_verilog/rtl/fpnew': checked out '855bb82b6e85772fc290fa8b9c14fdd8f1b16be7'
Submodule 'src-sv/common_cells' (https://github.com/pulp-platform/common_cells.git) registered for path 'pythondata_cpu_cv32e40p/system_verilog/rtl/fpnew/src/common_cells'
Submodule 'src-sv/fpu_div_sqrt_mvp' (https://github.com/pulp-platform/fpu_div_sqrt_mvp.git) registered for path 'pythondata_cpu_cv32e40p/system_verilog/rtl/fpnew/src/fpu_div_sqrt_mvp'
Submodule 'tb/flexfloat' (https://github.com/oprecomp/flexfloat.git) registered for path 'pythondata_cpu_cv32e40p/system_verilog/rtl/fpnew/tb/flexfloat'
Cloning into '/home/kevin/pythondata-cpu-cv32e40p/pythondata_cpu_cv32e40p/system_verilog/rtl/fpnew/src/common_cells'...
remote: Enumerating objects: 2709, done.
remote: Counting objects: 100% (575/575), done.
remote: Compressing objects: 100% (222/222), done.
remote: Total 2709 (delta 436), reused 420 (delta 352), pack-reused 2134
Receiving objects: 100% (2709/2709), 762.01 KiB | 4.07 MiB/s, done.
Resolving deltas: 100% (1836/1836), done.
Cloning into '/home/kevin/pythondata-cpu-cv32e40p/pythondata_cpu_cv32e40p/system_verilog/rtl/fpnew/src/fpu_div_sqrt_mvp'...
remote: Enumerating objects: 210, done.
remote: Counting objects: 100% (18/18), done.
remote: Compressing objects: 100% (15/15), done.
remote: Total 210 (delta 6), reused 10 (delta 3), pack-reused 192
Receiving objects: 100% (210/210), 775.64 KiB | 3.80 MiB/s, done.
Resolving deltas: 100% (127/127), done.
Cloning into '/home/kevin/pythondata-cpu-cv32e40p/pythondata_cpu_cv32e40p/system_verilog/rtl/fpnew/tb/flexfloat'...
remote: Enumerating objects: 206, done.
remote: Counting objects: 100% (63/63), done.
remote: Compressing objects: 100% (38/38), done.
remote: Total 206 (delta 25), reused 41 (delta 16), pack-reused 143
Receiving objects: 100% (206/206), 88.67 KiB | 1.17 MiB/s, done.
Resolving deltas: 100% (90/90), done.
Submodule path 'pythondata_cpu_cv32e40p/system_verilog/rtl/fpnew/src/common_cells': checked out '790f2385c01c83022474eede55809666209216e3'
Submodule path 'pythondata_cpu_cv32e40p/system_verilog/rtl/fpnew/src/fpu_div_sqrt_mvp': checked out '83a601f97934ed5e06d737b9c80d98b08867c5fa'
Submodule path 'pythondata_cpu_cv32e40p/system_verilog/rtl/fpnew/tb/flexfloat': checked out '28be2d4fbf41b38fc37763bb6e90a1c88f6aaa61'
Submodule path 'pythondata_cpu_cv32e40p/system_verilog/rtl/riscv-dbg': checked out '6d38d957b036231db668666255e938c91b7ce424'
Submodule path 'pythondata_cpu_cv32e40p/system_verilog/rtl/trace_debugger': checked out '0aafa398e208ad79826407e3805642987287cfae'
Submodule 'rtl/axi' (https://github.com/pulp-platform/axi.git) registered for path 'pythondata_cpu_cv32e40p/system_verilog/rtl/trace_debugger/rtl/axi'
Submodule 'rtl/common_cells' (https://github.com/pulp-platform/common_cells.git) registered for path 'pythondata_cpu_cv32e40p/system_verilog/rtl/trace_debugger/rtl/common_cells'
Submodule 'rtl/tech_cells_generic' (https://github.com/pulp-platform/tech_cells_generic.git) registered for path 'pythondata_cpu_cv32e40p/system_verilog/rtl/trace_debugger/rtl/tech_cells_generic'
Submodule 'trdb' (https://github.com/pulp-platform/trdb.git) registered for path 'pythondata_cpu_cv32e40p/system_verilog/rtl/trace_debugger/trdb'
Cloning into '/home/kevin/pythondata-cpu-cv32e40p/pythondata_cpu_cv32e40p/system_verilog/rtl/trace_debugger/rtl/axi'...
remote: Enumerating objects: 10145, done.
remote: Counting objects: 100% (1841/1841), done.
remote: Compressing objects: 100% (228/228), done.
remote: Total 10145 (delta 1697), reused 1669 (delta 1610), pack-reused 8304
Receiving objects: 100% (10145/10145), 6.00 MiB | 14.96 MiB/s, done.
Resolving deltas: 100% (7405/7405), done.
Cloning into '/home/kevin/pythondata-cpu-cv32e40p/pythondata_cpu_cv32e40p/system_verilog/rtl/trace_debugger/rtl/common_cells'...
remote: Enumerating objects: 2709, done.
remote: Counting objects: 100% (564/564), done.
remote: Compressing objects: 100% (217/217), done.
remote: Total 2709 (delta 426), reused 414 (delta 346), pack-reused 2145
Receiving objects: 100% (2709/2709), 763.46 KiB | 4.34 MiB/s, done.
Resolving deltas: 100% (1836/1836), done.
Cloning into '/home/kevin/pythondata-cpu-cv32e40p/pythondata_cpu_cv32e40p/system_verilog/rtl/trace_debugger/rtl/tech_cells_generic'...
remote: Enumerating objects: 525, done.
remote: Counting objects: 100% (198/198), done.
remote: Compressing objects: 100% (117/117), done.
remote: Total 525 (delta 100), reused 162 (delta 81), pack-reused 327
Receiving objects: 100% (525/525), 110.99 KiB | 1.32 MiB/s, done.
Resolving deltas: 100% (307/307), done.
Cloning into '/home/kevin/pythondata-cpu-cv32e40p/pythondata_cpu_cv32e40p/system_verilog/rtl/trace_debugger/trdb'...
remote: Enumerating objects: 1504, done.
remote: Total 1504 (delta 0), reused 0 (delta 0), pack-reused 1504
Receiving objects: 100% (1504/1504), 6.11 MiB | 7.17 MiB/s, done.
Resolving deltas: 100% (939/939), done.
Submodule path 'pythondata_cpu_cv32e40p/system_verilog/rtl/trace_debugger/rtl/axi': checked out '56440b0aad762cbfe2979b71e73f848d90b110d6'
Submodule path 'pythondata_cpu_cv32e40p/system_verilog/rtl/trace_debugger/rtl/common_cells': checked out '5b7021208a3ff818a617b497c5b5564f412fe0a8'
Submodule path 'pythondata_cpu_cv32e40p/system_verilog/rtl/trace_debugger/rtl/tech_cells_generic': checked out '0c5b6089c3d850843b72a9d1120414137976d746'
Submodule path 'pythondata_cpu_cv32e40p/system_verilog/rtl/trace_debugger/trdb': checked out '5bbece538796a170ae5ae78310608383f1823ad1'
Already on 'master'
Your branch is up to date with 'origin/master'.
[  74.754] Cloning pythondata-cpu-cv32e41p Git repository...
Cloning into 'pythondata-cpu-cv32e41p'...
remote: Enumerating objects: 9592, done.
remote: Counting objects: 100% (9592/9592), done.
remote: Compressing objects: 100% (2461/2461), done.
remote: Total 9592 (delta 7013), reused 9578 (delta 6999), pack-reused 0
Receiving objects: 100% (9592/9592), 5.51 MiB | 10.62 MiB/s, done.
Resolving deltas: 100% (7013/7013), done.
Already on 'master'
Your branch is up to date with 'origin/master'.
[  76.567] Cloning pythondata-cpu-cva5 Git repository...
Cloning into 'pythondata-cpu-cva5'...
remote: Enumerating objects: 3992, done.
remote: Counting objects: 100% (3992/3992), done.
remote: Compressing objects: 100% (825/825), done.
remote: Total 3992 (delta 3118), reused 3977 (delta 3103), pack-reused 0
Receiving objects: 100% (3992/3992), 1.29 MiB | 5.24 MiB/s, done.
Resolving deltas: 100% (3118/3118), done.
Already on 'master'
Your branch is up to date with 'origin/master'.
[  77.723] Cloning pythondata-cpu-cva6 Git repository...
Cloning into 'pythondata-cpu-cva6'...
remote: Enumerating objects: 16201, done.
remote: Counting objects: 100% (1430/1430), done.
remote: Compressing objects: 100% (1027/1027), done.
remote: Total 16201 (delta 473), reused 1249 (delta 352), pack-reused 14771
Receiving objects: 100% (16201/16201), 37.01 MiB | 17.91 MiB/s, done.
Resolving deltas: 100% (11266/11266), done.
Submodule 'pythondata_cpu_cva6/system_verilog/common/submodules/common_cells' (https://github.com/pulp-platform/common_cells.git) registered for path 'pythondata_cpu_cva6/system_verilog/common/submodules/common_cells'
Submodule 'pythondata_cpu_cva6/system_verilog/core/fpu' (https://github.com/pulp-platform/fpnew.git) registered for path 'pythondata_cpu_cva6/system_verilog/core/fpu'
Submodule 'pythondata_cpu_cva6/system_verilog/corev_apu/axi' (https://github.com/pulp-platform/axi.git) registered for path 'pythondata_cpu_cva6/system_verilog/corev_apu/axi'
Submodule 'pythondata_cpu_cva6/system_verilog/corev_apu/axi_mem_if' (https://github.com/pulp-platform/axi_mem_if.git) registered for path 'pythondata_cpu_cva6/system_verilog/corev_apu/axi_mem_if'
Submodule 'pythondata_cpu_cva6/system_verilog/corev_apu/fpga/src/apb_node' (https://github.com/pulp-platform/apb_node.git) registered for path 'pythondata_cpu_cva6/system_verilog/corev_apu/fpga/src/apb_node'
Submodule 'pythondata_cpu_cva6/system_verilog/corev_apu/fpga/src/apb_timer' (https://github.com/pulp-platform/apb_timer.git) registered for path 'pythondata_cpu_cva6/system_verilog/corev_apu/fpga/src/apb_timer'
Submodule 'pythondata_cpu_cva6/system_verilog/corev_apu/fpga/src/apb_uart' (https://github.com/pulp-platform/apb_uart.git) registered for path 'pythondata_cpu_cva6/system_verilog/corev_apu/fpga/src/apb_uart'
Submodule 'pythondata_cpu_cva6/system_verilog/corev_apu/fpga/src/ariane-ethernet' (https://github.com/lowRISC/ariane-ethernet.git) registered for path 'pythondata_cpu_cva6/system_verilog/corev_apu/fpga/src/ariane-ethernet'
Submodule 'pythondata_cpu_cva6/system_verilog/corev_apu/fpga/src/axi2apb' (https://github.com/pulp-platform/axi2apb.git) registered for path 'pythondata_cpu_cva6/system_verilog/corev_apu/fpga/src/axi2apb'
Submodule 'pythondata_cpu_cva6/system_verilog/corev_apu/fpga/src/axi_slice' (https://github.com/pulp-platform/axi_slice.git) registered for path 'pythondata_cpu_cva6/system_verilog/corev_apu/fpga/src/axi_slice'
Submodule 'pythondata_cpu_cva6/system_verilog/corev_apu/register_interface' (https://github.com/pulp-platform/register_interface.git) registered for path 'pythondata_cpu_cva6/system_verilog/corev_apu/register_interface'
Submodule 'pythondata_cpu_cva6/system_verilog/corev_apu/riscv-dbg' (https://github.com/pulp-platform/riscv-dbg.git) registered for path 'pythondata_cpu_cva6/system_verilog/corev_apu/riscv-dbg'
Submodule 'pythondata_cpu_cva6/system_verilog/corev_apu/rv_plic' (https://github.com/pulp-platform/rv_plic.git) registered for path 'pythondata_cpu_cva6/system_verilog/corev_apu/rv_plic'
Submodule 'pythondata_cpu_cva6/system_verilog/corev_apu/src/axi_riscv_atomics' (https://github.com/pulp-platform/axi_riscv_atomics.git) registered for path 'pythondata_cpu_cva6/system_verilog/corev_apu/src/axi_riscv_atomics'
Submodule 'pythondata_cpu_cva6/system_verilog/corev_apu/src/tech_cells_generic' (https://github.com/pulp-platform/tech_cells_generic.git) registered for path 'pythondata_cpu_cva6/system_verilog/corev_apu/src/tech_cells_generic'
Submodule 'pythondata_cpu_cva6/system_verilog/corev_apu/tb/common_verification' (https://github.com/pulp-platform/common_verification.git) registered for path 'pythondata_cpu_cva6/system_verilog/corev_apu/tb/common_verification'
Submodule 'pythondata_cpu_cva6/system_verilog/corev_apu/tb/dromajo' (https://github.com/kabylkas/dromajo.git) registered for path 'pythondata_cpu_cva6/system_verilog/corev_apu/tb/dromajo'
Cloning into '/home/kevin/pythondata-cpu-cva6/pythondata_cpu_cva6/system_verilog/common/submodules/common_cells'...
remote: Enumerating objects: 2709, done.
remote: Counting objects: 100% (577/577), done.
remote: Compressing objects: 100% (223/223), done.
remote: Total 2709 (delta 437), reused 421 (delta 353), pack-reused 2132
Receiving objects: 100% (2709/2709), 762.56 KiB | 4.17 MiB/s, done.
Resolving deltas: 100% (1836/1836), done.
Cloning into '/home/kevin/pythondata-cpu-cva6/pythondata_cpu_cva6/system_verilog/core/fpu'...
remote: Enumerating objects: 2141, done.
remote: Counting objects: 100% (457/457), done.
remote: Compressing objects: 100% (134/134), done.
remote: Total 2141 (delta 364), reused 375 (delta 317), pack-reused 1684
Receiving objects: 100% (2141/2141), 6.60 MiB | 12.42 MiB/s, done.
Resolving deltas: 100% (1507/1507), done.
Cloning into '/home/kevin/pythondata-cpu-cva6/pythondata_cpu_cva6/system_verilog/corev_apu/axi'...
remote: Enumerating objects: 10145, done.
remote: Counting objects: 100% (1813/1813), done.
remote: Compressing objects: 100% (223/223), done.
remote: Total 10145 (delta 1672), reused 1647 (delta 1587), pack-reused 8332
Receiving objects: 100% (10145/10145), 6.03 MiB | 14.15 MiB/s, done.
Resolving deltas: 100% (7404/7404), done.
Cloning into '/home/kevin/pythondata-cpu-cva6/pythondata_cpu_cva6/system_verilog/corev_apu/axi_mem_if'...
remote: Enumerating objects: 164, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 164 (delta 0), reused 1 (delta 0), pack-reused 160
Receiving objects: 100% (164/164), 67.12 KiB | 1.32 MiB/s, done.
Resolving deltas: 100% (79/79), done.
Cloning into '/home/kevin/pythondata-cpu-cva6/pythondata_cpu_cva6/system_verilog/corev_apu/fpga/src/apb_node'...
remote: Enumerating objects: 80, done.
remote: Counting objects: 100% (7/7), done.
remote: Compressing objects: 100% (6/6), done.
remote: Total 80 (delta 1), reused 5 (delta 1), pack-reused 73
Cloning into '/home/kevin/pythondata-cpu-cva6/pythondata_cpu_cva6/system_verilog/corev_apu/fpga/src/apb_timer'...
remote: Enumerating objects: 74, done.
remote: Counting objects: 100% (10/10), done.
remote: Compressing objects: 100% (9/9), done.
remote: Total 74 (delta 1), reused 7 (delta 1), pack-reused 64
Cloning into '/home/kevin/pythondata-cpu-cva6/pythondata_cpu_cva6/system_verilog/corev_apu/fpga/src/apb_uart'...
remote: Enumerating objects: 106, done.
remote: Counting objects: 100% (51/51), done.
remote: Compressing objects: 100% (37/37), done.
remote: Total 106 (delta 25), reused 32 (delta 13), pack-reused 55
Receiving objects: 100% (106/106), 63.37 KiB | 1.29 MiB/s, done.
Resolving deltas: 100% (54/54), done.
Cloning into '/home/kevin/pythondata-cpu-cva6/pythondata_cpu_cva6/system_verilog/corev_apu/fpga/src/ariane-ethernet'...
remote: Enumerating objects: 103, done.
remote: Total 103 (delta 0), reused 0 (delta 0), pack-reused 103
Receiving objects: 100% (103/103), 44.16 KiB | 1.03 MiB/s, done.
Resolving deltas: 100% (65/65), done.
Cloning into '/home/kevin/pythondata-cpu-cva6/pythondata_cpu_cva6/system_verilog/corev_apu/fpga/src/axi2apb'...
remote: Enumerating objects: 223, done.
remote: Total 223 (delta 0), reused 0 (delta 0), pack-reused 223
Receiving objects: 100% (223/223), 77.72 KiB | 1.49 MiB/s, done.
Resolving deltas: 100% (131/131), done.
Cloning into '/home/kevin/pythondata-cpu-cva6/pythondata_cpu_cva6/system_verilog/corev_apu/fpga/src/axi_slice'...
remote: Enumerating objects: 147, done.
remote: Total 147 (delta 0), reused 0 (delta 0), pack-reused 147
Receiving objects: 100% (147/147), 44.89 KiB | 581.00 KiB/s, done.
Resolving deltas: 100% (86/86), done.
Cloning into '/home/kevin/pythondata-cpu-cva6/pythondata_cpu_cva6/system_verilog/corev_apu/register_interface'...
remote: Enumerating objects: 776, done.
remote: Counting objects: 100% (272/272), done.
remote: Compressing objects: 100% (159/159), done.
remote: Total 776 (delta 132), reused 195 (delta 101), pack-reused 504
Receiving objects: 100% (776/776), 468.93 KiB | 2.66 MiB/s, done.
Resolving deltas: 100% (385/385), done.
Cloning into '/home/kevin/pythondata-cpu-cva6/pythondata_cpu_cva6/system_verilog/corev_apu/riscv-dbg'...
remote: Enumerating objects: 1377, done.
remote: Counting objects: 100% (360/360), done.
remote: Compressing objects: 100% (113/113), done.
remote: Total 1377 (delta 279), reused 249 (delta 247), pack-reused 1017
Receiving objects: 100% (1377/1377), 457.27 KiB | 1.47 MiB/s, done.
Resolving deltas: 100% (903/903), done.
Cloning into '/home/kevin/pythondata-cpu-cva6/pythondata_cpu_cva6/system_verilog/corev_apu/rv_plic'...
remote: Enumerating objects: 38, done.
remote: Counting objects: 100% (21/21), done.
remote: Compressing objects: 100% (15/15), done.
remote: Total 38 (delta 12), reused 6 (delta 6), pack-reused 17
Cloning into '/home/kevin/pythondata-cpu-cva6/pythondata_cpu_cva6/system_verilog/corev_apu/src/axi_riscv_atomics'...
remote: Enumerating objects: 652, done.
remote: Counting objects: 100% (86/86), done.
remote: Compressing objects: 100% (26/26), done.
remote: Total 652 (delta 73), reused 63 (delta 60), pack-reused 566
Receiving objects: 100% (652/652), 284.49 KiB | 2.09 MiB/s, done.
Resolving deltas: 100% (444/444), done.
Cloning into '/home/kevin/pythondata-cpu-cva6/pythondata_cpu_cva6/system_verilog/corev_apu/src/tech_cells_generic'...
remote: Enumerating objects: 525, done.
remote: Counting objects: 100% (198/198), done.
remote: Compressing objects: 100% (117/117), done.
remote: Total 525 (delta 100), reused 162 (delta 81), pack-reused 327
Receiving objects: 100% (525/525), 110.99 KiB | 1.39 MiB/s, done.
Resolving deltas: 100% (307/307), done.
Cloning into '/home/kevin/pythondata-cpu-cva6/pythondata_cpu_cva6/system_verilog/corev_apu/tb/common_verification'...
remote: Enumerating objects: 209, done.
remote: Counting objects: 100% (93/93), done.
remote: Compressing objects: 100% (63/63), done.
remote: Total 209 (delta 50), reused 55 (delta 24), pack-reused 116
Receiving objects: 100% (209/209), 55.34 KiB | 1.32 MiB/s, done.
Resolving deltas: 100% (112/112), done.
Cloning into '/home/kevin/pythondata-cpu-cva6/pythondata_cpu_cva6/system_verilog/corev_apu/tb/dromajo'...
remote: Enumerating objects: 2066, done.
remote: Counting objects: 100% (713/713), done.
remote: Compressing objects: 100% (45/45), done.
remote: Total 2066 (delta 675), reused 671 (delta 668), pack-reused 1353
Receiving objects: 100% (2066/2066), 1.91 MiB | 7.01 MiB/s, done.
Resolving deltas: 100% (1480/1480), done.
Submodule path 'pythondata_cpu_cva6/system_verilog/common/submodules/common_cells': checked out 'dc555643226419b7a602f0aa39d449545ea4c1f2'
Submodule path 'pythondata_cpu_cva6/system_verilog/core/fpu': checked out '79f75e0a0fdab6ebc3840a14077c39f4934321fe'
Submodule 'src-sv/common_cells' (https://github.com/pulp-platform/common_cells.git) registered for path 'pythondata_cpu_cva6/system_verilog/core/fpu/src/common_cells'
Submodule 'src-sv/fpu_div_sqrt_mvp' (https://github.com/pulp-platform/fpu_div_sqrt_mvp.git) registered for path 'pythondata_cpu_cva6/system_verilog/core/fpu/src/fpu_div_sqrt_mvp'
Submodule 'tb/flexfloat' (https://github.com/oprecomp/flexfloat.git) registered for path 'pythondata_cpu_cva6/system_verilog/core/fpu/tb/flexfloat'
Cloning into '/home/kevin/pythondata-cpu-cva6/pythondata_cpu_cva6/system_verilog/core/fpu/src/common_cells'...
remote: Enumerating objects: 2709, done.
remote: Counting objects: 100% (564/564), done.
remote: Compressing objects: 100% (217/217), done.
remote: Total 2709 (delta 426), reused 414 (delta 346), pack-reused 2145
Receiving objects: 100% (2709/2709), 763.46 KiB | 3.96 MiB/s, done.
Resolving deltas: 100% (1836/1836), done.
Cloning into '/home/kevin/pythondata-cpu-cva6/pythondata_cpu_cva6/system_verilog/core/fpu/src/fpu_div_sqrt_mvp'...
remote: Enumerating objects: 210, done.
remote: Counting objects: 100% (18/18), done.
remote: Compressing objects: 100% (15/15), done.
remote: Total 210 (delta 6), reused 10 (delta 3), pack-reused 192
Receiving objects: 100% (210/210), 775.64 KiB | 2.28 MiB/s, done.
Resolving deltas: 100% (127/127), done.
Cloning into '/home/kevin/pythondata-cpu-cva6/pythondata_cpu_cva6/system_verilog/core/fpu/tb/flexfloat'...
remote: Enumerating objects: 206, done.
remote: Counting objects: 100% (63/63), done.
remote: Compressing objects: 100% (38/38), done.
remote: Total 206 (delta 25), reused 41 (delta 16), pack-reused 143
Receiving objects: 100% (206/206), 88.67 KiB | 1.11 MiB/s, done.
Resolving deltas: 100% (90/90), done.
Submodule path 'pythondata_cpu_cva6/system_verilog/core/fpu/src/common_cells': checked out '790f2385c01c83022474eede55809666209216e3'
Submodule path 'pythondata_cpu_cva6/system_verilog/core/fpu/src/fpu_div_sqrt_mvp': checked out '83a601f97934ed5e06d737b9c80d98b08867c5fa'
Submodule path 'pythondata_cpu_cva6/system_verilog/core/fpu/tb/flexfloat': checked out '28be2d4fbf41b38fc37763bb6e90a1c88f6aaa61'
Submodule path 'pythondata_cpu_cva6/system_verilog/corev_apu/axi': checked out '697f13ff67153a5243e347f2d1992a125018b6c2'
Submodule path 'pythondata_cpu_cva6/system_verilog/corev_apu/axi_mem_if': checked out 'b494701501886ad71ba0c128560cc371610bcf1a'
Submodule path 'pythondata_cpu_cva6/system_verilog/corev_apu/fpga/src/apb_node': checked out '157e5f00a37440d53f2e5b3aabfc9d454530e688'
Submodule path 'pythondata_cpu_cva6/system_verilog/corev_apu/fpga/src/apb_timer': checked out '6c84f69d2e92bd766f609b5dd47ece723359bd24'
Submodule path 'pythondata_cpu_cva6/system_verilog/corev_apu/fpga/src/apb_uart': checked out 'ac3461ce23832e02903b9d2d7d4edd7fcb89bd92'
Submodule path 'pythondata_cpu_cva6/system_verilog/corev_apu/fpga/src/ariane-ethernet': checked out '6a5436bf110f83ebb13119dbd82650ccd8f947c9'
Submodule path 'pythondata_cpu_cva6/system_verilog/corev_apu/fpga/src/axi2apb': checked out '53e7b9f1b16e3f4d4aadc8fbf880d05879f54fe8'
Submodule path 'pythondata_cpu_cva6/system_verilog/corev_apu/fpga/src/axi_slice': checked out 'aae8ca49dcfbfa8e44e1938a2e4a768db83006cb'
Submodule path 'pythondata_cpu_cva6/system_verilog/corev_apu/register_interface': checked out '73de8e51b79f416350229b1d2420b2c527e002b8'
Submodule path 'pythondata_cpu_cva6/system_verilog/corev_apu/riscv-dbg': checked out 'e19d69efe7d7e4da6c25ed91d5e7f501ab52dd68'
Submodule path 'pythondata_cpu_cva6/system_verilog/corev_apu/rv_plic': checked out '5b5c5a4c1c15c3d7bb833071d344b2c2bc5f599d'
Submodule path 'pythondata_cpu_cva6/system_verilog/corev_apu/src/axi_riscv_atomics': checked out '550881f12e22dfae405612fc1df6368f4c003e68'
Submodule path 'pythondata_cpu_cva6/system_verilog/corev_apu/src/tech_cells_generic': checked out 'b2a68114302af1d8191ddf34ea0e07b471911866'
Submodule path 'pythondata_cpu_cva6/system_verilog/corev_apu/tb/common_verification': checked out 'a1e569119cdf2d25cecceee4016acd98030f6886'
Submodule path 'pythondata_cpu_cva6/system_verilog/corev_apu/tb/dromajo': checked out '8acade8725d5e6cbf373304b348a8d77e0a5c713'
Already on 'master'
Your branch is up to date with 'origin/master'.
[ 102.561] Cloning pythondata-cpu-ibex Git repository...
Cloning into 'pythondata-cpu-ibex'...
remote: Enumerating objects: 24806, done.
remote: Counting objects: 100% (1333/1333), done.
remote: Compressing objects: 100% (760/760), done.
remote: Total 24806 (delta 815), reused 929 (delta 555), pack-reused 23473
Receiving objects: 100% (24806/24806), 11.27 MiB | 10.36 MiB/s, done.
Resolving deltas: 100% (17695/17695), done.
Already on 'master'
Your branch is up to date with 'origin/master'.
Note: switching to 'd3d53df'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at d3d53df6 Merge commit 'e70add7228dc9b82c724078475e44e467808175d'
[ 105.496] Cloning pythondata-cpu-minerva Git repository...
Cloning into 'pythondata-cpu-minerva'...
remote: Enumerating objects: 1054, done.
remote: Counting objects: 100% (1054/1054), done.
remote: Compressing objects: 100% (376/376), done.
remote: Total 1054 (delta 713), reused 998 (delta 657), pack-reused 0
Receiving objects: 100% (1054/1054), 212.50 KiB | 1.74 MiB/s, done.
Resolving deltas: 100% (713/713), done.
Already on 'master'
Your branch is up to date with 'origin/master'.
[ 106.496] Cloning pythondata-cpu-naxriscv Git repository...
Cloning into 'pythondata-cpu-naxriscv'...
remote: Enumerating objects: 121, done.
remote: Counting objects: 100% (121/121), done.
remote: Compressing objects: 100% (72/72), done.
remote: Total 121 (delta 61), reused 99 (delta 43), pack-reused 0
Receiving objects: 100% (121/121), 16.09 KiB | 5.36 MiB/s, done.
Resolving deltas: 100% (61/61), done.
Already on 'master'
Your branch is up to date with 'origin/master'.
[ 107.289] Cloning pythondata-cpu-picorv32 Git repository...
Cloning into 'pythondata-cpu-picorv32'...
remote: Enumerating objects: 3257, done.
remote: Counting objects: 100% (476/476), done.
remote: Compressing objects: 100% (200/200), done.
remote: Total 3257 (delta 271), reused 463 (delta 258), pack-reused 2781
Receiving objects: 100% (3257/3257), 970.37 KiB | 4.51 MiB/s, done.
Resolving deltas: 100% (2059/2059), done.
Already on 'master'
Your branch is up to date with 'origin/master'.
[ 108.417] Cloning pythondata-cpu-rocket Git repository...
Cloning into 'pythondata-cpu-rocket'...
remote: Enumerating objects: 1396, done.
remote: Counting objects: 100% (603/603), done.
remote: Compressing objects: 100% (87/87), done.
remote: Total 1396 (delta 530), reused 578 (delta 510), pack-reused 793
Receiving objects: 100% (1396/1396), 118.15 MiB | 9.76 MiB/s, done.
Resolving deltas: 100% (1035/1035), done.
Updating files: 100% (1051/1051), done.
Already on 'master'
Your branch is up to date with 'origin/master'.
[ 146.680] Cloning pythondata-cpu-serv Git repository...
Cloning into 'pythondata-cpu-serv'...
remote: Enumerating objects: 2905, done.
remote: Counting objects: 100% (199/199), done.
remote: Compressing objects: 100% (144/144), done.
remote: Total 2905 (delta 93), reused 140 (delta 51), pack-reused 2706
Receiving objects: 100% (2905/2905), 1.99 MiB | 7.83 MiB/s, done.
Resolving deltas: 100% (1802/1802), done.
Already on 'master'
Your branch is up to date with 'origin/master'.
[ 147.806] Cloning pythondata-cpu-vexriscv Git repository...
Cloning into 'pythondata-cpu-vexriscv'...
remote: Enumerating objects: 1051, done.
remote: Counting objects: 100% (485/485), done.
remote: Compressing objects: 100% (90/90), done.
remote: Total 1051 (delta 411), reused 427 (delta 377), pack-reused 566
Receiving objects: 100% (1051/1051), 2.65 MiB | 9.59 MiB/s, done.
Resolving deltas: 100% (540/540), done.
Already on 'master'
Your branch is up to date with 'origin/master'.
[ 149.290] Cloning pythondata-cpu-vexriscv-smp Git repository...
Cloning into 'pythondata-cpu-vexriscv-smp'...
remote: Enumerating objects: 301, done.
remote: Counting objects: 100% (212/212), done.
remote: Compressing objects: 100% (14/14), done.
remote: Total 301 (delta 207), reused 198 (delta 198), pack-reused 89
Receiving objects: 100% (301/301), 4.53 MiB | 8.96 MiB/s, done.
Resolving deltas: 100% (212/212), done.
Submodule 'pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL' (https://github.com/SpinalHDL/SpinalHDL.git) registered for path 'pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL'
Submodule 'pythondata_cpu_vexriscv_smp/verilog/ext/VexRiscv' (https://github.com/SpinalHDL/VexRiscv.git) registered for path 'pythondata_cpu_vexriscv_smp/verilog/ext/VexRiscv'
Cloning into '/home/kevin/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL'...
remote: Enumerating objects: 86418, done.
remote: Counting objects: 100% (2325/2325), done.
remote: Compressing objects: 100% (618/618), done.
remote: Total 86418 (delta 1606), reused 2214 (delta 1517), pack-reused 84093
Receiving objects: 100% (86418/86418), 34.80 MiB | 14.90 MiB/s, done.
Resolving deltas: 100% (39176/39176), done.
Cloning into '/home/kevin/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/VexRiscv'...
remote: Enumerating objects: 15847, done.
remote: Counting objects: 100% (5377/5377), done.
remote: Compressing objects: 100% (1673/1673), done.
remote: Total 15847 (delta 3808), reused 4183 (delta 3686), pack-reused 10470
Receiving objects: 100% (15847/15847), 12.89 MiB | 16.31 MiB/s, done.
Resolving deltas: 100% (9489/9489), done.
Submodule path 'pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL': checked out '4fd59f09e99b2a3a9e2d5fa00fdad9a536652ae2'
Submodule 'tester/src/test/python/cocotblib' (https://github.com/SpinalHDL/CocotbLib.git) registered for path 'pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/tester/src/test/python/cocotblib'
Cloning into '/home/kevin/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/tester/src/test/python/cocotblib'...
remote: Enumerating objects: 124, done.
remote: Counting objects: 100% (15/15), done.
remote: Compressing objects: 100% (12/12), done.
remote: Total 124 (delta 4), reused 9 (delta 3), pack-reused 109
Receiving objects: 100% (124/124), 36.77 KiB | 875.00 KiB/s, done.
Resolving deltas: 100% (64/64), done.
Submodule path 'pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/tester/src/test/python/cocotblib': checked out 'a98830423924fc89bfebae84cb802fc90d352602'
Submodule path 'pythondata_cpu_vexriscv_smp/verilog/ext/VexRiscv': checked out 'd7e9c726c36c66caf0f6bc4c15ffc659f27c237f'
Submodule 'src/test/resources/VexRiscvRegressionData' (https://github.com/SpinalHDL/VexRiscvRegressionData.git) registered for path 'pythondata_cpu_vexriscv_smp/verilog/ext/VexRiscv/src/test/resources/VexRiscvRegressionData'
Cloning into '/home/kevin/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/VexRiscv/src/test/resources/VexRiscvRegressionData'...
remote: Enumerating objects: 78, done.
remote: Total 78 (delta 0), reused 0 (delta 0), pack-reused 78
Submodule path 'pythondata_cpu_vexriscv_smp/verilog/ext/VexRiscv/src/test/resources/VexRiscvRegressionData': checked out '539398c1481203a51115b5f1228ea961f0ac9bd3'
Already on 'master'
Your branch is up to date with 'origin/master'.
[ 164.310] Installing Git repositories...
[ 164.310] ------------------------------
[ 164.310] Installing migen Git repository...
Obtaining file:///home/kevin/migen
Requirement already satisfied: colorama in /usr/lib/python3/dist-packages (from migen==0.9.2) (0.4.3)
Installing collected packages: migen
  Attempting uninstall: migen
    Found existing installation: migen 0.9.2
    Can't uninstall 'migen'. No files were found to uninstall.
  Running setup.py develop for migen
Successfully installed migen
[ 166.560] Installing pythondata-software-picolibc Git repository...
Obtaining file:///home/kevin/pythondata-software-picolibc
Installing collected packages: pythondata-software-picolibc
  Attempting uninstall: pythondata-software-picolibc
    Found existing installation: pythondata-software-picolibc 1.7.9.post181
    Can't uninstall 'pythondata-software-picolibc'. No files were found to uninstall.
  Running setup.py develop for pythondata-software-picolibc
Successfully installed pythondata-software-picolibc
[ 168.966] Installing pythondata-software-compiler_rt Git repository...
Obtaining file:///home/kevin/pythondata-software-compiler_rt
Installing collected packages: pythondata-software-compiler-rt
  Attempting uninstall: pythondata-software-compiler-rt
    Found existing installation: pythondata-software-compiler-rt 0.0.post6206
    Can't uninstall 'pythondata-software-compiler-rt'. No files were found to uninstall.
  Running setup.py develop for pythondata-software-compiler-rt
Successfully installed pythondata-software-compiler-rt
[ 171.362] Installing litex Git repository...
Obtaining file:///home/kevin/litex
Requirement already satisfied: migen in /home/kevin/migen (from litex==2022.12) (0.9.2)
Collecting packaging
  Downloading packaging-23.1-py3-none-any.whl (48 kB)
     |████████████████████████████████| 48 kB 538 kB/s
Collecting pyserial
  Downloading pyserial-3.5-py2.py3-none-any.whl (90 kB)
     |████████████████████████████████| 90 kB 1.6 MB/s
Requirement already satisfied: requests in /usr/lib/python3/dist-packages (from litex==2022.12) (2.22.0)
Requirement already satisfied: colorama in /usr/lib/python3/dist-packages (from migen->litex==2022.12) (0.4.3)
Installing collected packages: packaging, pyserial, litex
  Running setup.py develop for litex
Successfully installed litex packaging-23.1 pyserial-3.5
[ 174.895] Installing liteeth Git repository...
Obtaining file:///home/kevin/liteeth
Collecting liteiclink
  Downloading liteiclink-2022.12.tar.gz (71 kB)
     |████████████████████████████████| 71 kB 1.1 MB/s
Requirement already satisfied: litex in /home/kevin/litex (from liteeth==2022.12) (2022.12)
Requirement already satisfied: pyyaml in /usr/lib/python3/dist-packages (from liteeth==2022.12) (5.3.1)
Requirement already satisfied: migen in /home/kevin/migen (from litex->liteeth==2022.12) (0.9.2)
Requirement already satisfied: packaging in /home/kevin/.local/lib/python3.8/site-packages (from litex->liteeth==2022.12) (23.1)
Requirement already satisfied: pyserial in /home/kevin/.local/lib/python3.8/site-packages (from litex->liteeth==2022.12) (3.5)
Requirement already satisfied: requests in /usr/lib/python3/dist-packages (from litex->liteeth==2022.12) (2.22.0)
Requirement already satisfied: colorama in /usr/lib/python3/dist-packages (from migen->litex->liteeth==2022.12) (0.4.3)
Building wheels for collected packages: liteiclink
  Building wheel for liteiclink (setup.py) ... done
  Created wheel for liteiclink: filename=liteiclink-2022.12-py3-none-any.whl size=80693 sha256=3c93f412c6a874476631f85c06663ad689415e91e34b46192e48d229ba6bf755
  Stored in directory: /home/kevin/.cache/pip/wheels/4c/0f/07/09db0dda82c183a57f4e0d27bb833d4a0c5da5e6432c66800c
Successfully built liteiclink
Installing collected packages: liteiclink, liteeth
  Running setup.py develop for liteeth
Successfully installed liteeth liteiclink-2022.12
[ 178.691] Installing litedram Git repository...
Obtaining file:///home/kevin/litedram
Requirement already satisfied: litex in /home/kevin/litex (from litedram==2022.12) (2022.12)
Requirement already satisfied: pyyaml in /usr/lib/python3/dist-packages (from litedram==2022.12) (5.3.1)
Requirement already satisfied: migen in /home/kevin/migen (from litex->litedram==2022.12) (0.9.2)
Requirement already satisfied: packaging in /home/kevin/.local/lib/python3.8/site-packages (from litex->litedram==2022.12) (23.1)
Requirement already satisfied: pyserial in /home/kevin/.local/lib/python3.8/site-packages (from litex->litedram==2022.12) (3.5)
Requirement already satisfied: requests in /usr/lib/python3/dist-packages (from litex->litedram==2022.12) (2.22.0)
Requirement already satisfied: colorama in /usr/lib/python3/dist-packages (from migen->litex->litedram==2022.12) (0.4.3)
Installing collected packages: litedram
  Attempting uninstall: litedram
    Found existing installation: litedram 2022.12
    Can't uninstall 'litedram'. No files were found to uninstall.
  Running setup.py develop for litedram
Successfully installed litedram
[ 180.969] Installing litepcie Git repository...
Obtaining file:///home/kevin/litepcie
Requirement already satisfied: litex in /home/kevin/litex (from litepcie==2022.12) (2022.12)
Requirement already satisfied: pyyaml in /usr/lib/python3/dist-packages (from litepcie==2022.12) (5.3.1)
Requirement already satisfied: migen in /home/kevin/migen (from litex->litepcie==2022.12) (0.9.2)
Requirement already satisfied: packaging in /home/kevin/.local/lib/python3.8/site-packages (from litex->litepcie==2022.12) (23.1)
Requirement already satisfied: pyserial in /home/kevin/.local/lib/python3.8/site-packages (from litex->litepcie==2022.12) (3.5)
Requirement already satisfied: requests in /usr/lib/python3/dist-packages (from litex->litepcie==2022.12) (2.22.0)
Requirement already satisfied: colorama in /usr/lib/python3/dist-packages (from migen->litex->litepcie==2022.12) (0.4.3)
Installing collected packages: litepcie
  Attempting uninstall: litepcie
    Found existing installation: litepcie 2022.12
    Can't uninstall 'litepcie'. No files were found to uninstall.
  Running setup.py develop for litepcie
Successfully installed litepcie
[ 183.400] Installing litesata Git repository...
Obtaining file:///home/kevin/litesata
Installing collected packages: litesata
  Attempting uninstall: litesata
    Found existing installation: litesata 0.0.0
    Can't uninstall 'litesata'. No files were found to uninstall.
  Running setup.py develop for litesata
Successfully installed litesata
[ 185.712] Installing litesdcard Git repository...
Obtaining file:///home/kevin/litesdcard
Installing collected packages: litesdcard
  Attempting uninstall: litesdcard
    Found existing installation: litesdcard 0.0.0
    Can't uninstall 'litesdcard'. No files were found to uninstall.
  Running setup.py develop for litesdcard
Successfully installed litesdcard
[ 187.993] Installing liteiclink Git repository...
Obtaining file:///home/kevin/liteiclink
Requirement already satisfied: litex in /home/kevin/litex (from liteiclink==2022.12) (2022.12)
Requirement already satisfied: pyyaml in /usr/lib/python3/dist-packages (from liteiclink==2022.12) (5.3.1)
Requirement already satisfied: migen in /home/kevin/migen (from litex->liteiclink==2022.12) (0.9.2)
Requirement already satisfied: packaging in /home/kevin/.local/lib/python3.8/site-packages (from litex->liteiclink==2022.12) (23.1)
Requirement already satisfied: pyserial in /home/kevin/.local/lib/python3.8/site-packages (from litex->liteiclink==2022.12) (3.5)
Requirement already satisfied: requests in /usr/lib/python3/dist-packages (from litex->liteiclink==2022.12) (2.22.0)
Requirement already satisfied: colorama in /usr/lib/python3/dist-packages (from migen->litex->liteiclink==2022.12) (0.4.3)
Installing collected packages: liteiclink
  Attempting uninstall: liteiclink
    Found existing installation: liteiclink 2022.12
    Uninstalling liteiclink-2022.12:
      Successfully uninstalled liteiclink-2022.12
  Running setup.py develop for liteiclink
Successfully installed liteiclink
[ 190.266] Installing litescope Git repository...
Obtaining file:///home/kevin/litescope
Installing collected packages: litescope
  Attempting uninstall: litescope
    Found existing installation: litescope 0.0.0
    Can't uninstall 'litescope'. No files were found to uninstall.
  Running setup.py develop for litescope
Successfully installed litescope
[ 192.548] Installing litejesd204b Git repository...
Obtaining file:///home/kevin/litejesd204b
Installing collected packages: litejesd204b
  Attempting uninstall: litejesd204b
    Found existing installation: litejesd204b 0.0.0
    Can't uninstall 'litejesd204b'. No files were found to uninstall.
  Running setup.py develop for litejesd204b
Successfully installed litejesd204b
[ 194.908] Installing litespi Git repository...
Obtaining file:///home/kevin/litespi
Installing collected packages: litespi
  Attempting uninstall: litespi
    Found existing installation: litespi 0.0.0
    Can't uninstall 'litespi'. No files were found to uninstall.
  Running setup.py develop for litespi
Successfully installed litespi
[ 197.192] Installing valentyusb Git repository...
Obtaining file:///home/kevin/valentyusb
Installing collected packages: valentyusb
  Attempting uninstall: valentyusb
    Found existing installation: valentyusb 0.0.0
    Can't uninstall 'valentyusb'. No files were found to uninstall.
  Running setup.py develop for valentyusb
Successfully installed valentyusb
[ 199.544] Installing litex-boards Git repository...
Obtaining file:///home/kevin/litex-boards
Installing collected packages: litex-boards
  Attempting uninstall: litex-boards
    Found existing installation: litex-boards 0.0.0
    Can't uninstall 'litex-boards'. No files were found to uninstall.
  Running setup.py develop for litex-boards
Successfully installed litex-boards
[ 201.889] Installing pythondata-misc-tapcfg Git repository...
Obtaining file:///home/kevin/pythondata-misc-tapcfg
Installing collected packages: pythondata-misc-tapcfg
  Attempting uninstall: pythondata-misc-tapcfg
    Found existing installation: pythondata-misc-tapcfg 0.0.post517
    Can't uninstall 'pythondata-misc-tapcfg'. No files were found to uninstall.
  Running setup.py develop for pythondata-misc-tapcfg
Successfully installed pythondata-misc-tapcfg
[ 204.218] Installing pythondata-misc-usb_ohci Git repository...
Obtaining file:///home/kevin/pythondata-misc-usb_ohci
Installing collected packages: pythondata-misc-usb-ohci
  Attempting uninstall: pythondata-misc-usb-ohci
    Found existing installation: pythondata-misc-usb-ohci 1.0.1.post325
    Can't uninstall 'pythondata-misc-usb-ohci'. No files were found to uninstall.
  Running setup.py develop for pythondata-misc-usb-ohci
Successfully installed pythondata-misc-usb-ohci
[ 206.544] Installing pythondata-cpu-lm32 Git repository...
Obtaining file:///home/kevin/pythondata-cpu-lm32
Installing collected packages: pythondata-cpu-lm32
  Attempting uninstall: pythondata-cpu-lm32
    Found existing installation: pythondata-cpu-lm32 0.0.post199
    Can't uninstall 'pythondata-cpu-lm32'. No files were found to uninstall.
  Running setup.py develop for pythondata-cpu-lm32
Successfully installed pythondata-cpu-lm32
[ 208.941] Installing pythondata-cpu-mor1kx Git repository...
Obtaining file:///home/kevin/pythondata-cpu-mor1kx
Installing collected packages: pythondata-cpu-mor1kx
  Attempting uninstall: pythondata-cpu-mor1kx
    Found existing installation: pythondata-cpu-mor1kx 5.1.1.post142
    Can't uninstall 'pythondata-cpu-mor1kx'. No files were found to uninstall.
  Running setup.py develop for pythondata-cpu-mor1kx
Successfully installed pythondata-cpu-mor1kx
[ 211.316] Installing pythondata-cpu-marocchino Git repository...
Obtaining file:///home/kevin/pythondata-cpu-marocchino
Installing collected packages: pythondata-cpu-marocchino
  Attempting uninstall: pythondata-cpu-marocchino
    Found existing installation: pythondata-cpu-marocchino 0.0.post209
    Can't uninstall 'pythondata-cpu-marocchino'. No files were found to uninstall.
  Running setup.py develop for pythondata-cpu-marocchino
Successfully installed pythondata-cpu-marocchino
[ 213.649] Installing pythondata-cpu-microwatt Git repository...
Obtaining file:///home/kevin/pythondata-cpu-microwatt
Installing collected packages: pythondata-cpu-microwatt
  Attempting uninstall: pythondata-cpu-microwatt
    Found existing installation: pythondata-cpu-microwatt 0.0.post1409
    Can't uninstall 'pythondata-cpu-microwatt'. No files were found to uninstall.
  Running setup.py develop for pythondata-cpu-microwatt
Successfully installed pythondata-cpu-microwatt
[ 216.114] Installing pythondata-cpu-blackparrot Git repository...
Obtaining file:///home/kevin/pythondata-cpu-blackparrot
Installing collected packages: pythondata-cpu-blackparrot
  Attempting uninstall: pythondata-cpu-blackparrot
    Found existing installation: pythondata-cpu-blackparrot 0.0.post1817
    Can't uninstall 'pythondata-cpu-blackparrot'. No files were found to uninstall.
  Running setup.py develop for pythondata-cpu-blackparrot
Successfully installed pythondata-cpu-blackparrot
[ 218.608] Installing pythondata-cpu-cv32e40p Git repository...
Obtaining file:///home/kevin/pythondata-cpu-cv32e40p
Installing collected packages: pythondata-cpu-cv32e40p
  Attempting uninstall: pythondata-cpu-cv32e40p
    Found existing installation: pythondata-cpu-cv32e40p 0.0.post152
    Can't uninstall 'pythondata-cpu-cv32e40p'. No files were found to uninstall.
  Running setup.py develop for pythondata-cpu-cv32e40p
Successfully installed pythondata-cpu-cv32e40p
[ 221.033] Installing pythondata-cpu-cv32e41p Git repository...
Obtaining file:///home/kevin/pythondata-cpu-cv32e41p
Installing collected packages: pythondata-cpu-cv32e41p
  Attempting uninstall: pythondata-cpu-cv32e41p
    Found existing installation: pythondata-cpu-cv32e41p 0.0.post1883
    Can't uninstall 'pythondata-cpu-cv32e41p'. No files were found to uninstall.
  Running setup.py develop for pythondata-cpu-cv32e41p
Successfully installed pythondata-cpu-cv32e41p
[ 223.451] Installing pythondata-cpu-cva5 Git repository...
Obtaining file:///home/kevin/pythondata-cpu-cva5
Installing collected packages: pythondata-cpu-cva5
  Attempting uninstall: pythondata-cpu-cva5
    Found existing installation: pythondata-cpu-cva5 0.0.post649
    Can't uninstall 'pythondata-cpu-cva5'. No files were found to uninstall.
  Running setup.py develop for pythondata-cpu-cva5
Successfully installed pythondata-cpu-cva5
[ 225.900] Installing pythondata-cpu-cva6 Git repository...
Obtaining file:///home/kevin/pythondata-cpu-cva6
Installing collected packages: pythondata-cpu-cva6
  Attempting uninstall: pythondata-cpu-cva6
    Found existing installation: pythondata-cpu-cva6 4.2.0.post435
    Can't uninstall 'pythondata-cpu-cva6'. No files were found to uninstall.
  Running setup.py develop for pythondata-cpu-cva6
Successfully installed pythondata-cpu-cva6
[ 228.377] Installing pythondata-cpu-ibex Git repository...
Obtaining file:///home/kevin/pythondata-cpu-ibex
Installing collected packages: pythondata-cpu-ibex
  Attempting uninstall: pythondata-cpu-ibex
    Found existing installation: pythondata-cpu-ibex 0.0.post2214
    Can't uninstall 'pythondata-cpu-ibex'. No files were found to uninstall.
  Running setup.py develop for pythondata-cpu-ibex
Successfully installed pythondata-cpu-ibex
[ 230.776] Installing pythondata-cpu-minerva Git repository...
Obtaining file:///home/kevin/pythondata-cpu-minerva
Installing collected packages: pythondata-cpu-minerva
  Attempting uninstall: pythondata-cpu-minerva
    Found existing installation: pythondata-cpu-minerva 0.0.post262
    Can't uninstall 'pythondata-cpu-minerva'. No files were found to uninstall.
  Running setup.py develop for pythondata-cpu-minerva
Successfully installed pythondata-cpu-minerva
[ 233.193] Installing pythondata-cpu-naxriscv Git repository...
Obtaining file:///home/kevin/pythondata-cpu-naxriscv
Installing collected packages: pythondata-cpu-naxriscv
  Attempting uninstall: pythondata-cpu-naxriscv
    Found existing installation: pythondata-cpu-naxriscv 1.0.1.post325
    Can't uninstall 'pythondata-cpu-naxriscv'. No files were found to uninstall.
  Running setup.py develop for pythondata-cpu-naxriscv
Successfully installed pythondata-cpu-naxriscv
[ 235.585] Installing pythondata-cpu-picorv32 Git repository...
Obtaining file:///home/kevin/pythondata-cpu-picorv32
Installing collected packages: pythondata-cpu-picorv32
  Attempting uninstall: pythondata-cpu-picorv32
    Found existing installation: pythondata-cpu-picorv32 1.0.post194
    Can't uninstall 'pythondata-cpu-picorv32'. No files were found to uninstall.
  Running setup.py develop for pythondata-cpu-picorv32
Successfully installed pythondata-cpu-picorv32
[ 238.004] Installing pythondata-cpu-rocket Git repository...
Obtaining file:///home/kevin/pythondata-cpu-rocket
Installing collected packages: pythondata-cpu-rocket
  Attempting uninstall: pythondata-cpu-rocket
    Found existing installation: pythondata-cpu-rocket 0.0.post7146
    Can't uninstall 'pythondata-cpu-rocket'. No files were found to uninstall.
  Running setup.py develop for pythondata-cpu-rocket
Successfully installed pythondata-cpu-rocket
[ 240.512] Installing pythondata-cpu-serv Git repository...
Obtaining file:///home/kevin/pythondata-cpu-serv
Installing collected packages: pythondata-cpu-serv
  Attempting uninstall: pythondata-cpu-serv
    Found existing installation: pythondata-cpu-serv 1.2.0.post146
    Can't uninstall 'pythondata-cpu-serv'. No files were found to uninstall.
  Running setup.py develop for pythondata-cpu-serv
Successfully installed pythondata-cpu-serv
[ 242.976] Installing pythondata-cpu-vexriscv Git repository...
Obtaining file:///home/kevin/pythondata-cpu-vexriscv
Installing collected packages: pythondata-cpu-vexriscv
  Attempting uninstall: pythondata-cpu-vexriscv
    Found existing installation: pythondata-cpu-vexriscv 1.0.1.post407
    Can't uninstall 'pythondata-cpu-vexriscv'. No files were found to uninstall.
  Running setup.py develop for pythondata-cpu-vexriscv
Successfully installed pythondata-cpu-vexriscv
[ 245.416] Installing pythondata-cpu-vexriscv-smp Git repository...
Obtaining file:///home/kevin/pythondata-cpu-vexriscv-smp
Installing collected packages: pythondata-cpu-vexriscv-smp
  Attempting uninstall: pythondata-cpu-vexriscv-smp
    Found existing installation: pythondata-cpu-vexriscv-smp 1.0.1.post325
    Can't uninstall 'pythondata-cpu-vexriscv-smp'. No files were found to uninstall.
  Running setup.py develop for pythondata-cpu-vexriscv-smp
Successfully installed pythondata-cpu-vexriscv-smp
kevin@kevin:~/linux-on-litex-vexriscv$ ./litex_setup.py --update
          __   _ __      _  __
         / /  (_) /____ | |/_/
        / /__/ / __/ -_)>  <
       /____/_/\__/\__/_/|_|
     Build your hardware, easily!
          LiteX Setup utility.

[   0.002] LiteX Setup auto-update...
[   0.486] LiteX Setup is up to date.
[   0.487] Updating Git repositories...
[   0.487] ----------------------------
[   0.487] Updating migen Git repository...
Already on 'master'
Your branch is up to date with 'origin/master'.
Already up to date.
[   1.060] Updating pythondata-software-picolibc Git repository...
Already on 'master'
Your branch is up to date with 'origin/master'.
Already up to date.
[   1.645] Updating pythondata-software-compiler_rt Git repository...
Already on 'master'
Your branch is up to date with 'origin/master'.
Already up to date.
[   2.322] Updating litex Git repository...
Already on 'master'
Your branch is up to date with 'origin/master'.
Already up to date.
[   2.927] Updating liteeth Git repository...
Already on 'master'
Your branch is up to date with 'origin/master'.
Already up to date.
[   3.394] Updating litedram Git repository...
Already on 'master'
Your branch is up to date with 'origin/master'.
Already up to date.
[   3.883] Updating litepcie Git repository...
Already on 'master'
Your branch is up to date with 'origin/master'.
Already up to date.
[   4.347] Updating litesata Git repository...
Already on 'master'
Your branch is up to date with 'origin/master'.
Already up to date.
[   4.803] Updating litesdcard Git repository...
Already on 'master'
Your branch is up to date with 'origin/master'.
Already up to date.
[   5.275] Updating liteiclink Git repository...
Already on 'master'
Your branch is up to date with 'origin/master'.
Already up to date.
[   5.744] Updating litescope Git repository...
Already on 'master'
Your branch is up to date with 'origin/master'.
Already up to date.
[   6.216] Updating litejesd204b Git repository...
Already on 'master'
Your branch is up to date with 'origin/master'.
Already up to date.
[   6.666] Updating litespi Git repository...
Already on 'master'
Your branch is up to date with 'origin/master'.
Already up to date.
[   7.141] Updating valentyusb Git repository...
Already on 'hw_cdc_eptri'
Your branch is up to date with 'origin/hw_cdc_eptri'.
Already up to date.
[   7.611] Updating litex-boards Git repository...
Already on 'master'
Your branch is up to date with 'origin/master'.
Already up to date.
[   8.155] Updating pythondata-misc-tapcfg Git repository...
Already on 'master'
Your branch is up to date with 'origin/master'.
Already up to date.
[   8.625] Updating pythondata-misc-usb_ohci Git repository...
Already on 'master'
Your branch is up to date with 'origin/master'.
Already up to date.
[   9.082] Updating pythondata-cpu-lm32 Git repository...
Already on 'master'
Your branch is up to date with 'origin/master'.
Already up to date.
[   9.553] Updating pythondata-cpu-mor1kx Git repository...
Already on 'master'
Your branch is up to date with 'origin/master'.
Already up to date.
[  10.015] Updating pythondata-cpu-naxriscv Git repository...
Already on 'master'
Your branch is up to date with 'origin/master'.
Already up to date.
[  10.475] Updating pythondata-cpu-serv Git repository...
Already on 'master'
Your branch is up to date with 'origin/master'.
Already up to date.
[  10.960] Updating pythondata-cpu-vexriscv Git repository...
Already on 'master'
Your branch is up to date with 'origin/master'.
Already up to date.
[  11.467] Updating pythondata-cpu-vexriscv-smp Git repository...
M       pythondata_cpu_vexriscv_smp.egg-info/SOURCES.txt
Already on 'master'
Your branch is up to date with 'origin/master'.
Already up to date.
kevin@kevin:~/linux-on-litex-vexriscv$ sudo ./litex_setup.py --gcc=riscv
          __   _ __      _  __
         / /  (_) /____ | |/_/
        / /__/ / __/ -_)>  <
       /____/_/\__/\__/_/|_|
     Build your hardware, easily!
          LiteX Setup utility.

[   0.002] LiteX Setup auto-update...
[   0.217] LiteX Setup is up to date.
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
  binutils-riscv64-linux-gnu cpp-9-riscv64-linux-gnu cpp-riscv64-linux-gnu gcc-10-cross-base-ports gcc-9-cross-base-ports gcc-9-riscv64-linux-gnu
  gcc-9-riscv64-linux-gnu-base libatomic1-riscv64-cross libc6-dev-riscv64-cross libc6-riscv64-cross libgcc-9-dev-riscv64-cross libgcc-s1-riscv64-cross
  libgomp1-riscv64-cross linux-libc-dev-riscv64-cross
Suggested packages:
  binutils-doc gcc-9-locales cpp-doc gcc-9-doc libtool gdb-riscv64-linux-gnu gcc-doc
The following NEW packages will be installed:
  binutils-riscv64-linux-gnu cpp-9-riscv64-linux-gnu cpp-riscv64-linux-gnu gcc-10-cross-base-ports gcc-9-cross-base-ports gcc-9-riscv64-linux-gnu
  gcc-9-riscv64-linux-gnu-base gcc-riscv64-linux-gnu libatomic1-riscv64-cross libc6-dev-riscv64-cross libc6-riscv64-cross libgcc-9-dev-riscv64-cross
  libgcc-s1-riscv64-cross libgomp1-riscv64-cross linux-libc-dev-riscv64-cross
0 upgraded, 15 newly installed, 0 to remove and 93 not upgraded.
Need to get 20.7 MB of archives.
After this operation, 59.3 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://tw.archive.ubuntu.com/ubuntu focal-updates/main amd64 binutils-riscv64-linux-gnu amd64 2.34-6ubuntu1.4 [1058 kB]
Get:2 http://tw.archive.ubuntu.com/ubuntu focal-updates/universe amd64 gcc-9-riscv64-linux-gnu-base amd64 9.4.0-1ubuntu1~20.04cross1 [19.6 kB]
Get:3 http://tw.archive.ubuntu.com/ubuntu focal-updates/universe amd64 cpp-9-riscv64-linux-gnu amd64 9.4.0-1ubuntu1~20.04cross1 [6305 kB]
Get:4 http://tw.archive.ubuntu.com/ubuntu focal/universe amd64 cpp-riscv64-linux-gnu amd64 4:9.3.0-1ubuntu2 [3416 B]
Get:5 http://tw.archive.ubuntu.com/ubuntu focal-updates/universe amd64 gcc-10-cross-base-ports all 10.3.0-1ubuntu1~20.04cross1 [15.3 kB]
Get:6 http://tw.archive.ubuntu.com/ubuntu focal-updates/universe amd64 gcc-9-cross-base-ports all 9.4.0-1ubuntu1~20.04cross1 [14.9 kB]
Get:7 http://tw.archive.ubuntu.com/ubuntu focal/universe amd64 libc6-riscv64-cross all 2.31-0ubuntu7cross1 [1030 kB]
Get:8 http://tw.archive.ubuntu.com/ubuntu focal-updates/universe amd64 libgcc-s1-riscv64-cross all 10.3.0-1ubuntu1~20.04cross1 [40.7 kB]
Get:9 http://tw.archive.ubuntu.com/ubuntu focal-updates/universe amd64 libgomp1-riscv64-cross all 10.3.0-1ubuntu1~20.04cross1 [81.9 kB]
Get:10 http://tw.archive.ubuntu.com/ubuntu focal-updates/universe amd64 libatomic1-riscv64-cross all 10.3.0-1ubuntu1~20.04cross1 [7196 B]
Get:11 http://tw.archive.ubuntu.com/ubuntu focal-updates/universe amd64 libgcc-9-dev-riscv64-cross all 9.4.0-1ubuntu1~20.04cross1 [403 kB]
Get:12 http://tw.archive.ubuntu.com/ubuntu focal-updates/universe amd64 gcc-9-riscv64-linux-gnu amd64 9.4.0-1ubuntu1~20.04cross1 [7053 kB]
Get:13 http://tw.archive.ubuntu.com/ubuntu focal/universe amd64 gcc-riscv64-linux-gnu amd64 4:9.3.0-1ubuntu2 [1420 B]
Get:14 http://tw.archive.ubuntu.com/ubuntu focal/universe amd64 linux-libc-dev-riscv64-cross all 5.4.0-21.25cross1 [1035 kB]
Get:15 http://tw.archive.ubuntu.com/ubuntu focal/universe amd64 libc6-dev-riscv64-cross all 2.31-0ubuntu7cross1 [3638 kB]
Fetched 20.7 MB in 1s (16.6 MB/s)
Selecting previously unselected package binutils-riscv64-linux-gnu.
(Reading database ... 192654 files and directories currently installed.)
Preparing to unpack .../00-binutils-riscv64-linux-gnu_2.34-6ubuntu1.4_amd64.deb ...
Unpacking binutils-riscv64-linux-gnu (2.34-6ubuntu1.4) ...
Selecting previously unselected package gcc-9-riscv64-linux-gnu-base:amd64.
Preparing to unpack .../01-gcc-9-riscv64-linux-gnu-base_9.4.0-1ubuntu1~20.04cross1_amd64.deb ...
Unpacking gcc-9-riscv64-linux-gnu-base:amd64 (9.4.0-1ubuntu1~20.04cross1) ...
Selecting previously unselected package cpp-9-riscv64-linux-gnu.
Preparing to unpack .../02-cpp-9-riscv64-linux-gnu_9.4.0-1ubuntu1~20.04cross1_amd64.deb ...
Unpacking cpp-9-riscv64-linux-gnu (9.4.0-1ubuntu1~20.04cross1) ...
Selecting previously unselected package cpp-riscv64-linux-gnu.
Preparing to unpack .../03-cpp-riscv64-linux-gnu_4%3a9.3.0-1ubuntu2_amd64.deb ...
Unpacking cpp-riscv64-linux-gnu (4:9.3.0-1ubuntu2) ...
Selecting previously unselected package gcc-10-cross-base-ports.
Preparing to unpack .../04-gcc-10-cross-base-ports_10.3.0-1ubuntu1~20.04cross1_all.deb ...
Unpacking gcc-10-cross-base-ports (10.3.0-1ubuntu1~20.04cross1) ...
Selecting previously unselected package gcc-9-cross-base-ports.
Preparing to unpack .../05-gcc-9-cross-base-ports_9.4.0-1ubuntu1~20.04cross1_all.deb ...
Unpacking gcc-9-cross-base-ports (9.4.0-1ubuntu1~20.04cross1) ...
Selecting previously unselected package libc6-riscv64-cross.
Preparing to unpack .../06-libc6-riscv64-cross_2.31-0ubuntu7cross1_all.deb ...
Unpacking libc6-riscv64-cross (2.31-0ubuntu7cross1) ...
Selecting previously unselected package libgcc-s1-riscv64-cross.
Preparing to unpack .../07-libgcc-s1-riscv64-cross_10.3.0-1ubuntu1~20.04cross1_all.deb ...
Unpacking libgcc-s1-riscv64-cross (10.3.0-1ubuntu1~20.04cross1) ...
Selecting previously unselected package libgomp1-riscv64-cross.
Preparing to unpack .../08-libgomp1-riscv64-cross_10.3.0-1ubuntu1~20.04cross1_all.deb ...
Unpacking libgomp1-riscv64-cross (10.3.0-1ubuntu1~20.04cross1) ...
Selecting previously unselected package libatomic1-riscv64-cross.
Preparing to unpack .../09-libatomic1-riscv64-cross_10.3.0-1ubuntu1~20.04cross1_all.deb ...
Unpacking libatomic1-riscv64-cross (10.3.0-1ubuntu1~20.04cross1) ...
Selecting previously unselected package libgcc-9-dev-riscv64-cross.
Preparing to unpack .../10-libgcc-9-dev-riscv64-cross_9.4.0-1ubuntu1~20.04cross1_all.deb ...
Unpacking libgcc-9-dev-riscv64-cross (9.4.0-1ubuntu1~20.04cross1) ...
Selecting previously unselected package gcc-9-riscv64-linux-gnu.
Preparing to unpack .../11-gcc-9-riscv64-linux-gnu_9.4.0-1ubuntu1~20.04cross1_amd64.deb ...
Unpacking gcc-9-riscv64-linux-gnu (9.4.0-1ubuntu1~20.04cross1) ...
Selecting previously unselected package gcc-riscv64-linux-gnu.
Preparing to unpack .../12-gcc-riscv64-linux-gnu_4%3a9.3.0-1ubuntu2_amd64.deb ...
Unpacking gcc-riscv64-linux-gnu (4:9.3.0-1ubuntu2) ...
Selecting previously unselected package linux-libc-dev-riscv64-cross.
Preparing to unpack .../13-linux-libc-dev-riscv64-cross_5.4.0-21.25cross1_all.deb ...
Unpacking linux-libc-dev-riscv64-cross (5.4.0-21.25cross1) ...
Selecting previously unselected package libc6-dev-riscv64-cross.
Preparing to unpack .../14-libc6-dev-riscv64-cross_2.31-0ubuntu7cross1_all.deb ...
Unpacking libc6-dev-riscv64-cross (2.31-0ubuntu7cross1) ...
Setting up gcc-10-cross-base-ports (10.3.0-1ubuntu1~20.04cross1) ...
Setting up binutils-riscv64-linux-gnu (2.34-6ubuntu1.4) ...
Setting up gcc-9-riscv64-linux-gnu-base:amd64 (9.4.0-1ubuntu1~20.04cross1) ...
Setting up gcc-9-cross-base-ports (9.4.0-1ubuntu1~20.04cross1) ...
Setting up cpp-9-riscv64-linux-gnu (9.4.0-1ubuntu1~20.04cross1) ...
Setting up linux-libc-dev-riscv64-cross (5.4.0-21.25cross1) ...
Setting up libc6-riscv64-cross (2.31-0ubuntu7cross1) ...
Setting up libgomp1-riscv64-cross (10.3.0-1ubuntu1~20.04cross1) ...
Setting up libatomic1-riscv64-cross (10.3.0-1ubuntu1~20.04cross1) ...
Setting up cpp-riscv64-linux-gnu (4:9.3.0-1ubuntu2) ...
Setting up libgcc-s1-riscv64-cross (10.3.0-1ubuntu1~20.04cross1) ...
Setting up libc6-dev-riscv64-cross (2.31-0ubuntu7cross1) ...
Setting up libgcc-9-dev-riscv64-cross (9.4.0-1ubuntu1~20.04cross1) ...
Setting up gcc-9-riscv64-linux-gnu (9.4.0-1ubuntu1~20.04cross1) ...
Setting up gcc-riscv64-linux-gnu (4:9.3.0-1ubuntu2) ...
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for libc-bin (2.31-0ubuntu9.9) ...
kevin@kevin:~/linux-on-litex-vexriscv$ ~/litex-boards/litex_boards/targets/xilinx_kv260.py
INFO:SoC:        __   _ __      _  __
INFO:SoC:       / /  (_) /____ | |/_/
INFO:SoC:      / /__/ / __/ -_)>  <
INFO:SoC:     /____/_/\__/\__/_/|_|
INFO:SoC:  Build your hardware, easily!
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:Creating SoC... (2023-04-29 12:54:41)
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:FPGA device : xck26-sfvc784-2lv-c.
INFO:SoC:System clock: 100.000MHz.
INFO:SoCBusHandler:Creating Bus Handler...
INFO:SoCBusHandler:32-bit wishbone Bus, 4.0GiB Address Space.
INFO:SoCBusHandler:Adding reserved Bus Regions...
INFO:SoCBusHandler:Bus Handler created.
INFO:SoCCSRHandler:Creating CSR Handler...
INFO:SoCCSRHandler:32-bit CSR Bus, 32-bit Aligned, 16.0KiB Address Space, 2048B Paging, big Ordering (Up to 32 Locations).
INFO:SoCCSRHandler:Adding reserved CSRs...
INFO:SoCCSRHandler:CSR Handler created.
INFO:SoCIRQHandler:Creating IRQ Handler...
INFO:SoCIRQHandler:IRQ Handler (up to 32 Locations).
INFO:SoCIRQHandler:Adding reserved IRQs...
INFO:SoCIRQHandler:IRQ Handler created.
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:Initial SoC:
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:32-bit wishbone Bus, 4.0GiB Address Space.
INFO:SoC:32-bit CSR Bus, 32-bit Aligned, 16.0KiB Address Space, 2048B Paging, big Ordering (Up to 32 Locations).
INFO:SoC:IRQ Handler (up to 32 Locations).
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:Controller ctrl added.
INFO:SoC:CPU zynqmp added.
INFO:SoC:CPU zynqmp adding IO Region 0 at 0x80000000 (Size: 0x40000000).
INFO:SoCBusHandler:io0 Region added at Origin: 0x80000000, Size: 0x40000000, Mode: RW, Cached: False Linker: False.
INFO:SoC:CPU zynqmp adding IO Region 1 at 0xe0000000 (Size: 0xff20000000).
INFO:SoCRegion:Region size rounded internally from 0xff20000000 to 0x10000000000.
INFO:SoCBusHandler:io1 Region added at Origin: 0xe0000000, Size: 0xff20000000, Mode: RW, Cached: False Linker: False.
INFO:SoC:CPU zynqmp setting reset address to 0xc0000000.
INFO:SoC:CPU zynqmp adding Bus Master(s).
INFO:SoCBusHandler:master0 added as Bus Master.
INFO:SoCBusHandler:sram Region added at Origin: 0x00000000, Size: 0x80000000, Mode: RW, Cached: True Linker: False.
INFO:SoCBusHandler:rom Region added at Origin: 0xc0000000, Size: 0x04000000, Mode: RW, Cached: True Linker: True.
kevin@kevin:~/linux-on-litex-vexriscv$ wget -O linux_2022_03_23.zip  https://github.com/litex-hub/linux-on-litex-vexriscv/files/8331338/linux_2022_03_23.zip
--2023-04-29 12:54:51--  https://github.com/litex-hub/linux-on-litex-vexriscv/files/8331338/linux_2022_03_23.zip
Resolving github.com (github.com)... 20.27.177.113
Connecting to github.com (github.com)|20.27.177.113|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://objects.githubusercontent.com/github-production-repository-file-5c1aeb/183392076/8331338?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20230429%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20230429T045452Z&X-Amz-Expires=300&X-Amz-Signature=5dc457ec093c7ec0123d3d805d2c81d6f3bf17fa0f74153e1976d427f7373a0f&X-Amz-SignedHeaders=host&actor_id=0&key_id=0&repo_id=183392076&response-content-disposition=attachment%3Bfilename%3Dlinux_2022_03_23.zip&response-content-type=application%2Fzip [following]
--2023-04-29 12:54:52--  https://objects.githubusercontent.com/github-production-repository-file-5c1aeb/183392076/8331338?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20230429%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20230429T045452Z&X-Amz-Expires=300&X-Amz-Signature=5dc457ec093c7ec0123d3d805d2c81d6f3bf17fa0f74153e1976d427f7373a0f&X-Amz-SignedHeaders=host&actor_id=0&key_id=0&repo_id=183392076&response-content-disposition=attachment%3Bfilename%3Dlinux_2022_03_23.zip&response-content-type=application%2Fzip
Resolving objects.githubusercontent.com (objects.githubusercontent.com)... 185.199.108.133, 185.199.109.133, 185.199.110.133, ...
Connecting to objects.githubusercontent.com (objects.githubusercontent.com)|185.199.108.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 5358911 (5.1M) [application/zip]
Saving to: ‘linux_2022_03_23.zip’

linux_2022_03_23.zip                    100%[=============================================================================>]   5.11M  3.88MB/s    in 1.3s

2023-04-29 12:54:54 (3.88 MB/s) - ‘linux_2022_03_23.zip’ saved [5358911/5358911]

kevin@kevin:~/linux-on-litex-vexriscv$ unzip linux_2022_03_23.zip -d ./images
Archive:  linux_2022_03_23.zip
replace ./images/boot.json? [y]es, [n]o, [A]ll, [N]one, [r]ename: y
  inflating: ./images/boot.json
  inflating: ./images/Image
  inflating: ./images/opensbi.bin
  inflating: ./images/rootfs.cpio
  inflating: ./images/rv32.dtb
kevin@kevin:~/linux-on-litex-vexriscv$ ./sim.py
INFO:SoC:        __   _ __      _  __
INFO:SoC:       / /  (_) /____ | |/_/
INFO:SoC:      / /__/ / __/ -_)>  <
INFO:SoC:     /____/_/\__/\__/_/|_|
INFO:SoC:  Build your hardware, easily!
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:Creating SoC... (2023-04-29 12:55:16)
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:FPGA device : SIM.
INFO:SoC:System clock: 100.000MHz.
INFO:SoCBusHandler:Creating Bus Handler...
INFO:SoCBusHandler:32-bit wishbone Bus, 4.0GiB Address Space.
INFO:SoCBusHandler:Adding reserved Bus Regions...
INFO:SoCBusHandler:Bus Handler created.
INFO:SoCCSRHandler:Creating CSR Handler...
INFO:SoCCSRHandler:32-bit CSR Bus, 32-bit Aligned, 16.0KiB Address Space, 2048B Paging, big Ordering (Up to 32 Locations).
INFO:SoCCSRHandler:Adding reserved CSRs...
INFO:SoCCSRHandler:CSR Handler created.
INFO:SoCIRQHandler:Creating IRQ Handler...
INFO:SoCIRQHandler:IRQ Handler (up to 32 Locations).
INFO:SoCIRQHandler:Adding reserved IRQs...
INFO:SoCIRQHandler:IRQ Handler created.
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:Initial SoC:
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:32-bit wishbone Bus, 4.0GiB Address Space.
INFO:SoC:32-bit CSR Bus, 32-bit Aligned, 16.0KiB Address Space, 2048B Paging, big Ordering (Up to 32 Locations).
INFO:SoC:IRQ Handler (up to 32 Locations).
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:Controller ctrl added.
INFO:SoC:CPU vexriscv_smp added.
INFO:SoC:CPU vexriscv_smp adding IO Region 0 at 0x80000000 (Size: 0x80000000).
INFO:SoCBusHandler:io0 Region added at Origin: 0x80000000, Size: 0x80000000, Mode: RW, Cached: False Linker: False.
INFO:SoC:CPU vexriscv_smp overriding sram mapping from 0x01000000 to 0x10000000.
INFO:SoC:CPU vexriscv_smp setting reset address to 0x00000000.
INFO:SoC:CPU vexriscv_smp adding Bus Master(s).
INFO:SoCBusHandler:cpu_bus0 added as Bus Master.
INFO:SoC:CPU vexriscv_smp adding Interrupt(s).
INFO:SoCIRQHandler:noirq IRQ added at Location 0.
INFO:SoC:CPU noirq adding SoC components.
INFO:SoCCSRHandler:uart CSR added at Location 2.
INFO:SoCCSRHandler:timer0 CSR added at Location 3.
INFO:SoCBusHandler:opensbi Region added at Origin: 0x40f00000, Size: 0x00080000, Mode: RW, Cached: True Linker: True.
INFO:SoCBusHandler:plic Region added at Origin: 0xf0c00000, Size: 0x00400000, Mode: RW, Cached: False Linker: False.
INFO:SoCBusHandler:plic added as Bus Slave.
INFO:SoCBusHandler:clint Region added at Origin: 0xf0010000, Size: 0x00010000, Mode: RW, Cached: False Linker: False.
INFO:SoCBusHandler:clint added as Bus Slave.
INFO:SoCBusHandler:rom Region added at Origin: 0x00000000, Size: 0x00010000, Mode: RX, Cached: True Linker: False.
INFO:SoCBusHandler:rom added as Bus Slave.
INFO:SoC:RAM rom added Origin: 0x00000000, Size: 0x00010000, Mode: RX, Cached: True Linker: False.
INFO:SoCBusHandler:sram Region added at Origin: 0x10000000, Size: 0x00002000, Mode: RWX, Cached: True Linker: False.
INFO:SoCBusHandler:sram added as Bus Slave.
INFO:SoC:RAM sram added Origin: 0x10000000, Size: 0x00002000, Mode: RWX, Cached: True Linker: False.
INFO:SoCIRQHandler:uart IRQ allocated at Location 1.
INFO:SoCIRQHandler:timer0 IRQ allocated at Location 2.
INFO:SoCBusHandler:main_ram Region added at Origin: 0x40000000, Size: 0x04000000, Mode: RWX, Cached: True Linker: False.
INFO:SoCBusHandler:main_ram added as Bus Slave.
INFO:SoC:CSR Bridge csr added.
INFO:SoCBusHandler:csr Region added at Origin: 0xf0000000, Size: 0x00010000, Mode: RW, Cached: False Linker: False.
INFO:SoCBusHandler:csr added as Bus Slave.
INFO:SoCCSRHandler:csr added as CSR Master.
INFO:SoCBusHandler:Interconnect: InterconnectShared (1 <-> 6).
INFO:SoCCSRHandler:ctrl CSR allocated at Location 0.
INFO:SoCCSRHandler:sdram CSR allocated at Location 1.
INFO:SoCCSRHandler:supervisor CSR allocated at Location 4.
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:Finalized SoC:
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:32-bit wishbone Bus, 4.0GiB Address Space.
IO Regions: (1)
io0                 : Origin: 0x80000000, Size: 0x80000000, Mode: RW, Cached: False Linker: False
Bus Regions: (7)
rom                 : Origin: 0x00000000, Size: 0x00010000, Mode: RX, Cached: True Linker: False
sram                : Origin: 0x10000000, Size: 0x00002000, Mode: RWX, Cached: True Linker: False
main_ram            : Origin: 0x40000000, Size: 0x04000000, Mode: RWX, Cached: True Linker: False
opensbi             : Origin: 0x40f00000, Size: 0x00080000, Mode: RW, Cached: True Linker: True
csr                 : Origin: 0xf0000000, Size: 0x00010000, Mode: RW, Cached: False Linker: False
clint               : Origin: 0xf0010000, Size: 0x00010000, Mode: RW, Cached: False Linker: False
plic                : Origin: 0xf0c00000, Size: 0x00400000, Mode: RW, Cached: False Linker: False
Bus Masters: (1)
- cpu_bus0
Bus Slaves: (6)
- plic
- clint
- rom
- sram
- main_ram
- csr
INFO:SoC:32-bit CSR Bus, 32-bit Aligned, 16.0KiB Address Space, 2048B Paging, big Ordering (Up to 32 Locations).
CSR Locations: (5)
- ctrl       : 0
- sdram      : 1
- uart       : 2
- timer0     : 3
- supervisor : 4
INFO:SoC:IRQ Handler (up to 32 Locations).
IRQ Locations: (3)
- noirq  : 0
- uart   : 1
- timer0 : 2
INFO:SoC:--------------------------------------------------------------------------------
VexRiscv cluster : VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:SoC Hierarchy:
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:
SoCLinux
└─── crg (CRG)
└─── bus (SoCBusHandler)
│    └─── _interconnect (InterconnectShared)
│    │    └─── arbiter (Arbiter)
│    │    │    └─── rr (RoundRobin)
│    │    └─── decoder (Decoder)
│    │    └─── timeout (Timeout)
│    │    │    └─── waittimer_0* (WaitTimer)
└─── csr (SoCCSRHandler)
└─── irq (SoCIRQHandler)
└─── ctrl (SoCController)
│    └─── _reset (CSRStorage)
│    └─── _scratch (CSRStorage)
│    └─── _bus_errors (CSRStatus)
└─── cpu (VexRiscvSMP)
│    └─── [VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood]
└─── rom (SRAM)
└─── sram (SRAM)
└─── uart_phy (RS232PHYModel)
└─── uart (UART)
│    └─── ev (EventManager)
│    │    └─── eventsourceprocess_0* (EventSourceProcess)
│    │    └─── eventsourceprocess_1* (EventSourceProcess)
│    └─── tx_fifo (SyncFIFO)
│    │    └─── fifo (SyncFIFOBuffered)
│    │    │    └─── fifo (SyncFIFO)
│    └─── rx_fifo (SyncFIFO)
│    │    └─── fifo (SyncFIFOBuffered)
│    │    │    └─── fifo (SyncFIFO)
└─── timer0 (Timer)
│    └─── ev (EventManager)
│    │    └─── eventsourceprocess_0* (EventSourceProcess)
└─── supervisor (Supervisor)
└─── sdrphy (SDRAMPHYModel)
│    └─── dfiphasemodel_0* (DFIPhaseModel)
│    └─── bankmodel_0* (BankModel)
│    └─── bankmodel_1* (BankModel)
│    └─── bankmodel_2* (BankModel)
│    └─── bankmodel_3* (BankModel)
└─── sdram (LiteDRAMCore)
│    └─── dfii (DFIInjector)
│    │    └─── pi0 (PhaseInjector)
│    └─── controller (LiteDRAMController)
│    │    └─── refresher (Refresher)
│    │    │    └─── timer (RefreshTimer)
│    │    │    └─── postponer (RefreshPostponer)
│    │    │    └─── sequencer (RefreshSequencer)
│    │    │    │    └─── refreshexecuter_0* (RefreshExecuter)
│    │    │    └─── fsm (FSM)
│    │    └─── bankmachine_0* (BankMachine)
│    │    │    └─── syncfifo_0* (SyncFIFO)
│    │    │    │    └─── fifo (SyncFIFO)
│    │    │    └─── buffer_0* (Buffer)
│    │    │    │    └─── pipe_valid (PipeValid)
│    │    │    │    └─── pipeline (Pipeline)
│    │    │    └─── twtpcon (tXXDController)
│    │    │    └─── trccon (tXXDController)
│    │    │    └─── trascon (tXXDController)
│    │    │    └─── fsm (FSM)
│    │    └─── bankmachine_1* (BankMachine)
│    │    │    └─── syncfifo_0* (SyncFIFO)
│    │    │    │    └─── fifo (SyncFIFO)
│    │    │    └─── buffer_0* (Buffer)
│    │    │    │    └─── pipe_valid (PipeValid)
│    │    │    │    └─── pipeline (Pipeline)
│    │    │    └─── twtpcon (tXXDController)
│    │    │    └─── trccon (tXXDController)
│    │    │    └─── trascon (tXXDController)
│    │    │    └─── fsm (FSM)
│    │    └─── bankmachine_2* (BankMachine)
│    │    │    └─── syncfifo_0* (SyncFIFO)
│    │    │    │    └─── fifo (SyncFIFO)
│    │    │    └─── buffer_0* (Buffer)
│    │    │    │    └─── pipe_valid (PipeValid)
│    │    │    │    └─── pipeline (Pipeline)
│    │    │    └─── twtpcon (tXXDController)
│    │    │    └─── trccon (tXXDController)
│    │    │    └─── trascon (tXXDController)
│    │    │    └─── fsm (FSM)
│    │    └─── bankmachine_3* (BankMachine)
│    │    │    └─── syncfifo_0* (SyncFIFO)
│    │    │    │    └─── fifo (SyncFIFO)
│    │    │    └─── buffer_0* (Buffer)
│    │    │    │    └─── pipe_valid (PipeValid)
│    │    │    │    └─── pipeline (Pipeline)
│    │    │    └─── twtpcon (tXXDController)
│    │    │    └─── trccon (tXXDController)
│    │    │    └─── trascon (tXXDController)
│    │    │    └─── fsm (FSM)
│    │    └─── multiplexer (Multiplexer)
│    │    │    └─── choose_cmd (_CommandChooser)
│    │    │    │    └─── roundrobin_0* (RoundRobin)
│    │    │    └─── choose_req (_CommandChooser)
│    │    │    │    └─── roundrobin_0* (RoundRobin)
│    │    │    └─── _steerer_0* (_Steerer)
│    │    │    └─── trrdcon (tXXDController)
│    │    │    └─── tfawcon (tFAWController)
│    │    │    └─── tccdcon (tXXDController)
│    │    │    └─── twtrcon (tXXDController)
│    │    │    └─── fsm (FSM)
│    └─── crossbar (LiteDRAMCrossbar)
│    │    └─── roundrobin_0* (RoundRobin)
│    │    └─── roundrobin_1* (RoundRobin)
│    │    └─── roundrobin_2* (RoundRobin)
│    │    └─── roundrobin_3* (RoundRobin)
└─── converter_0* (Converter)
└─── wishbone_bridge (LiteDRAMWishbone2Native)
│    └─── fsm (FSM)
└─── csr_bridge (Wishbone2CSR)
│    └─── fsm_0* (FSM)
└─── csr_bankarray (CSRBankArray)
│    └─── csrbank_0* (CSRBank)
│    │    └─── csrstorage_0* (CSRStorage)
│    │    └─── csrstorage_1* (CSRStorage)
│    │    └─── csrstatus_0* (CSRStatus)
│    └─── csrbank_1* (CSRBank)
│    │    └─── csrstorage_0* (CSRStorage)
│    │    └─── csrstorage_1* (CSRStorage)
│    │    └─── csrstorage_2* (CSRStorage)
│    │    └─── csrstorage_3* (CSRStorage)
│    │    └─── csrstorage_4* (CSRStorage)
│    │    └─── csrstatus_0* (CSRStatus)
│    └─── csrbank_2* (CSRBank)
│    └─── csrbank_3* (CSRBank)
│    │    └─── csrstorage_0* (CSRStorage)
│    │    └─── csrstorage_1* (CSRStorage)
│    │    └─── csrstorage_2* (CSRStorage)
│    │    └─── csrstorage_3* (CSRStorage)
│    │    └─── csrstatus_0* (CSRStatus)
│    │    └─── csrstatus_1* (CSRStatus)
│    │    └─── csrstatus_2* (CSRStatus)
│    │    └─── csrstorage_4* (CSRStorage)
│    └─── csrbank_4* (CSRBank)
│    │    └─── csrstatus_0* (CSRStatus)
│    │    └─── csrstatus_1* (CSRStatus)
│    │    └─── csrstatus_2* (CSRStatus)
│    │    └─── csrstatus_3* (CSRStatus)
│    │    └─── csrstorage_0* (CSRStorage)
│    │    └─── csrstatus_4* (CSRStatus)
│    │    └─── csrstatus_5* (CSRStatus)
└─── csr_interconnect (InterconnectShared)
* : Generated name.
[]: BlackBox.

INFO:SoC:--------------------------------------------------------------------------------
make: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/libc'
if [ -d "/home/kevin/litex/litex/soc/software/libc/riscv" ]; then \
        cp /home/kevin/litex/litex/soc/software/libc/riscv/* /home/kevin/pythondata-software-picolibc/pythondata_software_picolibc/data/newlib/libc/machine/riscv/ ;\
fi
meson /home/kevin/pythondata-software-picolibc/pythondata_software_picolibc/data \
        -Dmultilib=false \
        -Dpicocrt=false \
        -Datomic-ungetc=false \
        -Dthread-local-storage=false \
        -Dio-long-long=true \
        -Dformat-default=integer \
        -Dincludedir=picolibc/riscv64-linux-gnu/include \
        -Dlibdir=picolibc/riscv64-linux-gnu/lib \
        --cross-file cross.txt
WARNING: Unknown CPU family riscv, please report this at https://github.com/mesonbuild/meson/issues/new
The Meson build system
Version: 0.59.0
Source dir: /home/kevin/pythondata-software-picolibc/pythondata_software_picolibc/data
Build dir: /home/kevin/linux-on-litex-vexriscv/build/sim/software/libc
Build type: cross build
Project name: picolibc
Project version: 1.7.9
C compiler for the host machine: riscv64-linux-gnu-gcc (gcc 9.4.0 "riscv64-linux-gnu-gcc (Ubuntu 9.4.0-1ubuntu1~20.04) 9.4.0")
C linker for the host machine: riscv64-linux-gnu-gcc ld.bfd 2.34
C compiler for the build machine: cc (gcc 9.4.0 "cc (Ubuntu 9.4.0-1ubuntu1~20.04.1) 9.4.0")
C linker for the build machine: cc ld.bfd 2.34
Build machine cpu family: x86_64
Build machine cpu: x86_64
Host machine cpu family: riscv
Host machine cpu: vexriscv
Target machine cpu family: riscv
Target machine cpu: vexriscv
Compiler for C supports arguments -nostdlib: YES
Checking if "long double check" compiles: YES
Checking if "long double same as double" compiles: NO
Checking if "long double mantissa is 64 bits" compiles: NO
Checking if "long double mantissa is 113 bits" compiles: YES
Checking if "double same as float" compiles: NO
Compiler for C supports arguments -fno-common: YES
Compiler for C supports arguments -frounding-math: YES
Compiler for C supports arguments -fsignaling-nans: YES
Compiler for C supports arguments -Wno-unsupported-floating-point-opt: NO
Compiler for C supports arguments -fno-stack-protector: YES
Compiler for C supports arguments -fno-builtin-copysignl: YES
Program riscv64-linux-gnu-gcc-nm found: YES
Program scripts/duplicate-names found: YES (/home/kevin/pythondata-software-picolibc/pythondata_software_picolibc/data/scripts/duplicate-names)
Compiler for C supports link arguments -Wl,--defsym=_start=0: YES
Compiler for C supports link arguments -Wl,-alias,main,testalias: NO
Compiler for C supports function attribute alias: YES
Compiler for C supports function attribute format: YES
Compiler for C supports function attribute weak: YES
Configuring picolibc.specs using configuration
Configuring picolibcpp.specs using configuration
Configuring test.specs using configuration
Configuring picolibc.ld using configuration
Configuring picolibcpp.ld using configuration
Compiler for C supports arguments -Werror=implicit-function-declaration: YES
Compiler for C supports arguments -Werror=vla: YES
Compiler for C supports arguments -Warray-bounds: YES
Compiler for C supports arguments -Wold-style-definition: YES
Compiler for C supports arguments -Werror=double-promotion: YES
Compiler for C supports arguments -Wno-missing-braces: YES
Compiler for C supports arguments -Wno-implicit-int: YES
Compiler for C supports arguments -Wno-return-type: YES
Compiler for C supports arguments -Wno-unused-command-line-argument: NO
Checking if "packed structs may contain bitfields" compiles: YES
Checking if "has __builtin_mul_overflow" links: YES
Checking if "has __builtin_add_overflow" links: YES
Checking if "supports _Complex" compiles: YES
Checking if "has __builtin_expect" links: YES
Compiler for C supports arguments -Werror: YES
Checking if "attribute __alloc_size__" compiles: YES
Checking if "attributes constructor/destructor" compiles: YES
Checking if "test for __builtin_alloca" links: YES
Checking if "test for __builtin_ffs" links: YES
Checking if "test for __builtin_ffsl" links: YES
Checking if "test for __builtin_ffsll" links: YES
Checking if "test for __builtin_ctz" links: YES
Checking if "test for __builtin_ctzl" links: YES
Checking if "test for __builtin_ctzll" links: YES
Checking if "test for __builtin_copysignl" links: YES
Checking if "test for __builtin_copysign" links: YES
Checking if "test for __builtin_isinfl" links: YES
Checking if "test for __builtin_isinf" links: YES
Checking if "test for __builtin_isnanl" links: YES
Checking if "test for __builtin_isnan" links: YES
Checking if "test for __builtin_finitel" links: YES
Checking if "test for __builtin_isfinite" links: YES
Compiler for C supports arguments -fno-tree-loop-distribute-patterns: YES
Checking if "no_builtin attribute" compiles: NO
Compiler for C supports function attribute always_inline: YES
Compiler for C supports function attribute gnu_inline: YES
Compiler for C supports arguments -fno-builtin: YES
Compiler for C supports arguments -ffunction-sections: YES
Compiler for C supports arguments -fstack-protector-all: YES
Compiler for C supports arguments -fstack-protector-strong: YES
Compiler for C supports arguments -fno-builtin-malloc: YES
Compiler for C supports arguments -fno-builtin-free: YES
Message: libc/string/memcpy.c: machine overrides generic
Message: libc/string/memmove.S: machine overrides generic
Message: libc/string/memset.S: machine overrides generic
Message: libc/string/strcpy.c: machine overrides generic
Message: libc/string/strlen.c: machine overrides generic
Message: libc/string/strcmp.S: machine overrides generic
Message: libc/include/sys/fenv.h: machine overrides generic
Message: libc/include/machine/math.h: machine overrides generic
Message: libm/math/s_fabs.c: machine overrides generic
Message: libm/math/s_sqrt.c: machine overrides generic
Message: libm/math/sf_fabs.c: machine overrides generic
Message: libm/math/sf_sqrt.c: machine overrides generic
Message: libm/common/s_finite.c: machine overrides generic
Message: libm/common/s_copysign.c: machine overrides generic
Message: libm/common/s_isinf.c: machine overrides generic
Message: libm/common/s_isnan.c: machine overrides generic
Message: libm/common/s_fma.c: machine overrides generic
Message: libm/common/s_fmax.c: machine overrides generic
Message: libm/common/s_fmin.c: machine overrides generic
Message: libm/common/s_fpclassify.c: machine overrides generic
Message: libm/common/s_lrint.c: machine overrides generic
Message: libm/common/s_llrint.c: machine overrides generic
Message: libm/common/s_lround.c: machine overrides generic
Message: libm/common/s_llround.c: machine overrides generic
Message: libm/common/sf_finite.c: machine overrides generic
Message: libm/common/sf_copysign.c: machine overrides generic
Message: libm/common/sf_isinf.c: machine overrides generic
Message: libm/common/sf_isnan.c: machine overrides generic
Message: libm/common/sf_fma.c: machine overrides generic
Message: libm/common/sf_fmax.c: machine overrides generic
Message: libm/common/sf_fmin.c: machine overrides generic
Message: libm/common/sf_fpclassify.c: machine overrides generic
Message: libm/common/sf_lrint.c: machine overrides generic
Message: libm/common/sf_llrint.c: machine overrides generic
Message: libm/common/sf_lround.c: machine overrides generic
Message: libm/common/sf_llround.c: machine overrides generic
Message: libm/fenv/feclearexcept.c: machine overrides generic
Message: libm/fenv/fegetenv.c: machine overrides generic
Message: libm/fenv/fegetexceptflag.c: machine overrides generic
Message: libm/fenv/fegetround.c: machine overrides generic
Message: libm/fenv/feholdexcept.c: machine overrides generic
Message: libm/fenv/feraiseexcept.c: machine overrides generic
Message: libm/fenv/fesetenv.c: machine overrides generic
Message: libm/fenv/fesetexceptflag.c: machine overrides generic
Message: libm/fenv/fesetround.c: machine overrides generic
Message: libm/fenv/fetestexcept.c: machine overrides generic
Message: libm/fenv/feupdateenv.c: machine overrides generic
Configuring picolibc.h using configuration
Build targets in project: 9

Found ninja-1.11.1.git.kitware.jobserver-1 at /home/kevin/.local/bin/ninja
meson compile
[886/886] Generating libc_duplicates with a custom command
cp newlib/libc.a __libc.a
 CC       _libc.a
 AR       _libc.a
cp __libc.a _libc.a
 CC       libc.a
 AR       libc.a
cp _libc.a libc.a
make: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/libc'
make: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/libcompiler_rt'
 CC       umodsi3.o
 CC       udivsi3.o
 CC       divsi3.o
 CC       modsi3.o
 CC       comparesf2.o
/home/kevin/pythondata-software-compiler_rt/pythondata_software_compiler_rt/data/lib/builtins/comparesf2.c:85:1: warning: function declaration isn’t a prototype [-Wstrict-prototypes]
   85 | FNALIAS(__cmpsf2, __lesf2);
      | ^~~~~~~
 CC       comparedf2.o
/home/kevin/pythondata-software-compiler_rt/pythondata_software_compiler_rt/data/lib/builtins/comparedf2.c:85:1: warning: function declaration isn’t a prototype [-Wstrict-prototypes]
   85 | FNALIAS(__cmpdf2, __ledf2);
      | ^~~~~~~
 CC       negsf2.o
 CC       negdf2.o
 CC       addsf3.o
 CC       subsf3.o
 CC       mulsf3.o
 CC       divsf3.o
 CC       lshrdi3.o
 CC       muldi3.o
 CC       divdi3.o
 CC       ashldi3.o
 CC       ashrdi3.o
 CC       udivmoddi4.o
 CC       floatsisf.o
 CC       floatunsisf.o
 CC       fixsfsi.o
 CC       fixdfdi.o
 CC       fixunssfsi.o
 CC       fixunsdfdi.o
 CC       adddf3.o
 CC       subdf3.o
 CC       muldf3.o
 CC       divdf3.o
 CC       floatsidf.o
 CC       floatunsidf.o
 CC       floatdidf.o
 CC       fixdfsi.o
 CC       fixunsdfsi.o
 CC       clzsi2.o
 CC       ctzsi2.o
 CC       udivdi3.o
 CC       umoddi3.o
 CC       moddi3.o
 CC       ucmpdi2.o
 CC       mulsi3.o
 AR       libcompiler_rt.a
make: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/libcompiler_rt'
make: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/libbase'
 CC       crc16.o
 CC       crc32.o
 CC       console.o
 CC       system.o
 CC       progress.o
 CC       memtest.o
 CC       uart.o
 CC       spiflash.o
 CC       i2c.o
 CC       isr.o
 AR       libbase.a
make: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/libbase'
make: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/libfatfs'
 CC       ffunicode.o
 CC       ff.o
 AR       libfatfs.a
make: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/libfatfs'
make: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/liblitespi'
 CC       spiflash.o
 AR       liblitespi.a
make: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/liblitespi'
make: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/liblitedram'
 CC       sdram.o
 CC       bist.o
 CC       sdram_dbg.o
 CC       sdram_spd.o
 CC       utils.o
 CC       accessors.o
 AR       liblitedram.a
make: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/liblitedram'
make: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/libliteeth'
 CC       udp.o
 CC       tftp.o
 CC       mdio.o
 AR       libliteeth.a
make: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/libliteeth'
make: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/liblitesdcard'
 CC       sdcard.o
 CC       spisdcard.o
 AR       liblitesdcard.a
make: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/liblitesdcard'
make: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/liblitesata'
 CC       sata.o
 AR       liblitesata.a
make: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/liblitesata'
make: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/bios'
 CC       boot-helper.o
 CC       boot.o
 CC       helpers.o
 CC       cmd_bios.o
 CC       cmd_mem.o
 CC       cmd_boot.o
 CC       cmd_i2c.o
 CC       cmd_spiflash.o
 CC       cmd_litedram.o
 CC       cmd_liteeth.o
 CC       cmd_litesdcard.o
 CC       cmd_litesata.o
 CC       sim_debug.o
 CC       main.o
 CC       complete.o
 CC       readline.o
 CC       crt0.o
 CC       bios.elf
chmod -x bios.elf
 OBJCOPY  bios.bin
chmod -x bios.bin
python3 -m litex.soc.software.crcfbigen bios.bin --little
python3 -m litex.soc.software.memusage bios.elf /home/kevin/linux-on-litex-vexriscv/build/sim/software/bios/../include/generated/regions.ld riscv64-linux-gnu

ROM usage: 24.25KiB     (37.89%)
RAM usage: 1.36KiB      (16.99%)

rm crt0.o
make: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/bios'
INFO:SoC:Initializing ROM rom with contents (Size: 0x6104).
INFO:SoC:Auto-Resizing ROM rom from 0x10000 to 0x6104.
INFO:SoC:        __   _ __      _  __
INFO:SoC:       / /  (_) /____ | |/_/
INFO:SoC:      / /__/ / __/ -_)>  <
INFO:SoC:     /____/_/\__/\__/_/|_|
INFO:SoC:  Build your hardware, easily!
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:Creating SoC... (2023-04-29 12:55:39)
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:FPGA device : SIM.
INFO:SoC:System clock: 100.000MHz.
INFO:SoCBusHandler:Creating Bus Handler...
INFO:SoCBusHandler:32-bit wishbone Bus, 4.0GiB Address Space.
INFO:SoCBusHandler:Adding reserved Bus Regions...
INFO:SoCBusHandler:Bus Handler created.
INFO:SoCCSRHandler:Creating CSR Handler...
INFO:SoCCSRHandler:32-bit CSR Bus, 32-bit Aligned, 16.0KiB Address Space, 2048B Paging, big Ordering (Up to 32 Locations).
INFO:SoCCSRHandler:Adding reserved CSRs...
INFO:SoCCSRHandler:CSR Handler created.
INFO:SoCIRQHandler:Creating IRQ Handler...
INFO:SoCIRQHandler:IRQ Handler (up to 32 Locations).
INFO:SoCIRQHandler:Adding reserved IRQs...
INFO:SoCIRQHandler:IRQ Handler created.
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:Initial SoC:
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:32-bit wishbone Bus, 4.0GiB Address Space.
INFO:SoC:32-bit CSR Bus, 32-bit Aligned, 16.0KiB Address Space, 2048B Paging, big Ordering (Up to 32 Locations).
INFO:SoC:IRQ Handler (up to 32 Locations).
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:Controller ctrl added.
INFO:SoC:CPU vexriscv_smp added.
INFO:SoC:CPU vexriscv_smp adding IO Region 0 at 0x80000000 (Size: 0x80000000).
INFO:SoCBusHandler:io0 Region added at Origin: 0x80000000, Size: 0x80000000, Mode: RW, Cached: False Linker: False.
INFO:SoC:CPU vexriscv_smp setting reset address to 0x00000000.
INFO:SoC:CPU vexriscv_smp adding Bus Master(s).
INFO:SoCBusHandler:cpu_bus0 added as Bus Master.
INFO:SoC:CPU vexriscv_smp adding Interrupt(s).
INFO:SoCIRQHandler:noirq IRQ added at Location 0.
INFO:SoC:CPU noirq adding SoC components.
INFO:SoCCSRHandler:uart CSR added at Location 2.
INFO:SoCCSRHandler:timer0 CSR added at Location 3.
INFO:SoCBusHandler:opensbi Region added at Origin: 0x40f00000, Size: 0x00080000, Mode: RW, Cached: True Linker: True.
INFO:SoCBusHandler:plic Region added at Origin: 0xf0c00000, Size: 0x00400000, Mode: RW, Cached: False Linker: False.
INFO:SoCBusHandler:plic added as Bus Slave.
INFO:SoCBusHandler:clint Region added at Origin: 0xf0010000, Size: 0x00010000, Mode: RW, Cached: False Linker: False.
INFO:SoCBusHandler:clint added as Bus Slave.
INFO:SoCBusHandler:rom Region added at Origin: 0x00000000, Size: 0x00010000, Mode: RX, Cached: True Linker: False.
INFO:SoCBusHandler:rom added as Bus Slave.
INFO:SoC:RAM rom added Origin: 0x00000000, Size: 0x00010000, Mode: RX, Cached: True Linker: False.
INFO:SoCBusHandler:sram Region added at Origin: 0x10000000, Size: 0x00002000, Mode: RWX, Cached: True Linker: False.
INFO:SoCBusHandler:sram added as Bus Slave.
INFO:SoC:RAM sram added Origin: 0x10000000, Size: 0x00002000, Mode: RWX, Cached: True Linker: False.
INFO:SoCIRQHandler:uart IRQ allocated at Location 1.
INFO:SoCIRQHandler:timer0 IRQ allocated at Location 2.
INFO:SoCBusHandler:main_ram Region added at Origin: 0x40000000, Size: 0x04000000, Mode: RWX, Cached: True Linker: False.
INFO:SoCBusHandler:main_ram added as Bus Slave.
INFO:SoC:CSR Bridge csr added.
INFO:SoCBusHandler:csr Region added at Origin: 0xf0000000, Size: 0x00010000, Mode: RW, Cached: False Linker: False.
INFO:SoCBusHandler:csr added as Bus Slave.
INFO:SoCCSRHandler:csr added as CSR Master.
INFO:SoCBusHandler:Interconnect: InterconnectShared (1 <-> 6).
INFO:SoCCSRHandler:ctrl CSR allocated at Location 0.
INFO:SoCCSRHandler:sdram CSR allocated at Location 1.
INFO:SoCCSRHandler:supervisor CSR allocated at Location 4.
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:Finalized SoC:
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:32-bit wishbone Bus, 4.0GiB Address Space.
IO Regions: (1)
io0                 : Origin: 0x80000000, Size: 0x80000000, Mode: RW, Cached: False Linker: False
Bus Regions: (7)
rom                 : Origin: 0x00000000, Size: 0x00010000, Mode: RX, Cached: True Linker: False
sram                : Origin: 0x10000000, Size: 0x00002000, Mode: RWX, Cached: True Linker: False
main_ram            : Origin: 0x40000000, Size: 0x04000000, Mode: RWX, Cached: True Linker: False
opensbi             : Origin: 0x40f00000, Size: 0x00080000, Mode: RW, Cached: True Linker: True
csr                 : Origin: 0xf0000000, Size: 0x00010000, Mode: RW, Cached: False Linker: False
clint               : Origin: 0xf0010000, Size: 0x00010000, Mode: RW, Cached: False Linker: False
plic                : Origin: 0xf0c00000, Size: 0x00400000, Mode: RW, Cached: False Linker: False
Bus Masters: (1)
- cpu_bus0
Bus Slaves: (6)
- plic
- clint
- rom
- sram
- main_ram
- csr
INFO:SoC:32-bit CSR Bus, 32-bit Aligned, 16.0KiB Address Space, 2048B Paging, big Ordering (Up to 32 Locations).
CSR Locations: (5)
- ctrl       : 0
- sdram      : 1
- uart       : 2
- timer0     : 3
- supervisor : 4
INFO:SoC:IRQ Handler (up to 32 Locations).
IRQ Locations: (3)
- noirq  : 0
- uart   : 1
- timer0 : 2
INFO:SoC:--------------------------------------------------------------------------------
VexRiscv cluster : VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:SoC Hierarchy:
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:
SoCLinux
└─── crg (CRG)
└─── bus (SoCBusHandler)
│    └─── _interconnect (InterconnectShared)
│    │    └─── arbiter (Arbiter)
│    │    │    └─── rr (RoundRobin)
│    │    └─── decoder (Decoder)
│    │    └─── timeout (Timeout)
│    │    │    └─── waittimer_0* (WaitTimer)
└─── csr (SoCCSRHandler)
└─── irq (SoCIRQHandler)
└─── ctrl (SoCController)
│    └─── _reset (CSRStorage)
│    └─── _scratch (CSRStorage)
│    └─── _bus_errors (CSRStatus)
└─── cpu (VexRiscvSMP)
│    └─── [VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood]
└─── rom (SRAM)
└─── sram (SRAM)
└─── uart_phy (RS232PHYModel)
└─── uart (UART)
│    └─── ev (EventManager)
│    │    └─── eventsourceprocess_0* (EventSourceProcess)
│    │    └─── eventsourceprocess_1* (EventSourceProcess)
│    └─── tx_fifo (SyncFIFO)
│    │    └─── fifo (SyncFIFOBuffered)
│    │    │    └─── fifo (SyncFIFO)
│    └─── rx_fifo (SyncFIFO)
│    │    └─── fifo (SyncFIFOBuffered)
│    │    │    └─── fifo (SyncFIFO)
└─── timer0 (Timer)
│    └─── ev (EventManager)
│    │    └─── eventsourceprocess_0* (EventSourceProcess)
└─── supervisor (Supervisor)
└─── sdrphy (SDRAMPHYModel)
│    └─── dfiphasemodel_0* (DFIPhaseModel)
│    └─── bankmodel_0* (BankModel)
│    └─── bankmodel_1* (BankModel)
│    └─── bankmodel_2* (BankModel)
│    └─── bankmodel_3* (BankModel)
└─── sdram (LiteDRAMCore)
│    └─── dfii (DFIInjector)
│    │    └─── pi0 (PhaseInjector)
│    └─── controller (LiteDRAMController)
│    │    └─── refresher (Refresher)
│    │    │    └─── timer (RefreshTimer)
│    │    │    └─── postponer (RefreshPostponer)
│    │    │    └─── sequencer (RefreshSequencer)
│    │    │    │    └─── refreshexecuter_0* (RefreshExecuter)
│    │    │    └─── fsm (FSM)
│    │    └─── bankmachine_0* (BankMachine)
│    │    │    └─── syncfifo_0* (SyncFIFO)
│    │    │    │    └─── fifo (SyncFIFO)
│    │    │    └─── buffer_0* (Buffer)
│    │    │    │    └─── pipe_valid (PipeValid)
│    │    │    │    └─── pipeline (Pipeline)
│    │    │    └─── twtpcon (tXXDController)
│    │    │    └─── trccon (tXXDController)
│    │    │    └─── trascon (tXXDController)
│    │    │    └─── fsm (FSM)
│    │    └─── bankmachine_1* (BankMachine)
│    │    │    └─── syncfifo_0* (SyncFIFO)
│    │    │    │    └─── fifo (SyncFIFO)
│    │    │    └─── buffer_0* (Buffer)
│    │    │    │    └─── pipe_valid (PipeValid)
│    │    │    │    └─── pipeline (Pipeline)
│    │    │    └─── twtpcon (tXXDController)
│    │    │    └─── trccon (tXXDController)
│    │    │    └─── trascon (tXXDController)
│    │    │    └─── fsm (FSM)
│    │    └─── bankmachine_2* (BankMachine)
│    │    │    └─── syncfifo_0* (SyncFIFO)
│    │    │    │    └─── fifo (SyncFIFO)
│    │    │    └─── buffer_0* (Buffer)
│    │    │    │    └─── pipe_valid (PipeValid)
│    │    │    │    └─── pipeline (Pipeline)
│    │    │    └─── twtpcon (tXXDController)
│    │    │    └─── trccon (tXXDController)
│    │    │    └─── trascon (tXXDController)
│    │    │    └─── fsm (FSM)
│    │    └─── bankmachine_3* (BankMachine)
│    │    │    └─── syncfifo_0* (SyncFIFO)
│    │    │    │    └─── fifo (SyncFIFO)
│    │    │    └─── buffer_0* (Buffer)
│    │    │    │    └─── pipe_valid (PipeValid)
│    │    │    │    └─── pipeline (Pipeline)
│    │    │    └─── twtpcon (tXXDController)
│    │    │    └─── trccon (tXXDController)
│    │    │    └─── trascon (tXXDController)
│    │    │    └─── fsm (FSM)
│    │    └─── multiplexer (Multiplexer)
│    │    │    └─── choose_cmd (_CommandChooser)
│    │    │    │    └─── roundrobin_0* (RoundRobin)
│    │    │    └─── choose_req (_CommandChooser)
│    │    │    │    └─── roundrobin_0* (RoundRobin)
│    │    │    └─── _steerer_0* (_Steerer)
│    │    │    └─── trrdcon (tXXDController)
│    │    │    └─── tfawcon (tFAWController)
│    │    │    └─── tccdcon (tXXDController)
│    │    │    └─── twtrcon (tXXDController)
│    │    │    └─── fsm (FSM)
│    └─── crossbar (LiteDRAMCrossbar)
│    │    └─── roundrobin_0* (RoundRobin)
│    │    └─── roundrobin_1* (RoundRobin)
│    │    └─── roundrobin_2* (RoundRobin)
│    │    └─── roundrobin_3* (RoundRobin)
└─── converter_0* (Converter)
└─── wishbone_bridge (LiteDRAMWishbone2Native)
│    └─── fsm (FSM)
└─── csr_bridge (Wishbone2CSR)
│    └─── fsm_0* (FSM)
└─── csr_bankarray (CSRBankArray)
│    └─── csrbank_0* (CSRBank)
│    │    └─── csrstorage_0* (CSRStorage)
│    │    └─── csrstorage_1* (CSRStorage)
│    │    └─── csrstatus_0* (CSRStatus)
│    └─── csrbank_1* (CSRBank)
│    │    └─── csrstorage_0* (CSRStorage)
│    │    └─── csrstorage_1* (CSRStorage)
│    │    └─── csrstorage_2* (CSRStorage)
│    │    └─── csrstorage_3* (CSRStorage)
│    │    └─── csrstorage_4* (CSRStorage)
│    │    └─── csrstatus_0* (CSRStatus)
│    └─── csrbank_2* (CSRBank)
│    └─── csrbank_3* (CSRBank)
│    │    └─── csrstorage_0* (CSRStorage)
│    │    └─── csrstorage_1* (CSRStorage)
│    │    └─── csrstorage_2* (CSRStorage)
│    │    └─── csrstorage_3* (CSRStorage)
│    │    └─── csrstatus_0* (CSRStatus)
│    │    └─── csrstatus_1* (CSRStatus)
│    │    └─── csrstatus_2* (CSRStatus)
│    │    └─── csrstorage_4* (CSRStorage)
│    └─── csrbank_4* (CSRBank)
│    │    └─── csrstatus_0* (CSRStatus)
│    │    └─── csrstatus_1* (CSRStatus)
│    │    └─── csrstatus_2* (CSRStatus)
│    │    └─── csrstatus_3* (CSRStatus)
│    │    └─── csrstorage_0* (CSRStorage)
│    │    └─── csrstatus_4* (CSRStatus)
│    │    └─── csrstatus_5* (CSRStatus)
└─── csr_interconnect (InterconnectShared)
* : Generated name.
[]: BlackBox.

INFO:SoC:--------------------------------------------------------------------------------
make: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/libc'
make: Nothing to be done for 'all'.
make: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/libc'
make: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/libcompiler_rt'
make: Nothing to be done for 'all'.
make: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/libcompiler_rt'
make: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/libbase'
 CC       console.o
 CC       system.o
 CC       memtest.o
 CC       uart.o
 CC       spiflash.o
 CC       i2c.o
 CC       isr.o
 AR       libbase.a
make: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/libbase'
make: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/libfatfs'
make: Nothing to be done for 'all'.
make: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/libfatfs'
make: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/liblitespi'
 CC       spiflash.o
 AR       liblitespi.a
make: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/liblitespi'
make: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/liblitedram'
 CC       sdram.o
 CC       bist.o
 CC       sdram_dbg.o
 CC       sdram_spd.o
 CC       utils.o
 CC       accessors.o
 AR       liblitedram.a
make: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/liblitedram'
make: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/libliteeth'
 CC       udp.o
 CC       mdio.o
 AR       libliteeth.a
make: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/libliteeth'
make: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/liblitesdcard'
 CC       sdcard.o
 CC       spisdcard.o
 AR       liblitesdcard.a
make: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/liblitesdcard'
make: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/liblitesata'
 CC       sata.o
 AR       liblitesata.a
make: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/liblitesata'
make: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/bios'
 CC       boot.o
 CC       cmd_bios.o
 CC       cmd_mem.o
 CC       cmd_boot.o
 CC       cmd_i2c.o
 CC       cmd_spiflash.o
 CC       cmd_litedram.o
 CC       cmd_liteeth.o
 CC       cmd_litesdcard.o
 CC       cmd_litesata.o
 CC       sim_debug.o
 CC       main.o
 CC       crt0.o
 CC       bios.elf
chmod -x bios.elf
 OBJCOPY  bios.bin
chmod -x bios.bin
python3 -m litex.soc.software.crcfbigen bios.bin --little
python3 -m litex.soc.software.memusage bios.elf /home/kevin/linux-on-litex-vexriscv/build/sim/software/bios/../include/generated/regions.ld riscv64-linux-gnu

ROM usage: 24.25KiB     (37.89%)
RAM usage: 1.36KiB      (16.99%)

rm crt0.o
make: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/software/bios'
INFO:SoC:Initializing ROM rom with contents (Size: 0x6104).
INFO:SoC:Auto-Resizing ROM rom from 0x10000 to 0x6104.
make: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/gateware'
mkdir -p modules
make -C modules -f /home/kevin/litex/litex/build/sim/core/modules/Makefile
make[1]: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/gateware/modules'
mkdir -p xgmii_ethernet
make MOD=xgmii_ethernet -C xgmii_ethernet -f /home/kevin/litex/litex/build/sim/core/modules/xgmii_ethernet/Makefile
make[2]: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/gateware/modules/xgmii_ethernet'
cc -c -Wall -O3 -ggdb -fPIC -Werror -I/home/kevin/pythondata-misc-tapcfg/pythondata_misc_tapcfg/data/src/include -I/home/kevin/litex/litex/build/sim/core/modules/xgmii_ethernet/../.. -o xgmii_ethernet.o /home/kevin/litex/litex/build/sim/core/modules/xgmii_ethernet/xgmii_ethernet.c
cc -Wall -O3 -ggdb -fPIC -Werror -I/home/kevin/pythondata-misc-tapcfg/pythondata_misc_tapcfg/data/src/include -c -o tapcfg.o /home/kevin/pythondata-misc-tapcfg/pythondata_misc_tapcfg/data/src/lib/tapcfg.c
cc -Wall -O3 -ggdb -fPIC -Werror -I/home/kevin/pythondata-misc-tapcfg/pythondata_misc_tapcfg/data/src/include -c -o taplog.o /home/kevin/pythondata-misc-tapcfg/pythondata_misc_tapcfg/data/src/lib/taplog.c
cc -levent -shared -fPIC -lz -Wl,-soname,xgmii_ethernet.so -o xgmii_ethernet.so xgmii_ethernet.o tapcfg.o taplog.o
make[2]: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/gateware/modules/xgmii_ethernet'
cp xgmii_ethernet/xgmii_ethernet.so xgmii_ethernet.so
mkdir -p ethernet
make MOD=ethernet -C ethernet -f /home/kevin/litex/litex/build/sim/core/modules/ethernet/Makefile
make[2]: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/gateware/modules/ethernet'
cc -c -Wall -O3 -ggdb -fPIC -Werror -I/home/kevin/pythondata-misc-tapcfg/pythondata_misc_tapcfg/data/src/include -I/home/kevin/litex/litex/build/sim/core/modules/ethernet/../.. -o ethernet.o /home/kevin/litex/litex/build/sim/core/modules/ethernet/ethernet.c
cc -Wall -O3 -ggdb -fPIC -Werror -I/home/kevin/pythondata-misc-tapcfg/pythondata_misc_tapcfg/data/src/include -c -o tapcfg.o /home/kevin/pythondata-misc-tapcfg/pythondata_misc_tapcfg/data/src/lib/tapcfg.c
cc -Wall -O3 -ggdb -fPIC -Werror -I/home/kevin/pythondata-misc-tapcfg/pythondata_misc_tapcfg/data/src/include -c -o taplog.o /home/kevin/pythondata-misc-tapcfg/pythondata_misc_tapcfg/data/src/lib/taplog.c
cc -levent -shared -fPIC -Wl,-soname,ethernet.so -o ethernet.so ethernet.o tapcfg.o taplog.o
make[2]: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/gateware/modules/ethernet'
cp ethernet/ethernet.so ethernet.so
mkdir -p serial2console
make MOD=serial2console -C serial2console -f /home/kevin/litex/litex/build/sim/core/modules/serial2console/Makefile
make[2]: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/gateware/modules/serial2console'
cc -c -Wall -O3 -ggdb -fPIC -Werror -I/home/kevin/litex/litex/build/sim/core/modules/serial2console/../.. -o serial2console.o /home/kevin/litex/litex/build/sim/core/modules/serial2console/serial2console.c
cc -levent -shared -fPIC -Wl,-soname,serial2console.so -o serial2console.so serial2console.o
rm serial2console.o
make[2]: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/gateware/modules/serial2console'
cp serial2console/serial2console.so serial2console.so
mkdir -p serial2tcp
make MOD=serial2tcp -C serial2tcp -f /home/kevin/litex/litex/build/sim/core/modules/serial2tcp/Makefile
make[2]: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/gateware/modules/serial2tcp'
cc -c -Wall -O3 -ggdb -fPIC -Werror -I/home/kevin/litex/litex/build/sim/core/modules/serial2tcp/../.. -o serial2tcp.o /home/kevin/litex/litex/build/sim/core/modules/serial2tcp/serial2tcp.c
cc -levent -shared -fPIC -Wl,-soname,serial2tcp.so -o serial2tcp.so serial2tcp.o
rm serial2tcp.o
make[2]: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/gateware/modules/serial2tcp'
cp serial2tcp/serial2tcp.so serial2tcp.so
mkdir -p clocker
make MOD=clocker -C clocker -f /home/kevin/litex/litex/build/sim/core/modules/clocker/Makefile
make[2]: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/gateware/modules/clocker'
cc -c -Wall -O3 -ggdb -fPIC -Werror -I/home/kevin/litex/litex/build/sim/core/modules/clocker/../.. -o clocker.o /home/kevin/litex/litex/build/sim/core/modules/clocker/clocker.c
cc -levent -shared -fPIC -Wl,-soname,clocker.so -o clocker.so clocker.o
rm clocker.o
make[2]: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/gateware/modules/clocker'
cp clocker/clocker.so clocker.so
mkdir -p spdeeprom
make MOD=spdeeprom -C spdeeprom -f /home/kevin/litex/litex/build/sim/core/modules/spdeeprom/Makefile
make[2]: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/gateware/modules/spdeeprom'
cc -c -Wall -O3 -ggdb -fPIC -Werror -I/home/kevin/litex/litex/build/sim/core/modules/spdeeprom/../.. -o spdeeprom.o /home/kevin/litex/litex/build/sim/core/modules/spdeeprom/spdeeprom.c
cc -levent -shared -fPIC -Wl,-soname,spdeeprom.so -o spdeeprom.so spdeeprom.o
rm spdeeprom.o
make[2]: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/gateware/modules/spdeeprom'
cp spdeeprom/spdeeprom.so spdeeprom.so
mkdir -p gmii_ethernet
make MOD=gmii_ethernet -C gmii_ethernet -f /home/kevin/litex/litex/build/sim/core/modules/gmii_ethernet/Makefile
make[2]: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/gateware/modules/gmii_ethernet'
cc -c -Wall -O3 -ggdb -fPIC -Werror -I/home/kevin/pythondata-misc-tapcfg/pythondata_misc_tapcfg/data/src/include -I/home/kevin/litex/litex/build/sim/core/modules/gmii_ethernet/../.. -o gmii_ethernet.o /home/kevin/litex/litex/build/sim/core/modules/gmii_ethernet/gmii_ethernet.c
cc -Wall -O3 -ggdb -fPIC -Werror -I/home/kevin/pythondata-misc-tapcfg/pythondata_misc_tapcfg/data/src/include -c -o tapcfg.o /home/kevin/pythondata-misc-tapcfg/pythondata_misc_tapcfg/data/src/lib/tapcfg.c
cc -Wall -O3 -ggdb -fPIC -Werror -I/home/kevin/pythondata-misc-tapcfg/pythondata_misc_tapcfg/data/src/include -c -o taplog.o /home/kevin/pythondata-misc-tapcfg/pythondata_misc_tapcfg/data/src/lib/taplog.c
cc -levent -shared -fPIC -lz -Wl,-soname,gmii_ethernet.so -o gmii_ethernet.so gmii_ethernet.o tapcfg.o taplog.o
make[2]: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/gateware/modules/gmii_ethernet'
cp gmii_ethernet/gmii_ethernet.so gmii_ethernet.so
mkdir -p jtagremote
make MOD=jtagremote -C jtagremote -f /home/kevin/litex/litex/build/sim/core/modules/jtagremote/Makefile
make[2]: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/gateware/modules/jtagremote'
cc -c -Wall -O3 -ggdb -fPIC -Werror -I/home/kevin/litex/litex/build/sim/core/modules/jtagremote/../.. -o jtagremote.o /home/kevin/litex/litex/build/sim/core/modules/jtagremote/jtagremote.c
cc -levent -shared -fPIC -Wl,-soname,jtagremote.so -o jtagremote.so jtagremote.o
rm jtagremote.o
make[2]: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/gateware/modules/jtagremote'
cp jtagremote/jtagremote.so jtagremote.so
make[1]: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/gateware/modules'
mkdir -p /home/kevin/linux-on-litex-vexriscv/build/sim/gateware/obj_dir
cc -c -ggdb -Wall -O3   -o /home/kevin/linux-on-litex-vexriscv/build/sim/gateware/obj_dir/modules.o /home/kevin/litex/litex/build/sim/core/modules.c
In file included from /usr/include/string.h:495,
                 from /home/kevin/litex/litex/build/sim/core/modules.c:5:
In function ‘strcat’,
    inlined from ‘tinydir_readfile’ at /home/kevin/litex/litex/build/sim/core/tinydir.h:532:2,
    inlined from ‘litex_sim_load_ext_modules’ at /home/kevin/litex/litex/build/sim/core/modules.c:68:14:
/usr/include/x86_64-linux-gnu/bits/string_fortified.h:128:10: warning: ‘__builtin___strcat_chk’ accessing 4097 or more bytes at offsets 0 and 4096 may overlap 1 byte at offset 4096 [-Wrestrict]
  128 |   return __builtin___strcat_chk (__dest, __src, __bos (__dest));
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
cc -c -ggdb -Wall -O3   -o /home/kevin/linux-on-litex-vexriscv/build/sim/gateware/obj_dir/pads.o /home/kevin/litex/litex/build/sim/core/pads.c
cc -c -ggdb -Wall -O3   -o /home/kevin/linux-on-litex-vexriscv/build/sim/gateware/obj_dir/sim.o /home/kevin/litex/litex/build/sim/core/sim.c
cc -c -ggdb -Wall -O3   -o /home/kevin/linux-on-litex-vexriscv/build/sim/gateware/obj_dir/libdylib.o /home/kevin/litex/litex/build/sim/core/libdylib.c
cc -c -ggdb -Wall -O3   -o /home/kevin/linux-on-litex-vexriscv/build/sim/gateware/obj_dir/parse.o /home/kevin/litex/litex/build/sim/core/parse.c
verilator -Wno-fatal -O3 --cc /home/kevin/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/Ram_1w_1rs_Generic.v --cc /home/kevin/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood.v --cc /home/kevin/linux-on-litex-vexriscv/build/sim/gateware/sim.v  --top-module sim --exe \
        -DPRINTF_COND=0 \
        sim_init.cpp /home/kevin/litex/litex/build/sim/core/veril.cpp modules.o pads.o sim.o libdylib.o parse.o \
        --top-module sim \
         \
        -CFLAGS "-ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core" \
        -LDFLAGS "-lpthread -Wl,--no-as-needed -ljson-c -lz -lm -lstdc++ -Wl,--no-as-needed -ldl -levent " \
        --trace \
         \
         \
        --unroll-count 256 \
        --output-split 5000 \
        --output-split-cfuncs 500 \
        --output-split-ctrace 500 \
         \
        -Wno-BLKANDNBLK \
        -Wno-WIDTH \
        -Wno-COMBDLY \
        -Wno-CASEINCOMPLETE \
        --relative-includes
%Warning-TIMESCALEMOD: /home/kevin/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/Ram_1w_1rs_Generic.v:2:8: Timescale missing on this module as other modules have it (IEEE 1800-2017 3.14.2.3)
    2 | module Ram_1w_1rs #(
      |        ^~~~~~~~~~
                       /home/kevin/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood.v:7:8: ... Location of module with timescale
    7 | module VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood (
      |        ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
                       ... For warning description see https://verilator.org/warn/TIMESCALEMOD?v=5.009
                       ... Use "/* verilator lint_off TIMESCALEMOD */" and lint_on around source to disable this message.
make -j -C /home/kevin/linux-on-litex-vexriscv/build/sim/gateware/obj_dir -f Vsim.mk Vsim
make[1]: Entering directory '/home/kevin/linux-on-litex-vexriscv/build/sim/gateware/obj_dir'
g++  -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -Os -c -o veril.o /home/kevin/litex/litex/build/sim/core/veril.cpp
g++  -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -Os -c -o sim_init.o ../sim_init.cpp
g++ -Os  -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o verilated.o /home/kevin/verilator/include/verilated.cpp
g++ -Os  -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o verilated_dpi.o /home/kevin/verilator/include/verilated_dpi.cpp
g++ -Os  -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o verilated_vcd_c.o /home/kevin/verilator/include/verilated_vcd_c.cpp
g++ -Os  -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o verilated_threads.o /home/kevin/verilator/include/verilated_threads.cpp
g++ -Os  -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim.o Vsim.cpp
g++ -Os  -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim___024root__DepSet_h104c642d__0.o Vsim___024root__DepSet_h104c642d__0.cpp
g++ -Os  -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim___024root__DepSet_hb1836b75__0.o Vsim___024root__DepSet_hb1836b75__0.cpp
g++ -Os  -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim_sim__DepSet_h837b84dc__0.o Vsim_sim__DepSet_h837b84dc__0.cpp
g++ -Os  -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim_sim__DepSet_h40728c06__0.o Vsim_sim__DepSet_h40728c06__0.cpp
g++ -Os  -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim_sim__DepSet_h40728c06__1.o Vsim_sim__DepSet_h40728c06__1.cpp
g++ -Os  -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim_VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood__DepSet_h700cc5f3__0.o Vsim_VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood__DepSet_h700cc5f3__0.cpp
g++ -Os  -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim_VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood__DepSet_he9900fa0__0.o Vsim_VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood__DepSet_he9900fa0__0.cpp
g++ -Os  -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim_VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood__DepSet_he9900fa0__1.o Vsim_VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood__DepSet_he9900fa0__1.cpp
g++ -Os  -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim_VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood__DepSet_he9900fa0__2.o Vsim_VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood__DepSet_he9900fa0__2.cpp
g++ -Os  -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim_VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood__DepSet_he9900fa0__3.o Vsim_VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood__DepSet_he9900fa0__3.cpp
g++ -Os  -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim_VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood__DepSet_he9900fa0__4.o Vsim_VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood__DepSet_he9900fa0__4.cpp
g++ -Os  -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim_VexRiscv__DepSet_hda50bfa8__0.o Vsim_VexRiscv__DepSet_hda50bfa8__0.cpp
g++ -Os  -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim_VexRiscv__DepSet_h9f7c89a9__0.o Vsim_VexRiscv__DepSet_h9f7c89a9__0.cpp
g++ -Os  -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim_VexRiscv__DepSet_h9f7c89a9__1.o Vsim_VexRiscv__DepSet_h9f7c89a9__1.cpp
g++ -Os  -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim_VexRiscv__DepSet_h9f7c89a9__2.o Vsim_VexRiscv__DepSet_h9f7c89a9__2.cpp
g++ -Os  -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim__Dpi.o Vsim__Dpi.cpp
g++ -Os  -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim__Trace__0.o Vsim__Trace__0.cpp
g++ -Os  -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim__Trace__1.o Vsim__Trace__1.cpp
g++ -Os  -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim__Trace__2.o Vsim__Trace__2.cpp
g++   -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim__ConstPool_0.o Vsim__ConstPool_0.cpp
g++   -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim__ConstPool_1.o Vsim__ConstPool_1.cpp
g++   -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim___024root__Slow.o Vsim___024root__Slow.cpp
g++   -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim___024root__DepSet_h104c642d__0__Slow.o Vsim___024root__DepSet_h104c642d__0__Slow.cpp
g++   -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim___024root__DepSet_hb1836b75__0__Slow.o Vsim___024root__DepSet_hb1836b75__0__Slow.cpp
g++   -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim_sim__Slow.o Vsim_sim__Slow.cpp
g++   -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim_sim__DepSet_h837b84dc__0__Slow.o Vsim_sim__DepSet_h837b84dc__0__Slow.cpp
g++   -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim_sim__DepSet_h837b84dc__1__Slow.o Vsim_sim__DepSet_h837b84dc__1__Slow.cpp
g++   -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim_sim__DepSet_h40728c06__0__Slow.o Vsim_sim__DepSet_h40728c06__0__Slow.cpp
g++   -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim_sim__DepSet_h40728c06__1__Slow.o Vsim_sim__DepSet_h40728c06__1__Slow.cpp
g++   -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim_VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood__Slow.o Vsim_VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood__Slow.cpp
g++   -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim_VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood__DepSet_h700cc5f3__0__Slow.o Vsim_VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood__DepSet_h700cc5f3__0__Slow.cpp
g++   -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim_VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood__DepSet_he9900fa0__0__Slow.o Vsim_VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood__DepSet_he9900fa0__0__Slow.cpp
g++   -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim_VexRiscv__Slow.o Vsim_VexRiscv__Slow.cpp
g++   -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim_VexRiscv__DepSet_hda50bfa8__0__Slow.o Vsim_VexRiscv__DepSet_hda50bfa8__0__Slow.cpp
g++   -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim_VexRiscv__DepSet_hda50bfa8__1__Slow.o Vsim_VexRiscv__DepSet_hda50bfa8__1__Slow.cpp
g++   -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim_VexRiscv__DepSet_h9f7c89a9__0__Slow.o Vsim_VexRiscv__DepSet_h9f7c89a9__0__Slow.cpp
g++   -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim__Syms.o Vsim__Syms.cpp
g++   -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim__Trace__0__Slow.o Vsim__Trace__0__Slow.cpp
g++   -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim__Trace__1__Slow.o Vsim__Trace__1__Slow.cpp
g++   -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim__Trace__2__Slow.o Vsim__Trace__2__Slow.cpp
g++   -I.  -MMD -I/home/kevin/verilator/include -I/home/kevin/verilator/include/vltstd -DVM_COVERAGE=0 -DVM_SC=0 -DVM_TRACE=1 -DVM_TRACE_FST=0 -DVM_TRACE_VCD=1 -faligned-new -fcf-protection=none -Wno-bool-operation -Wno-sign-compare -Wno-uninitialized -Wno-unused-but-set-variable -Wno-unused-parameter -Wno-unused-variable -Wno-shadow     -ggdb -Wall -O3   -I/home/kevin/litex/litex/build/sim/core   -c -o Vsim__Trace__3__Slow.o Vsim__Trace__3__Slow.cpp
echo "" > Vsim__ALL.verilator_deplist.tmp
Archive ar -rcs Vsim__ALL.a Vsim.o Vsim___024root__DepSet_h104c642d__0.o Vsim___024root__DepSet_hb1836b75__0.o Vsim_sim__DepSet_h837b84dc__0.o Vsim_sim__DepSet_h40728c06__0.o Vsim_sim__DepSet_h40728c06__1.o Vsim_VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood__DepSet_h700cc5f3__0.o Vsim_VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood__DepSet_he9900fa0__0.o Vsim_VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood__DepSet_he9900fa0__1.o Vsim_VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood__DepSet_he9900fa0__2.o Vsim_VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood__DepSet_he9900fa0__3.o Vsim_VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood__DepSet_he9900fa0__4.o Vsim_VexRiscv__DepSet_hda50bfa8__0.o Vsim_VexRiscv__DepSet_h9f7c89a9__0.o Vsim_VexRiscv__DepSet_h9f7c89a9__1.o Vsim_VexRiscv__DepSet_h9f7c89a9__2.o Vsim__Dpi.o Vsim__Trace__0.o Vsim__Trace__1.o Vsim__Trace__2.o Vsim__ConstPool_0.o Vsim__ConstPool_1.o Vsim___024root__Slow.o Vsim___024root__DepSet_h104c642d__0__Slow.o Vsim___024root__DepSet_hb1836b75__0__Slow.o Vsim_sim__Slow.o Vsim_sim__DepSet_h837b84dc__0__Slow.o Vsim_sim__DepSet_h837b84dc__1__Slow.o Vsim_sim__DepSet_h40728c06__0__Slow.o Vsim_sim__DepSet_h40728c06__1__Slow.o Vsim_VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood__Slow.o Vsim_VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood__DepSet_h700cc5f3__0__Slow.o Vsim_VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ldw32_Ood__DepSet_he9900fa0__0__Slow.o Vsim_VexRiscv__Slow.o Vsim_VexRiscv__DepSet_hda50bfa8__0__Slow.o Vsim_VexRiscv__DepSet_hda50bfa8__1__Slow.o Vsim_VexRiscv__DepSet_h9f7c89a9__0__Slow.o Vsim__Syms.o Vsim__Trace__0__Slow.o Vsim__Trace__1__Slow.o Vsim__Trace__2__Slow.o Vsim__Trace__3__Slow.o
g++    veril.o sim_init.o verilated.o verilated_dpi.o verilated_vcd_c.o verilated_threads.o Vsim__ALL.a   modules.o pads.o sim.o libdylib.o parse.o -lpthread -Wl,--no-as-needed -ljson-c -lz -lm -lstdc++ -Wl,--no-as-needed -ldl -levent  -pthread -lpthread -latomic   -o Vsim
rm Vsim__ALL.verilator_deplist.tmp
make[1]: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/gateware/obj_dir'
make: Leaving directory '/home/kevin/linux-on-litex-vexriscv/build/sim/gateware'

[xgmii_ethernet] loaded (0x5636122c5ef0)
[gmii_ethernet] loaded (0x5636122c5ef0)
[jtagremote] loaded (0x5636122c5ef0)
[spdeeprom] loaded (addr = 0x0)
[clocker] loaded
[serial2tcp] loaded (0x5636122c5ef0)
[serial2console] loaded (0x5636122c5ef0)
[ethernet] loaded (0x5636122c5ef0)
[clocker] sys_clk: freq_hz=1000000, phase_deg=0

        __   _ __      _  __
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
