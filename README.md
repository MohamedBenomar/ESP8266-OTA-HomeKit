# ESP8266-OTA-HomeKit

ESP8266-OTA-HomeKit

```
. $HOME/esp/esp-idf/export.sh

esptool.py -p /dev/tty.SLAB_USBtoUART --baud 115200 erase_flash

esptool.py -p /dev/tty.SLAB_USBtoUART --baud 115200 write_flash -fs 1MB -fm dout -ff 40m 0x0000 rboot.bin 0x1000 blank_config.bin 0x2000 otaboot.bin
```

### Compile Code

`docker run -it --rm -v "$(pwd)":/project -w /project esp-rtos make -C main FLASH_SIZE=8 HOMEKIT_SPI_FLASH_BASE_ADDR=0x8C000 all`

```
openssl sha384 -binary -out main/firmware/main.bin.sig main/firmware/main.bin

printf "%08x" `cat main/firmware/main.bin | wc -c`| xxd -r -p >>main/firmware/main.bin.sig
