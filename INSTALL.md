ADLINK LEC-MTK-1200_android   Module with iPI SMARC plus Android 13 BSP

Prerequisites
===========


### Hardware :

```
Module      : Target device(I-Pi SMARC 1200)
Base Board  : I-Pi SMARC Plus A3
Power cable
USB to Micro cable.
```

Note: For I-Pi SMARC 1200, the boot switch must be **1001** on the target device.

### Host machine :

- Machine: x86

- The Linux host must be Ubuntu 20.04 or later,

-  RAM: Minimum of 16 GB RAM.

-  Storage : 900GB

Host Machine Setup
==================================================================
Installing Dependency Packages
------------------------------------

Use the following commands to install the dependency packages.

```Shell
sudo apt-get install gawk wget git-core diffstat unzip texinfo gcc-multilib

sudo apt-get install build-essential chrpath socat cpio python python3 python3-pip python3-pexpect

sudo apt-get install xz-utils debianutils iputils-ping python3-git python3-jinja2 libegl1-mesa libsdl1.2-dev pylint xterm

sudo apt-get install flex bison

sudo apt-get install libncurses5-dev

sudo apt-get install libncurses5

sudo add-apt-repository ppa:ubuntu-toolchain-r/test

sudo apt-get install libstdc++6

sudo dpkg --add-architecture i386

sudo apt update

sudo apt install zlib1g:i386

sudo apt install zlib1g-dev:i386
```

Git Setup
---------
Use the following commands for git configuration.

```Shell
git config --global user.name "First Last"
git config --global user.email "first.last@company.com"
```

Python setup
---------------------
Use the following commands for Python configuration.

- Install python2.7
	
	```Shell
	sudo apt install python2 -y
	
	sudo apt install software-properties-common
	
	sudo add-apt-repository ppa:deadsnakes/ppa
	
	sudo apt update
	```
	
	
	
- Configure python2.7 as default python
	
	```Shell
	sudo apt install python2
	
	sudo update-alternatives --install /usr/bin/python python /usr/bin/python2.7 1
	
	sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.10 2
	
	sudo update-alternatives -- config python
	```
	
	Then select `1` ( to configure python2.7 as default python)

Download the source from Mediatek 
==================================================================

- Create a new folder and initiate the repository using below commands 

  ```shell
  mkdir ~/android_bsp/
  cd ~/android_bsp
  repo init -u https://wtmec-aiot-git01-user@git01.mediatek.com/alps_release/platform/manifest -b wtmec -m t-alps-release-t0.mp5-aiot-V5.5.3.xml --no-repo-verify
  repo sync -c -f -j8 --no-repo-verify --optimized-fetch
  
  ```

  **Note:** 
  1. For access contact [wtmec/ipi.wiki@adlinktech.com](wtmec/ipi.wiki@adlinktech.com)
  2. BSP needs to be on a case-sensitive file system such as ext4 else may cause build error.
  
  

Build Instructions
==================================================================

To Compile the Android BSP
------------------------------

After downloading BSP, compile the source using following command

```Shell
cd ~/android_bsp/

vendor/mediatek/proprietary/scripts/releasetools/split_build_helper.py --run full_aiot8395p1_64_bsp-userdebug > build_log.txt
```

On successfully compilation, a message mentioning `build completed successfully` will be displayed 

Note: It is recommended to compile the base version, before proceeding with patches .

- Git clone the patches from git to the Android13 project folder 

  ```shell
  cd ~/android_bsp
  git clone https://github.com/ADLINK/mtk_1200_android -b Android13
  ```

   For access contact :[ipi.wiki@adlinktech.com](ipi.wiki@adlinktech.com)

  

- Copy-Paste the `mtk_1200_android-main/mtk_base` patches to `android_bsp` folder 

  ```Shell
  cd ~/android_bsp
  cp mtk_base_patches/*  ~/android_bsp/
  ```

- Apply mtk_base patches

  ```Shell
  cd ~/android_bsp/
  git apply 0001-Disable-HDCP-AAL-git-check.patch
  git apply 0002-Enable-UFS-boot-device.patch
  git apply 0003-Ignore-enter-factory-mode-and-boot-to-kernel.patch
  git apply 0004-Disable-thermal-AUXADC.patch
  ```

