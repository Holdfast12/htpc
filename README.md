# Мультимедийный комп на archlinux на базовых репозиториях
## 1. Загрузка с usb-flash

pacman -Sw virtualbox-guest-utils --cachedir /mnt/ && repo-add /mnt/custom.db.tar.gz /mnt/*.pkg.tar.zst

список установленных пакетов
pacman -Qqe

обновить бд пакетов
pacman -Syy

scp -P2222 root@127.1:/test/* /mnt/c/Users/michael/htpc/packages/

scp -r -P2222 root@127.1:/home/vagrant/awx /mnt/c/Users/michael/htpc/
cp -r /vagrant/awx /home/vagrant/

xrandr -s 3840x1982_60

для работы скрипта поиска шрифтов
perl -MCPAN -e 'install Font::FreeType'



видео с дропающимися эмодзи
Советы которые спасут тебе Жизнь #shorts

/etc/polybar/config.ini

