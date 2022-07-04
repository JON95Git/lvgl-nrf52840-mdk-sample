# zephyr-lvgl-nrf52840-mdk-sample
A simple example of how to use a [LVGL](https://lvgl.io/) widget in 
Zephyr RTOS running on a [nRF52840_mdk](https://wiki.makerdiary.com/nrf52840-mdk/)
board and a `ST7789 - 240x240 IPS` display

# Tests
It was tested in a `nRF52840_mdk` board.

# Driver change
In order to get this display working properly, you have to change
`zephyr/drivers/display/display_st7789v.c (line 422)`:

From
```
#define ST7789V_INIT(inst)                                              \
    static const struct st7789v_config st7789v_config_ ## inst = {      \
        .bus = SPI_DT_SPEC_INST_GET(inst, SPI_OP_MODE_MASTER |          \
                              SPI_WORD_SET(8), 0),                      \
```

To

```
#define ST7789V_INIT(inst)                                               \
    static const struct st7789v_config st7789v_config_ ## inst = {       \
        .bus = SPI_DT_SPEC_INST_GET(inst, SPI_OP_MODE_MASTER |           \
        SPI_WORD_SET(8) | SPI_TRANSFER_MSB | SPI_MODE_CPOL, 0),          \
```

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
