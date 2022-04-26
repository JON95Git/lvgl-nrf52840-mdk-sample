# zephyr-lvgl-nrf52840-mdk-sample
A simple example of how to use a [LVGL](https://lvgl.io/) widget in 
Zephyr RTOS running on a [nRF52840_mdk](https://wiki.makerdiary.com/nrf52840-mdk/)
board and a `ST7789 - 240x240 IPS` display

# Tests
It was tested in a `nRF52840_mdk` board.

# Pinout

| nRF52840_mdk |   ST7789   |
|--------------|------------|
|     P0.28    |    RES     |
|     P0.29    |  DC (CMD)  |
|     P0.27    |  SCK (SCL) |
|     P0.26    | MOSI (SDA) |

# How to build
```
$ west build -p auto -b nrf52840_mdk
```

# How to flash
```
$ west flash
```
# Application running

![capture](nrf52840-st7789-lvgl.gif)