- Copy-Paste the patches from `mtk_1200_android-main/bionic` patches to `~/android_bsp/bionic/`

  ```Shell
  cd ~/android_bsp/
  cp mtk_1200_android-main/bionic/* ~/android_bsp/bionic/
  ```

- Apply bionic patches

  ```Shell
  cd ~/android_bsp/bionic/
  git apply 00*
  ```

- Copy-Paste the patches from `mtk_1200_android-main/build` to `~/android_bsp/build`

  ```Shell
  cd ~/android_bsp/
  cp mtk_1200_android-main/build/* ~/android_bsp/build/
  ```

- Apply build patches

  ```Shell
  cd ~/android_bsp/build/
  git apply 00*
  ```

- Copy-Paste the patches from `mtk_1200_android-main/device` to `~/android_bsp/device/`

  ```Shell
  cd ~/android_bsp/
  cp mtk_1200_android-main/device/* ~/android_bsp/device/
  ```

- Apply device patches 

  ```Shell
  cd ~/android_bsp/device/
  git apply 00*
  ```

- Copy-Paste the patches from `mtk_1200_android-main/external`  to `~/android_bsp/external/`

  ```Shell
  cd ~/android_bsp/
  cp mtk_1200_android-main/external/* ~/android_bsp/external/
  ```

- Apply external patches 

  ```shell
  cd ~/android_bsp/external/
  git apply 00*
  ```

- Copy-Paste the patches from `mtk_1200_android-main/kernel-5.15` to `~/alps-release-t0.mp5-aiot-V5.5.3/kernel-5.15/`

  ```Shell
  cd ~/android_bsp/
  cp mtk_1200_android-main/kernel-5.15 /* ~/android_bsp/kernel-5.15/
  ```

- Apply kernel-5.15 patches

  ```shell
  cd ~/android_bsp/kernel-5.15/
  git apply 00*
  ```

- Copy-Paste the patches from `mtk_1200_android-main/vendor`  to `~/alps-release-t0.mp5-aiot-V5.5.3/vendor/`

  ```Shell
  cd ~/android_bsp/
  cp mtk_1200_android-main/vendor/* ~/android_bsp/vendor/
  ```

- Apply vendor patches 

  ```Shell
  cd ~/android_bsp/vendor/
  git apply 00*
  ```
  
- For adding   Chrome-apk to BSP
  
  ```shell
  cp ~/mtk_1200_android-main/prebuilt-apk/0002-build_adding_chrome.patch ~/android_bsp/build/0002-build_adding_chrome.patch
  cp ~/mtk_1200_android-main/prebuilt-apk/0003-vendor_adding_chrome.patch ~/android_bsp/vendor/0003
   vendor_adding_chrome.patch
  git apply ~/android_bsp/vendor/0003-vendor_adding_chrome.patch
  git apply ~/android_bsp/build/0002-build_adding_chrome.patch
  #Download prebuilt APK
  cd ~/
  wget https://hq0epm0west0us0storage.blob.core.windows.net/development/MTK-LEC-I1200/android/chrome-120.apk
  cp ~/chrome-120. apk vendor/mediatek/proprietary/system/Chrome/
  ```
  
- After applying all patches, rebuild the source
  
  ```shell
  cd ~/android_bsp/
  vendor/mediatek/proprietary/scripts/releasetools/split_build_helper.py --run full_aiot8395p1_64_bsp-userdebug > build_log.txt
  ```

Note: Compilation log could be located at `~/android_bsp/build_log.txt` for debugging.

Image Path
--------------------------------------

Image will be generate in the  path : `out/target/product/aiot8395p1_64_bsp/merged/`

