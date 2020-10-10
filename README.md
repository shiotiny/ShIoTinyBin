# ShIoTinyBin

Бинарные прошивки для ESP-07

Схема, прошивка и документация.

Прошивка: bin/esp-07-shiotiny.bin

Схема:	doc/esp-07-shiotiny.png

Описание и инструкция: doc/ShIoT-esp8266-01_obzor.pdf

-----------------------------------------------------------------------------------------------------------------
Шить, если у вас esptool -  так:
 
1. Перед прошивкой замкнуть DIP-переключатель PROG (GPIO0).

2. Нажать RESET

3.Стереть память (вместо /dev/ttyUSB2 подставить свой COM-порт)

		# ./esptool.py --port /dev/ttyUSB2 -p /dev/ttyUSB2 -b 115200 erase_flash

4. Загрузить прошивку (вместо /dev/ttyUSB2 подставить свой COM-порт)

		# ./esptool.py -p /dev/ttyUSB2 -b 115200 write_flash -ff 40m -fm qio -fs 8m 0x000000 esp-07-shiotiny.bin

5. Рамкнуть DIP-переключатель PROG (GPIO0).

6. Нажать RESET

После этого устройство будет в режиме конфигурации (открытая точка доступа).

-----------------------------------------------------------------------------------------------------------------

Для переключения в режим конфигурации (открытая точка доступа) из любого рабочего режима:

 -- Нажать кнопку AP (GPIO15) и удерживать её в течении 5сек (пока не загориться светодиод GPIO0) --

-----------------------------------------------------------------------------------------------------------------

Если у вас ESP8266 с несколькими мегабайтами FLASH, то для работы надо прошить образ два раза: в первый и последний мегабайт FLASH.

    Размер FLASH 1M: прошивка образа с адреса 0x00000000
	# ./esptool.py -p /dev/ttyUSB2 -b 115200 write_flash -ff 40m -fm qio -fs 8m 0x000000 esp-07-shiotiny.bin

    Размер FLASH 2M: прошивка образа с адреса 0x00000000 (1копия) и с адреса 0x00100000 (2копия)
	# ./esptool.py -p /dev/ttyUSB2 -b 115200 write_flash -ff 40m -fm qio -fs 8m 0x000000 esp-07-shiotiny.bin
	# ./esptool.py -p /dev/ttyUSB2 -b 115200 write_flash -ff 40m -fm qio -fs 8m 0x100000 esp-07-shiotiny.bin

    Размер FLASH 4M: прошивка образа с адреса 0x00000000 (1копия) и с адреса 0x00300000 (2копия)
	# ./esptool.py -p /dev/ttyUSB2 -b 115200 write_flash -ff 40m -fm qio -fs 8m 0x000000 esp-07-shiotiny.bin
	# ./esptool.py -p /dev/ttyUSB2 -b 115200 write_flash -ff 40m -fm qio -fs 8m 0x300000 esp-07-shiotiny.bin

    Размер FLASH 8M: прошивка образа с адреса 0x00000000 (1копия) и с адреса 0x00700000 (2копия)
	# ./esptool.py -p /dev/ttyUSB2 -b 115200 write_flash -ff 40m -fm qio -fs 8m 0x000000 esp-07-shiotiny.bin
	# ./esptool.py -p /dev/ttyUSB2 -b 115200 write_flash -ff 40m -fm qio -fs 8m 0x700000 esp-07-shiotiny.bin

    Размер FLASH 16M: прошивка образа с адреса 0x00000000 (1копия) и с адреса 0x00F00000 (2копия)
	# ./esptool.py -p /dev/ttyUSB2 -b 115200 write_flash -ff 40m -fm qio -fs 8m 0x000000 esp-07-shiotiny.bin
	# ./esptool.py -p /dev/ttyUSB2 -b 115200 write_flash -ff 40m -fm qio -fs 8m 0xF00000 esp-07-shiotiny.bin

-----------------------------------------------------------------------------------------------------------------
