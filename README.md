# Вентилятор BORK ESPHOME 
Модернизация вентилятора BORK CF TOR4135 BK для ESPHome
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://github.com/diemon24/BORK-Fun/blob/main/img/1_55253.jpg?raw=true">
  <source media="(prefers-color-scheme: light)" srcset="[https://github.com/diemon24/BORK-Fun/blob/main/img/SCH_BORK%20FAN_1-P1_2025-06-05.png?raw=true](https://github.com/diemon24/BORK-Fun/blob/main/img/1_55253.jpg?raw=true)">
  <img alt="Shows an illustrated sun in light mode and a moon with stars in dark mode." src="https://github.com/diemon24/BORK-Fun/blob/main/img/1_55253.jpg?raw=true)">
</picture>

Перед тем как модернизировать вентилятор я ставил перед собой задачу не только оставить текущий функционал, но и дополнить его - вентилятор должен уметь работать без интеграции с HomeAssistant. Но и сама интеграция с моим умным домом позволит расширить возможности вентилятора. 
Сразу оговорюсь, что я пытался использовать вентилятор через SmartIR, но в практике такое использование обернулось некорректной работой из-за работы функции осцилляции (вращения) - ИК сигналы просто не всегда улавливались из-за того, что вентилятор в момент отправки команды мог быть отвернут от ИК-передатчика. Ну и привязка данного вентилятора к комнате, в которой установлен ИК-передачик такое себе - вентилятор нужно иметь возможность носить в разные комнаты. 
IR коды для управления вентилятором через штатный пульт: https://github.com/smarthomehub/smartir/issues/1227?ysclid=mbj3myt8as96671823

Штатные функции вентилятора при использовании кнопок на панели управления: 
- Вкл/Выкл
- Выбор скорости (3 скорости)
- Режим эффекта природного ветра (волнообразный)
- Таймер выключения (никогда не использовал - считаю самой бесполезной функцией - разработчикам BORK привет)
- Вкл/Выкл осцилляции (вращения вентилятора по своей оси, для распределения воздушного потока в помещении)
- Звуковая индикация нажатий 
- Световая индикация, включая 2 кнопки с трехцветной индикацией (выбор скорости, таймер)
- Управление через ИК-пульт

