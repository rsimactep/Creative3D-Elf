# Marlin 3D Printer Firmware for Creativity 3D Elf

Это конфигурация [официального Marlin](https://github.com/MarlinFirmware/Marlin) для принтера Creativity 3D Elf (плата MKS Robin Nano 1.x).

Прошивка адптированна под использование хотэнда Crazy NF (Mosquito), для чего добавлена дополнительная температурная таблица.
И BMG dual gear экструдера (влияет на количество шагов двигателя экструдера, в конфиге есть пометка)

В данной прошифке работает графический экран, BL Touch (подключенный вместо детектора окончания филамента MDET2) и WiFI.

## MKS WIFI модуль

### Работает

* Отображение температуры в Cura
* Просмотр содержимого SD карты
* Удаление файлов с SD карты
* Загрузка файлов на SD карту
* Автоматический запуск печати при загрузке файла.

### Не работает

* **Имена файлов на русском** Переименуйте файл в Cura
* Формат имени файла 8.3 (другими словами 8 символ на имя)
* Отображение состояния принтера (печатает, не печатает) в Cura

## Особенности

В данной конфигцрации настроены все доайвера как TMC 2208, для использования стоковой конфигурации необходимо немного подправить конфиг.
Разница, только в направлении движения осей.

Для установки прошивки файл Robin_nano35.bin нужно записать в корень SD карты и включить принтер.

Вернуть стандартную прошивку можно в любой момент. Просто запишите ее на SD и включите принтер.

Для настройки под свои нужды, прошивку нужно собрать самостоятельно.

### Первое, что нужно сделать, после прошивки

Первое, что нужно сделать после прошивки, это проинициализировать EEPROM (память внутри принтера), сбросив настройки по-умолчанию. После прошивки там находится мусор, который может привести к совершенно необъяснимому поведению.

Делается это через меню Configuration -> Advanced settings -> Initialize eeprom.

### Как собрать прошивку самому

[Видео](https://www.youtube.com/watch?v=HirIZk0rWOQ) Дмитрия Соркина

Нужная плата, Robin Nano, уже выбрана в качестве платы по-умолчанию. В меню Platformio можно не выбирать плату, а использовать сочетание клавиш Ctrl+Alt+B.

После компиляции, готовая прошивка лежит в .pio/build/mks_robin_nano35/Robin_nano35.bin

На SD карту нужно записывать именно Robin_nano35.bin, и к нему папку assets (в ней находятся картинки. Но обратите внимание, картинки с направлениями движения по Z перепутаны и нужно переименовать фалы, тем самым поменять картинки местами)

### Что нужно настроить, если собираете сами

Нужно настроить направления движения по осям под свои драйвера в файле [Configuration.h](./Marlin/Configuration.h) (параметры INVERT_?_DIR).

По умолчанию стоят настройки под драйвера 2208/2209 на всех осях. В файле [Configuration.h](./Marlin/Configuration.h).

### Настройки WIFI, если вы используете готовую прошивку

Настройки сети хранятся в самом ESP-модуле. Есть несколько вариантов настройки:

* Если модуль уже был настроен, то возможно никакая настройка не понадобится
* Если модуль не был настроен, либо по какой-то причине не смог подключиться к сети, то он запустится в режиме точки доступа с именем сети MKSWIFI??? (вместо ? будут произвольные символы). Подключитесь к этой сети, откройте страницу по адресу 192.168.4.1 и установите нужные настройки сети.

### Состояние WIFI

При успешном подключении к сети (или создании сети в режиме точки доступа) в стандартный UART, который выведен на USB разъем принтера, будет выведен IP адрес и название сети, а так же IP адрес будет отображен на экране принтера.

### Как понять, что WIFI работает

При включении принтера, на экране отобразится статус "WIFI init"

Если ESP модулю удалось подключиться к сети, на экране будет IP адрес.

При старте передачи файла отображается "Upload file", в процессе загрузки отображается прогресс в процентах.

Если файл успешно принят отобразится "Upload done".

Если во время приема файла были ошибки, отобразится надпись "Upload Failed".

### Драйвера TMC2209

По-умолчанию прошивка настроена на работу с драйверами шаговых двигателей без программного управления. В случае применения драйвером TMC 2209 или TMC 2208 можно включить управление по UART. Подробнее о [настройке и подключении](https://sergey1560.github.io/fb4s_howto/tmc_uart/).

# Mks-Robin-Nano-Marlin2.0-Firmware
## Features
The firmware of Mks Robin Nano, based on [Marlin2.0.x](https://github.com/MarlinFirmware/Marlin), added the [LittlevGL](https://github.com/littlevgl/lvgl), supporting colourful GUI and touch screen. It is developed on PlatformIO, we hope more and more developers will participate the development of this repository.

![](https://github.com/makerbase-mks/Mks-Robin-Nano-Marlin2.0-Firmware/blob/master/Images/MKS_Robin_Nano_printing.png)

## Build
As the firmware is based on Marlin2.0.x which is built on the core of PlatformIO, the buid compiling steps are the same as Marlin2.0.x. You can directly using [PlatformIO Shell Commands](https://docs.platformio.org/en/latest/core/installation.html#piocore-install-shell-commands), or using IDEs contain built-in PlatformIO Core(CLI), for example, [VSCode](https://docs.platformio.org/en/latest/integration/ide/vscode.html#ide-vscode) and [Atom](https://docs.platformio.org/en/latest/integration/ide/atom.html). VSCode is recommended.

## About the gcode file preview
The images should be added to gcode file when slicing, and MKS has developed the [plugin for Cura](https://github.com/makerbase-mks/mks-wifi-plugin) to make it.

## About the image conversion
- Open [LVGL online image converter tool](https://lvgl.io/tools/imageconverter). 
- Open bmp images.
- Enter the saved file name.
- Choose color format:True color.
- Choose file output format:Binary RGB565.
- Start convertion.
- Save bin file.
- Copy the converted bin file to the assets folder.
- Copy the assets folder to the SD card.
- SD card is connected to the motherboard, and you can see the update interface after powering on.

## Firmware Can be run on Robin Nano V1.x and V2.x boards
## MKS Robin Nano V1.x build and update firmware

1. Build config:
     
- `default_envs = mks_robin_nano35`     
- `#define MOTHERBOARD BOARD_MKS_ROBIN_NANO`    
- `#define TFT_LVGL_UI_FSMC`

2. Update firmware:
   
- Enter the `.pio\build\mks_robin_nano35` directory, copy the `assets` folder and `Robin_nano35.bin` to the sd card
- SD card is connected to the motherboard, and you can see the update interface after powering on.   

## MKS Robin Nano V2.x build and update firmware

1. Build config:
     
- `default_envs = mks_robin_nano35`     
- `#define MOTHERBOARD BOARD_MKS_ROBIN_NANO_V2`    
- `#define TFT_LVGL_UI_SPI`

2. Update firmware:
   
- Enter the `.pio\build\mks_robin_nano35` directory, copy the `assets` folder and `Robin_nano35.bin` to the sd card
- SD card is connected to the motherboard, and you can see the update interface after powering on.   

## Others functional configuration
Please refer to [MKS-Robin-Nano-V2 wiki](https://github.com/makerbase-mks/MKS-Robin-Nano-V2/wiki/Marlin_firmware).

## More information about the Robin Nano
Please refer to [MKS Robin Nano github](https://github.com/makerbase-mks/MKS-Robin-Nano).
