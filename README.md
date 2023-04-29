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
