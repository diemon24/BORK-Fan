# Вентилятор BORK ESPHOME 
Модернизация вентилятора BORK CF TOR4135 BK для ESPHome
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://github.com/diemon24/BORK-Fun/blob/main/img/1_55253.jpg?raw=true">
  <source media="(prefers-color-scheme: light)" srcset="[https://github.com/diemon24/BORK-Fun/blob/main/img/SCH_BORK%20FAN_1-P1_2025-06-05.png?raw=true](https://github.com/diemon24/BORK-Fun/blob/main/img/1_55253.jpg?raw=true)">
  <img alt="Shows an illustrated sun in light mode and a moon with stars in dark mode." src="https://github.com/diemon24/BORK-Fun/blob/main/img/1_55253.jpg?raw=true)">
</picture>

Перед тем как модернизировать вентилятор я ставил перед собой задачу не только оставить текущий функционал, но и дополнить его - вентилятор должен уметь работать без интеграции с HomeAssistant. Но и сама интеграция с моим умным домом позволит расширить возможности вентилятора. 
Сразу оговорюсь, что я пытался использовать вентилятор через SmartIR, но в практике такое использование обернулось некорректной работой из-за работы функции осцилляции (вращения) - ИК сигналы просто не всегда улавливались из-за того, что вентилятор в момент отправки команды мог быть отвернут от ИК-передатчика. Ну и привязка данного вентилятора к комнате, в которой установлен ИК-передачик такое себе - вентилятор нужно иметь возможность носить в разные комнаты. 

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
- Управление 
- Звуковая и световая индикация при подключении к сети Wi-Fi (в разработке)
- Возможность отключения звуковой/световой индикации (режим "Не беспокоить, в разработке) 

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
Монтируем компоненты на плату:

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://github.com/diemon24/BORK-Fun/blob/main/img/IMG_20250601_235638%202.JPG?raw=true">
  <source media="(prefers-color-scheme: light)" srcset="https://github.com/diemon24/BORK-Fun/blob/main/img/IMG_20250601_235638%202.JPG?raw=true">
  <img alt="Shows an illustrated sun in light mode and a moon with stars in dark mode." src="https://github.com/diemon24/BORK-Fun/blob/main/img/IMG_20250601_235638%202.JPG?raw=true">
</picture>



Вам нужно использовать плату разработки ESP32 S3 в узком формате. Тем не менее расположить на плате можно плату разработки в широком формате, но тогда необходимо использовать однорядные гнездовые разъемы для монтажа ESP32 S3 на плату с небольлшим наклоном. При использовании гнездовых разъемов для монтажа ESP32 S3 на плату, высота монтажа элементов увеличивается и потребуется небольшая доработка корпуса - сделав отверстие, т.к. разъемы 
