# Установка OMV в Pnet
Делаю тоже самое, что и во время второго модуля, для установки debian.
Начало установки:
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/Image/%D0%91%D0%B5%D0%B7%20%D0%BD%D0%B0%D0%B7%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F-24.10.2025-20_40.png?raw=true)

---

Результат установки
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/Image/%D0%91%D0%B5%D0%B7%20%D0%BD%D0%B0%D0%B7%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F-24.10.2025-20_53.png?raw=true)

---
Графическая оболочка
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/Image/%D0%91%D0%B5%D0%B7%20%D0%BD%D0%B0%D0%B7%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F-24.10.2025-21_12.png?raw=true)

--- 
## Установка oxidized
Я решил ставить эту программу через Docker.
Что было сделано:
- Установлен docker
- Установлен AppArmor
- Создана директория для Oxidized
- Создан файл `docker-compose.yml`, а также конфигурационный файл oxidized `/srv/oxidized/config/config`
- Был создан список устройств, но на данный момент там 1 устройство, которого нет в сети
- Запуск oxidized

Файл `docker-compose.yml`
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/Image/%D0%91%D0%B5%D0%B7%20%D0%BD%D0%B0%D0%B7%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F-24.10.2025-21_37.png?raw=true)

---
Файл oxidized `/srv/oxidized/config/config`
![[Без названия-24.10.2025-22_03.png]]

---
Файл `router.db` без которого все ломается
![[Без названия-24.10.2025-22_05.png]]

---
Результат работы
![[Без названия-24.10.2025-22_15.png]]