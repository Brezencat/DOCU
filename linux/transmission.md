# Установка торрент-клиента Transmissition
_Установка в LXC контейнер_

После клонирования контейнера запускаем его и логинимся под root.

## Подготовка и установка

### Создаём пользователя, под которым будем работать
Более подробно можно почитать в заметке [Создание нового пользователя в Linux](./adduser.md)
```bash
adduser torrent
```

### Выдаём права на sudo новому пользователю
```bash
usermod -aG sudo torrent
```

### Переключаемся на созданного пользователя
```bash
su torrent
```

### Устанавливаем приложение Transmission
```bash
sudo apt install transmission-daemon -y
```
_если нет sudo, то нужно перелогиниться под root и поставить командой apt install sudo_

### Создаём каталоги, с которыми будет работать приложение 
```bash
mkdir /home/torrent/torrents
mkdir /home/torrent/downloads
mkdir /home/torrent/incomplete
```

### Выдаём права на каталоги для чтения и исполнения
```bash
sudo chmod 775 /home/torrent/torrents
sudo chmod 775 /home/torrent/downloads
sudo chmod 775 /home/torrent/incomplete
```

## Настройка Transmission

Перед настройкой необходимо оставновить сервис. Если этого не сделать, то при перезапуске и перезагрузке файл конфигурации вернётся в прежнее состояние.

### Останавливаем демона (сервис)
```bash
sudo service transmission-daemon stop
```

### Создадим бекап исходного файла настроек
```bash
sudo cp -pr /etc/transmission-daemon/settings.json /etc/transmission-daemon/settings.json.example
```

### Редактируем файл настроек Transmission
```bash
sudo nano /etc/transmission-daemon/settings.json
```

### Описание некоторых настоек
* "bind-address-ipv4": <прописываем IP-адрес контейнера, по которому будем подключаться к web-интерфейсу transmission>
* "download-dir": "/home/torrent/downloads", - директория, в которую будут загружаться торренты
* "incomplete-dir": "/home/torrent/incomplete", - директория для незавершенных загрузок
* "incomplete-dir-enabled": true, - сохранение незавершённых загрузок в отдельную директорию
* "rpc-authentication-required": true, - включаем запрос пароля в web-нитерфейсе
* "rpc-bind-address": <ip-адрес из поля "bind-address-ipv4">, - ip-адрес по которому будет доступен web-интерфейс
* "rpc-enabled": true, - включаем вход по логину и паролю в web-интерфейс
* "rpc-whitelist": "127.0.0.1,192.168.8.*", - указываем необходимые IP-адреса и подсети через запятую и без пробела
* "rpc-whitelist-enabled": true, - доступность web-интерфейса только с определенных ip и/или подсетей
* "rpc-password": "Password", - пароль для доступа через web-интерфейс (после перезагрузки конфига значение будет хешировано)
* "rpc-port": 9091, - порт, по которому доступен web-интерфейс
* "rpc-username": "torrent", - логин для доступа через web-интерфейс 

В конце файла конфигурации добавляем ещё два парамерта (не забываем поставить запятую в конце предшествующей строки):
* "watch-dir": "/home/torrent/torrents", - директория, где хранятся torrent-файлы
* "watch-dir-enabled": true - автоматическая постановка на закачку torrent-файлов

*!!!* Нужно добавить ссылку на ненадёжных пользователей (чёрный список пользователей)
http://john.bitsurge.net/public/biglist.p2p.gz


Переходим по указанному в настрейках IP-адресу и порту:\
http://192.168.8.170:9091


Есть инфо по доп настройке
https://help.ubuntu.ru/wiki/transmission-daemon
https://any-key.net/nastrojka-transmission-daemon-v-debian-9-stretch/