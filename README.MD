# Мультимедийный комп на archlinux
## 1. Загрузка с usb-flash
настройка до момомента первой загрузки
https://help.reg.ru/support/servery-vps/oblachnyye-servery/ustanovka-programmnogo-obespecheniya/arch-linux-chto-takoye-i-kak-ustanovit


### настройка dns
rm /etc/resolv.conf
ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf

установка пакетов для дальнейшей работы
ssh
