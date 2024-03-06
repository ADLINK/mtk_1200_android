ADLINK LEC-MTK-i1200 module with Android 13 BSP
===============================================
Platform : Lec-MTK1200	
Kernel Version : 5.15

Change Log
==========

0v1
---
 - Android Serial Console
 - GPIO


UART Console
------------

 - Install minicom or using USB-RS232 Serial cable 
 - Connect TX and RX pins
 - CN1602 => TX-3 : RX-1
 - Console Settings : 921600 8N1

GPIO
-----

 - $cd /sys/class/gpio/ 
 - $echo 314 > export
 - $cd /sys/class/gpio/gpio314/
 - To find the direction
 - $cat direction
 - To find the value
 - $cat valueTo change the direction
 - $echo out > direction for setting pin direction output
 - $echo in > direction for setting pin direction input
 - To change the Value 
 - $set value echo 0 > value (to value set low)
 - $set value echo 1 > value (to value set high)

 - we  can Validate GPIO using  below Sysfs number for 
 - respective GPIO pin of CN1001 header of iPI-Smarc Plus

 - Sno	Name	      CN1001	  Sysfs
 - 1	S_GPIO07_3V 	 Pin12	  314	
 - 2	S_GPIO08_3V	 Pin11	  315	
 - 3	S_GPIO09_3V	 Pin13	  316	
 - 4	S_GPIO10_3V	 Pin15	  317	
 - 5	S_GPIO11_3V	 Pin16	  326	
 - 6	S_GPIO12_3V	 Pin18	  327
 - 7	S_GPIO13_3V	 Pin22	  328	
 - 8	E_GPIO1_0	 Pin29	  330	
 - 9	E_GPIO1_1	 Pin31	  331	
 - 10	E_GPIO1_2	 Pin32	  332	
 - 11	E_GPIO1_3	 Pin33	  333	
 - 12	E_GPIO1_4	 Pin35	  334	
 - 13	E_GPIO1_5	 Pin36	  335	
 - 14	E_GPIO1_6	 Pin37	  336	
 - 15	E_GPIO1_7	 Pin38	  337	
 - 16	E_GPIO1_8	 Pin40	  338

0v2
---
 - USB Host support with HID / Mass storage
 - Ethernet (eth0)

USB
---
 - When attached and detache USB storage device  its shown dmesg
 - We can also find the device in lsusb.
 - USB HID Mouse, keyboard & Mass Storage are supported

Ethernet
--------
 - eth0  => USB to Ethernet Convertor - lan78xx


0v3
---

 - HDMI

HDMI
----
 - Connect the Display ports to HDMI port on board
 - HDMI Display start with android logo.

 - 1|console:/ # cat /sys/class/drm/card0-HDMI-A-1/status
 - connected


0v4
---

 - CAN
 - SPI
 - USB OTG

CAN
---

 - Setup CAN0 : Conn CN1602 => connect 13 & 15 with another CAN Terminal

1) Configure the CAN0 ports as

   - ip link set can0 type can bitrate 500000

   - ip link set can0 up

2) Dump CAN data on can0:
   - candump can0 &


3) Send data over can1:

   - cansend can1 01a#11223344AABBCCDD

SPI
---

  - Setup SPI :  Conn CN1602 -> short MOSI 27 & MISO 28 pins.

  - spidevtest -D /dev/spidev1.0 -v


USB OTG
---

Host machine

1)Command adb devices

  - shows List of devices attached

    List of devices attached
    0123456789ABCDEF	device

2)adb shell

  - adb shell would appear 
    aiot8395p1_64_bsp:/ $


0v5
---

 - PCIe
 - WiFi

PCIe
---

1)PCIe host tested using lspci

 - Command lspci

	console:/ # lspci                                                          
	00:00.0 :   (rev 01)
	01:00.0 :   (rev 11)

Wifi
---
 - Aw-CM276NF Wifi support.
 - Wifi working with Android UI.
    

0v6
---

 - Camera imx214

Camera
---
 - Camera support for imx214.
 - Connect Smarc CN1802 CSI-4 lanes with Trasferboard CN602 connector  
 - Validated camera using Android UI


0v7
---
 - Wifi scan fix

0v8
---
 - DSI-Display B101UAN01
 - DSI panel connected dsi0 connect on smarc
 note: works parallely with HDMI display

0v9
---

 - Audio TLV320 codec support added	
 - playback 
   
   ```Shell
   su
   tinymix -D 0 'O072 I070 Switch'  1
   tinymix -D 0 'O073 I071 Switch' 1
   tinyplay /vendor/res/sound/ringtone.wav -D 0 -d 0
   ```
 - for playback Audio from DSI plannel
   
   ```Shell
   su
   tinymix -D 0 'O072 I020 Switch'  1
   tinymix -D 0 'O073 I021 Switch' 1
   ```
 - Capture
   
    Syntax #tinycap /data/rec.wav -D 0 -d 9 <frequency> -b 32 -T 4
   
   ```Shell
   tinycap /data/rec.wav -D 0 -d 9 -r 192000 -b 32 -T 4
   Capturing sample: 2 ch, 192000 hz, 32 bit
   Captured 757760 frames
   ```

0v10
---
 - eth1  =>RGMII -Rdwmac-mediatek

 - Connect the Lan cable to Ethernet port

Known issues:
---

 - Bluetooth not working