```Shell
ls alps-release-t0.mp5-aiot-V5.5.3/out/target/product/aiot8395p1_64_bsp/merged/
1__LEC-MTK-i1200-32G-Android-13_1V1.0.0_24_01_02.zip  LEC-MTK-i1200-4G-Android-13_1V1.0.0_24_01_02.zip  preloader.img      system_other.img
APDB_MT8195_S01__W2310                                lk.img                                            preloader_raw.img  target_files.zip
APDB_MT8195_S01__W2310_ENUM                           logo.img                                          preloader_ufs.img  tee.img
apusys.img                                            mcupm.img                                         product.img        testcases
boot-debug.img                                        md1dsp.img                                        product.map        userdata.img
boot.img                                              md1img.img                                        scp.img            vbmeta.img
cam_vpu1.img                                          MT8195_Android_scatter.txt                        spmfw.img          vbmeta_system.img
cam_vpu2.img                                          MT8195_Android_scatter.xml                        sspm.img           vbmeta_vendor.img
cam_vpu3.img                                          mtk_unsigned_images                               super_empty.img    vendor_boot-debug.img
dpm.img                                               odm_dlkm.img                                      super.img          vendor_boot.img
dtbo.img                                              odm_dlkm.map                                      system_dlkm.img    vendor_dlkm.img
init_boot.img                                         pi_img.img                                        system_dlkm.map    vendor_dlkm.map
installed-files-ramdisk.txt                           preloader_aiot8395p1_64_bsp.bin                   system.img         vendor.img
installed-files-vendor.txt                            preloader_emmc.img                                system.map         vendor.map
```



Flash Procedure for Android 13 LEC-MTK
==================================================================

USB Setup
---------
For Ubuntu host system --> Add rules for ADB & flash_tool to identify the MTK device.

```Shell
sudo gedit /etc/udev/rules.d/53-android.rules
SUBSYSTEM=="usb", SYSFS{idVendor}=="0bb4", MODE="0666"
SUBSYSTEM=="usb", ATTR{idVendor}="0bb4", ATTR{idProduct}="0c03", SYMLINK+="android_adb"

sudo gedit /etc/udev/rules.d/53-MTKinc.rules
SUBSYSTEM=="usb", SYSFS{idVendor}=="0e8d", MODE="0666"
SUBSYSTEM=="usb", ATTR{idVendor}="0e8d", ATTR{idProduct}="2000", SYMLINK+="android_adb"
KERNEL=="ttyACM*", MODE="0666"

sudo chmod a+rx /etc/udev/rules.d/53-android.rules
sudo chmod a+rx /etc/udev/rules.d/53-MTKinc.rules
sudo /etc/init.d/udev restart
sudo apt-get remove modemmanager
sudo /etc/init.d/udev restart
```



Download the Flash Tool
----------------------

- Download the  Flash Tool from [Download SP-Flash-Tool](https://hq0epm0west0us0storage.blob.core.windows.net/$web/public/SMARC/LEC-1200/Tools/SP_Flash_Tool_Selector_exe_Linux_v1.2308.00.100.tar.xz).

- Extract the contents of the downloaded `SP_Flash_Tool_Selector_exe_Linux_.zip` file into your preferred directory.

- Turn on the target device and connect the USB cable from the host device to the target device.

- Download the pre-built image from [https://www.ipi.wiki/pages/i-pi-smarc-1200-download](https://www.ipi.wiki/pages/i-pi-smarc-1200-download) Latest image under **Android**

  

Flashing Procedure
----------------

- For I-Pi SMARC 1200, the boot switch must be **1001** on the target device.

- unzip the Flash tool

  
  
  ```shell
   tar -xf SP_Flash_Tool_Selector_exe_Linux_v1.2308.00.100.tar.xz
   cd SP_Flash_Tool_Selector_exe_Linux_v1.2308.00.100/SP_Flash_Tool_V5
   ./flash_tool
  ```
  
  1. Scatter loading File : use Choose button to select the MT8195_Android_scatter.txt (Figure 1)

      ```
      Path Scatter-loading File: alps-release-t0.mp5-aiot-V5.5.3/out/target/product/aiot8395p1_64_bsp/merged/MT8195_Android_scatter.txt
      
      Download-Agent : SP_Flash_Tool_Selector_exe_Linux_v1.2308.00.100/SP_Flash_Tool_V5/MTK_AllInOne_DA.bin
      ```
      
  2. Select `Format All+ Download` in Drop down box.
  
  3. Connect `LEC-MTKi1200` and host machine using USB OTG and click the `Download` button in the flash tool.
  
  4. Press the `Reset` button on LEC-MTKi1200 to initiate the flashing of the image.
  
  5. Once the flash completes successfully, the prompt `Download OK` will appear
  
  6. Press the `Reset` button for booting the Android.
  
  7. Navigate to Settings --> About Phone to check the Android version
  

