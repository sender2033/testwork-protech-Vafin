# Установка OMV в Pnet
Делаю тоже самое, что и во время второго модуля, для установки debian.
Начало установки:
![Image|700x788](https://github.com/sender2033/testwork-protech-Vafin/blob/main/Image/%D0%91%D0%B5%D0%B7%20%D0%BD%D0%B0%D0%B7%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F-24.10.2025-20_40.png?raw=true)

---

Результат установки
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/Image/%D0%91%D0%B5%D0%B7%20%D0%BD%D0%B0%D0%B7%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F-24.10.2025-20_53.png?raw=true)

---
Графическая оболочка
![Image|700x394](https://github.com/sender2033/testwork-protech-Vafin/blob/main/Image/%D0%91%D0%B5%D0%B7%20%D0%BD%D0%B0%D0%B7%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F-24.10.2025-21_12.png?raw=true)

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
![Image|699x445](https://github.com/sender2033/testwork-protech-Vafin/blob/main/Image/%D0%91%D0%B5%D0%B7%20%D0%BD%D0%B0%D0%B7%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F-24.10.2025-22_03.png?raw=true)

---
Файл `router.db` без которого все ломается
![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/Image/02_%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0%20OMV,%20%D0%B0%20%D1%80%D0%B0%D0%B7%D0%B2%D1%91%D1%80%D1%82%D1%8B%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5%20%D0%BD%D0%B0%20%D0%BD%D0%B5%D0%B9%20Oxidized-31.10.2025-15_17.png?raw=true)



---
Результат работы
![Image|700x595](https://github.com/sender2033/testwork-protech-Vafin/blob/main/Image/02_%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0%20OMV,%20%D0%B0%20%D1%80%D0%B0%D0%B7%D0%B2%D1%91%D1%80%D1%82%D1%8B%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5%20%D0%BD%D0%B0%20%D0%BD%D0%B5%D0%B9%20Oxidized-29.10.2025-22_14.png?raw=true)


 ![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/Image/02_%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0%20OMV,%20%D0%B0%20%D1%80%D0%B0%D0%B7%D0%B2%D1%91%D1%80%D1%82%D1%8B%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5%20%D0%BD%D0%B0%20%D0%BD%D0%B5%D0%B9%20Oxidized-31.10.2025-15_21.png?raw=true)
 
 ![Image](https://github.com/sender2033/testwork-protech-Vafin/blob/main/Image/02_%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0%20OMV,%20%D0%B0%20%D1%80%D0%B0%D0%B7%D0%B2%D1%91%D1%80%D1%82%D1%8B%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5%20%D0%BD%D0%B0%20%D0%BD%D0%B5%D0%B9%20Oxidized-31.10.2025-15_21-1.png?raw=true)
 