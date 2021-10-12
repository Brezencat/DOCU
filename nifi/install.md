# Установка Apache NiFi на Debian 11

_все команды в терминале запускаются из под рута (root), если не указано иное._

## Java
Перед установкой самого NiFi сначала стоит проверить версию Java, если она установлена.
```bash
java -version
```
Если версия ниже 8, то необходимо установить Java 8 или 11 (на данный момент именно они рекомендованы).\
Есть несколько разновидностей открытого пакета openjdk: 
* **JDK** (Java Development Kit) - для разработки на Java, 
* **JRE** (Java Runtime Environment) - для запуска приложений.

 _Я буду ставить Java 11 версию JRE._
```bash
apt install -y openjdk-11-jre
```


## Установка Apache NiFi

Скачиваем архив для установки NiFi с [офф.сайта](https://nifi.apache.org/download.html)
```bash
wget https://dlcdn.apache.org/nifi/1.14.0/nifi-1.14.0-bin.tar.gz 
```

Распаковываем скаченный архив
```bash
tar -xvzf nifi-1.13.2-bin.tar.gz
```

Переносим папку в рабочую дирректорию
```bash
mv nifi-1.14.0 /opt/nifi
```

Почистим директорию, куда скачивали архив
```bash
rm nifi-1.14.0-bin.tar.gz
```

Рекомендуют перед дальнейшей настройкой поизвести первый запуск NiFi
```bash
/opt/nifi/bin/nifi.sh start 
```
Скорее всего получим ошибку об отсутсвии переменной окружения JAVA_HOME:\
_nifi.sh: JAVA_HOME not set; results may vary_

предварительно узнаем путь, где у нас установлена Java JDK
```bash
update-alternatives --config java
```
Увидим что-то подобное:\
_There is only one alternative in link group java (providing /usr/bin/java): /usr/lib/jvm/java-11-openjdk-amd64/bin/java_

Редактируем настройки окружения NiFi
```bash
nano /opt/nifi/bin/nifi-env.sh
```
Расскоментируем строку:\
_#export JAVA_HOME=/usr/java/jdk1.8.0/_\
и заменим путь на наш:\
_export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64_\
Применим изменения
```bash
source /opt/nifi/bin/nifi-env.sh
```
Проверим переменную среды
```bash
echo $JAVA_HOME
```

Устанавливаем NiFi сервисом
```bash
/opt/nifi/bin/nifi.sh install
```
Перезагружаем демон systemd
```bash
systemctl daemon-reload
```
Запускаем сервис Apache NiFi
```bash
/etc/init.d/nifi start
```
Выводом будет:
```bash
Java home: /usr/lib/jvm/java-11-openjdk-amd64/
NiFi home: /opt/nifi

Bootstrap Config File: /opt/nifi/conf/bootstrap.conf
```

Переходим к настройке NiFi
```bash
nano /opt/nifi/conf/nifi.properties 
```
Прописываем значения:
```bash
nifi.web.http.host=127.0.0.1 (или IP адрес NiFi)
nifi.web.http.port=8080
nifi.web.http.network.interface.default=eth0 (адаптер, на котором есть сеть и чей IP прописывали выше)
```
Очищаем значения
```bash
nifi.web.https.host=
nifi.web.https.port=
```
Сохраняем.

Переходим в браузер по ссылке:\
http://localhost:8080/nifi\
_вместо localhost указываем IP адрес NiFi_