Целевой функционал: 
- Вкл/Выкл (один клик), перезагрузка ESP - мультиклик 3c
- Выбор скорости (3 скорости)
- Режим эффекта природного ветра (волнообразный)
- Таймер выключения (никогда не использовал - считаю самой бесполезной функцией - разработчикам BORK привет)
- Вкл/Выкл осцилляции (вращения вентилятора по своей оси, для распределения воздушного потока в помещении)
- Звуковая индикация нажатий с разными эффектами
- Световая индикация, включая 2 кнопки с трехцветной индикацией (выбор скорости, таймер)
- Управление через ИК-пульт (опционально подключение IR-приемника на GPIO20 - данный GPIO необходимо переключить в режим input без возможности использования USB)
- Звуковая индикация корректной загрузки ESP при подаче питания
- Звуковая и световая индикация при подключении к сети Wi-Fi (в разработке при необходимости)
- Возможность отключения звуковой/световой индикации (режим "Не беспокоить, в разработке при необходимости) 


# Модернизация: 

Схема блока управления вентилятором:
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://github.com/diemon24/BORK-Fun/blob/main/img/SCH_BORK%20FAN_1-P1_2025-06-05.png?raw=true">
  <source media="(prefers-color-scheme: light)" srcset="https://github.com/diemon24/BORK-Fun/blob/main/img/SCH_BORK%20FAN_1-P1_2025-06-05.png?raw=true">
  <img alt="Shows an illustrated sun in light mode and a moon with stars in dark mode." src="https://github.com/diemon24/BORK-Fun/blob/main/img/SCH_BORK%20FAN_1-P1_2025-06-05.png?raw=true">
</picture>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://github.com/diemon24/BORK-Fun/blob/main/img/3D_PCB4_2025-06-05_top.png?raw=true">
  <source media="(prefers-color-scheme: light)" srcset="https://github.com/diemon24/BORK-Fun/blob/main/img/3D_PCB4_2025-06-05_top.png?raw=true">
  <img alt="Shows an illustrated sun in light mode and a moon with stars in dark mode." src="https://github.com/diemon24/BORK-Fun/blob/main/img/3D_PCB4_2025-06-05_top.png?raw=true">
</picture>

Gerber файл в https://github.com/diemon24/BORK-Fun/blob/main/Gerber_PCB4_2025-06-05_ver.1.1.zip


Вам нужно использовать плату разработки ESP32 S3 в узком формате. Тем не менее расположить на плате можно плату разработки в широком формате, но тогда необходимо использовать однорядные гнездовые разъемы для монтажа ESP32 S3 на плату с небольлшим наклоном. При использовании гнездовых разъемов для монтажа ESP32 S3 на плату, высота монтажа элементов увеличивается и потребуется небольшая доработка задней стенки корпуса - сделав отверстие под размер ESP. Но от этого есть плюс - при необходимости прошивки через JTAG, это можно будет выполнить без демонтажа корпуса вентилятора. 

В качестве датчика температуры выбран датчик ATH30 (https://esphome.io/components/sensor/aht10.html). Если есть необходимость использовать другой датчик (например TVOC и т.п.), то его также можно подключить в разъем CN6 i2c шины с небольшой доработкой прошивки. 

Часть деталей я использовал со штатной платы: зуммер, конденсатор C1 и варистор R1. 


Монтируем компоненты на плату:

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://github.com/diemon24/BORK-Fun/blob/main/img/IMG_20250601_235638%202.JPG?raw=true">
  <source media="(prefers-color-scheme: light)" srcset="https://github.com/diemon24/BORK-Fun/blob/main/img/IMG_20250601_235638%202.JPG?raw=true">
  <img alt="Shows an illustrated sun in light mode and a moon with stars in dark mode." src="https://github.com/diemon24/BORK-Fun/blob/main/img/IMG_20250601_235638%202.JPG?raw=true">
</picture>

На нижней стороны платы подготовлены места для мотажа RC фильтра (C2-R12, C3-R13, C4-R14, C5-R15), которые (как рекомендуют некоторые непроверенные источники в сети Интернет) необходимы для защиты симистора, и резисторов подтяжки (R16-R19). Но по факту RC и PULL-UP я не использую, т.к. электродвигатели вентилятора не имеют высокой мощности. Заявленная производителем мощность потребления вентилятора - не более 40Вт, когда как используются симисторы с возможностью подключения нагрузки до 1А на канал (±220 Вт). Тестировал не долго, но все работает прекрасно. 
Это моя первая разработка платы и схемы в EasyEDA для ESPHome, поэтому не судите строго. В испытаниях MOCов и симисторов, а также в разработке схемы и платы мне помогал Владимир @Greg_v_v, за что выражаю ему  благодарность. 

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://github.com/diemon24/BORK-Fun/blob/main/img/IMG_20250602_230544.JPG?raw=true!">
  <source media="(prefers-color-scheme: light)" srcset="https://github.com/diemon24/BORK-Fun/blob/main/img/IMG_20250602_230544.JPG?raw=true!">
  <img alt="Shows an illustrated sun in light mode and a moon with stars in dark mode." src="https://github.com/diemon24/BORK-Fun/blob/main/img/IMG_20250602_230544.JPG?raw=true!">
</picture>

Сравнение нового контроллера со штатной платой:

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://github.com/diemon24/BORK-Fun/blob/main/img/IMG_20250602_222543.JPG">
  <source media="(prefers-color-scheme: light)" srcset="https://github.com/diemon24/BORK-Fun/blob/main/img/IMG_20250602_222543.JPG">
  <img alt="Shows an illustrated sun in light mode and a moon with stars in dark mode." src="https://github.com/diemon24/BORK-Fun/blob/main/img/IMG_20250602_222543.JPG">
</picture>

Я не стал проектировать новые платы для кнопок и светодиодов - на светодиодной плате я использовал штатные. Не смотря на то, что для управления светодиодами используется ШИМ, я все равно заменил перемычку между светодиодами TYPE и SPEED (выпаял нужный по цветовой схеме с демонтированной штатной платы) и соединил каплей припоя черный провод (GND) с дорожкой, идущей сразу под местом подпайки - дав светодиоду SWING GND подключение. Собственно больше никаких доработок не производилось. 




