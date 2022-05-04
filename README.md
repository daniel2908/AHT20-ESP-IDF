# _AHT20 driver for the ESP-IDF framework_

A simple driver for the esp32 using the IDF framework, currently assuming i2c mode is set to master and missing some functionality like interrupts and some RTOS things. Provided is an example labeled _main.c_ as well as a module that can be found in the _/components/AHT20_ folder.



## How to use example

```
static i2c_config_t aht20_i2c_conf = {
    .mode = I2C_MODE_MASTER,
    .sda_io_num = 16, //default pin for SDA
    .scl_io_num = 17, //default pin for SCL
    .sda_pullup_en = GPIO_PULLUP_DISABLE,
    .scl_pullup_en = GPIO_PULLUP_DISABLE,
    .master.clk_speed = 100000
};

void aht20_init(gpio_num_t clock, gpio_num_t data) {
    vTaskDelay(1000 / portTICK_PERIOD_MS);
    aht20_i2c_conf.sda_io_num = data;
    aht20_i2c_conf.scl_io_num = clock;
}

static void i2c_setup(){

    i2c_param_config(I2C_NUM_0, &aht20_i2c_conf);
    i2c_driver_install(I2C_NUM_0, I2C_MODE_MASTER, 0, 0, 0);
}
```


