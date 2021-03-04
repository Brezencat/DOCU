#Grafana. Установка и настройка на Raspberry Pi

Устанавливаем утилиту и библиотеку шрифтов (скорее всего уже установлены)
```
sudo apt install -y adduser libfontconfig1
```
Перед скачиваем дистрибутива проверяем архитектуру и версию процессора
```
cat /proc/cpuinfo
```
Переходим в папку Загрузки
```
cd Downloads/
```
и скачиваем пакет Greafana с [офф.сайта](https://grafana.com/grafana/download?platform=arm)
```
wget https://dl.grafana.com/oss/release/grafana_7.4.3_armhf.deb
```
Устанавливаем пакет
```
sudo dpkg -i grafana_7.4.3_armhf.deb
```
Удаляем загруженный пакет
```
rm grafana_7.4.3_armhf.deb
```
\
Самое время поставить СУБД, если не установлена ни одна из SQLite3, MySQL (MariaDB), PostgreSQL.
Я использую MariaDB.
_Ссылка на установку и настройку в инструкции по установке Nextcloud._ 
\
Подключаемся к БД (обязательно под root и от sudo)
```
sudo mariadb -u root -p
```
Вводим пароль от root для БД (задавали при настройке).
Должны увидеть приглашение командной строки: **MariaDB [(none)]>**.

Создаём БД для Grafana
```
CREATE DATABASE grafana;
```
Создаём пользователя для Grafana ('password' заменить на свой пароль)
```
CREATE USER grafana@localhost IDENTIFIED BY 'password';
```
Выдаём привилегии пользователю grafana
```
GRANT ALL PRIVILEGES ON grafana.* TO grafana@localhost;
```
Перезагрузка привилегий
```
FLUSH PRIVILEGES;
```
Выход из БД
```
exit
```
или
```
\q
```
\
Переходим в настройки Grafana
```
sudo nano /etc/grafana/grafana.ini
```
Прописываем нашу БД
```
# Either "mysql", "postgres" or "sqlite3", it's your choice
;type = mysql
;host = 127.0.0.1:3306
;name = grafana
;user = grafana
# If the password contains # or ; you have to wrap it with triple quotes. Ex ""$
;password = password
```
Заменить пароль у админа и указать IP вместо localhost. 
\
Перезапускаем сервис
```
sudo systemctl restart grafana-server
```
\
Переходим в интерфейс http://192.168.1.90:3000
IP адрес малинки, который указывали в настройках, порт 3000 по умолчанию порт Grafana.
\
\
Добавляем порт в исключения брандмауэра (если он настроен)
```
ufw allow 3000/tcp
```
\
\
Обновление плагинов
```
grafana-cli plugins update-all
```
\
\
Бекап БД (Про создание бекапов в MySQL/MariaDB можно поситать [здесь](https://www.dmosk.ru/miniinstruktions.php?mini=mysql-dump))
```
mysqldump -u grafana -p grafana > /home/pi/backup/grafana_mysql.sql
```