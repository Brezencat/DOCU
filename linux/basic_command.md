# Базовые команды Linux

#### MAN
Описание (мануал) команды
```bash
man <command-name>
```

#### EXIT
Завершить текущую сессию в терминале
```bash
exit
```

#### CLEAR
Очистить окно терминала
```bash
clear
```

#### HISTIRY
история вводимых команд в терминале
```bash
history
```



#### LESS
```bash
less <file-name>
```

#### GREP
```bash
grep "<string>" <file-name>
```
```bash
grep -i "<string>" <file-name>
```
```bash
grep -r "<string>" <file-name>
```



## Создание файлов и папок

#### TOUCH
Создать файл
```bash
touch  <file-name>
```



## Работа с архивами

#### TAR
Создание архива.
```bash
tar -cvf <archive-name.tar> <file-name-to-archive>
```
Посмотреть содержимое архива.
```bash
tar -tvf <archive-to-view.tar>
```
Распаковать архив.
```bash
tar -xvf <archive-to-extract.tar>
```

#### UNZIP
```bash
unzip <archive-to-extract.zip>
```
```bash
unzip -l <archive-to-extract.zip>
```



## Системные (Работа с процессами)

#### PS
Выводит информацию о текущих запущенных процессах. Чаще используется с доп. флагами
```bash
ps
```



## Работа с сетью

#### PING
```bash
ping <host-address or IP>
```



#### 
```bash

```