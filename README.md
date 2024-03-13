# Android13

- Kernel version: 5.15
- Released year: 2023
- Android support by Adlink(continuing).
  

## 2. Supported Modules

- LEC-MTK-I1200


## 3. Supported Features & Interfaces

### 3.1 LEC-MTK1200 (based on I-Pi SMARC plus carrier + LEC-MTK1200 Dev Kit)

| Interfaces                                 | Support |
| ------------------------------------------ | ------- |
| RAM [LPDDR4(2G/4G/8G)]                     | Y       |
| MIPI-DSI [auo-B101UAN01]                   | Y       |
| Cameras [imx214]                           | Y       |
| GPU                                        | Y       |
| HDMI                                       | Y       |
| UFS                                        | Y       |
| Debug Header                               | Y       |
| Audio [tlv320aic3x]                        | Y       |
| Video                                      | Y       |
| Ethernet - 0 & 1                           | Y       |
| Wi-Fi(optional) [Azurewave AW-CM276NF]     | Y       |
| PCIe                                       | Y       |
| USB 2.0                                    | Y       |
| USB 3.0                                    | Y       |
| SER                                        | Y       |
| CAN                                        | Y       |
| SPI                                        | Y       |
| I2S (Audio TLV320 codec )                  | Y       |
| I2C                                        | Y       |
| GPIO                                       | Y       |
| SDIO                                       | Y       |



## 4. Documentation

Refer to the [wiki](https://github.com/AdlinkCCoE/mtk_1200_android/blob/main/INSTALL.md) page for instructions on building the Android13 as well as flashing the image.

## 5. Known Issues

- Blutooth (UART mode)
- NPU (Not fully validated)
