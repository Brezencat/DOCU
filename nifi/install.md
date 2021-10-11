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

