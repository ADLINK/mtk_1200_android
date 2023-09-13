ADLINK LEC-MTK-1200_android   Module with iPI SMARC plus Android 13 BSP
==================================================================

Preparation
===========

Installing Dependency Packages
--------------------------------

- sudo apt-get install gawk wget git-core diffstat unzip texinfo gcc-multilib
- sudo apt-get install build-essential chrpath socat cpio python python3 python3-pip python3-pexpect 
- sudo apt-get install xz-utils debianutils iputils-ping python3-git python3-jinja2 libegl1-mesa libsdl1.2-dev pylint xterm 
- sudo apt-get install flex bison
- sudo apt-get install libncurses5-dev 
- sudo apt-get install libncurses5
- sudo add-apt-repository ppa:ubuntu-toolchain-r/test
- sudo apt-get install libstdc++6

Git Setup
---------

- git config --global user.name "First Last"
- git config --global user.email "first.last@company.com"

To setup PYTHON
---------------------

- Install python2.7
	- sudo apt install python2 -y
	- sudo apt install software-properties-common
	- sudo add-apt-repository ppa:deadsnakes/ppa
	- sudo apt update

- Change python2.7 as defult python
	- sudo update-alternatives --config python

To download the source from Mediatek
-------------------------------

- Method for Sharing BSP with customer is under dissusion 
- BSP is in  folder  alps-release-t0.mp5-aiot-V5.5.3/ 

To apply the patches
--------------------

- cp https://github.com/ADLINK/mtk_1200_android/tree/main/mtk_base_patches/ ~/alps-release-t0.mp5-aiot-V5.5.3/
- cd ~/alps-release-t0.mp5-aiot-V5.5.3/
- git apply 0001-Disable-HDCP-AAL-git-check.patch
- git apply 0002-Enable-UFS-boot-device.patch
- git apply 0003-Ignore-enter-factory-mode-and-boot-to-kernel.patch
- git apply 0004-Disable-thermal-AUXADC.patch 

- cp https://github.com/ADLINK/mtk_1200_android/tree/main/bionic/0001-bionic.patch  ~/alps-release-t0.mp5-aiot-V5.5.3/bionic/
- cd ~/alps-release-t0.mp5-aiot-V5.5.3/bionic/
- git apply 0001-bionic.patch

- cp https://github.com/ADLINK/mtk_1200_android/blob/main/build/0001-build.patch  ~/alps-release-t0.mp5-aiot-V5.5.3/build/
- cd ~/alps-release-t0.mp5-aiot-V5.5.3/build/
- git apply 0001-build.patch

- cp https://github.com/ADLINK/mtk_1200_android/blob/main/device/0001-device.patch ~/alps-release-t0.mp5-aiot-V5.5.3/device/
- cd ~/alps-release-t0.mp5-aiot-V5.5.3/device/
- git apply 0001-device.patch

- cp https://github.com/ADLINK/mtk_1200_android/blob/main/external/0001-external.patch ~/alps-release-t0.mp5-aiot-V5.5.3/external/
- cd ~/alps-release-t0.mp5-aiot-V5.5.3/external/
- git apply 0001-external.patch

- cp https://github.com/ADLINK/mtk_1200_android/blob/main/kernel-5.15/0001-kernel-5.15.patch ~/alps-release-t0.mp5-aiot-V5.5.3/kernel-5.15/
- cd ~/alps-release-t0.mp5-aiot-V5.5.3/kernel-5.15/
- git apply 0001-kernel-5.15.patch

- https://github.com/ADLINK/mtk_1200_android/blob/main/vendor/0001-vendor.patch ~/alps-release-t0.mp5-aiot-V5.5.3/vendor/
- cd ~/alps-release-t0.mp5-aiot-V5.5.3/vendor/
- git apply 0001-vendor.patch


To Compile the Android 13 BSP
------------------------------

- $ cd alps-release-t0.mp5-aiot-V5.5.3/
- $ vendor/mediatek/proprietary/scripts/releasetools/split_build_helper.py --run full_aiot8395p1_64_bsp-userdebug

