# Создание и добавление ключа RSA
Ключ нужн для повышения безопасности и подключения к удалённому серверу без ввода пароля (условно).

## Создание ключа
- в процессе

## Добавление rsa ключа на сервер

Подключаемся к удалённому серверу по ssh
```bash
 ssh <login>@<host-name>
```

Проверяем, есть ли у нас директория (.ssh) и файл (authorized_keys) для храненения ключей
```bash
ls -lha ~
```

Если отсутсвует, как у меня
```bash
drwx------   4 <USER> <USER>  91 окт 28 09:13 .
drwxr-xr-x. 11 root        root        155 окт 27 17:08 ..
-rw-r--r--   1 <USER> <USER>  18 окт 24  2020 .bash_logout
-rw-r--r--   1 <USER> <USER> 141 окт 24  2020 .bash_profile
-rw-r--r--   1 <USER> <USER> 376 окт 24  2020 .bashrc
drwxr-xr-x   2 <USER> <USER>   6 мар 31  2021 .cache
drwx------   3 <USER> <USER>  20 окт 28 09:13 .config
```

То создаём директорию
```bash
mkdir ./.ssh/
```

и файл, в который сразу же записываем свой публичный ключ (из файла id_rsa.pub, который создали ранее)
```bash
echo 'ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDpwlehSb6XG7N8V2QLVii9uiIxNF ... adPVbfpxs3290KgMNID6V2uo+MzYH2um/ioROmL5 <USER>@<HOST>' > ./.ssh/authorized_keys
```

Проверяем, что у нас всё есть и какие права на директории 
```bash
$ ls -lha
итого 12K
drwx------   5 <USER> <USER> 103 окт 28 09:15 .
drwxr-xr-x. 11 root        root        155 окт 27 17:08 ..
drwxrwxr-x   2 <USER> <USER>  29 окт 28 09:19 .ssh
```
и файле
```bash
$ ls -lha ./.ssh/
итого 4,0K
drwxrwxr-x 2 <USER> <USER>  29 окт 28 09:19 .
drwx------ 5 <USER> <USER> 103 окт 28 09:15 ..
-rw-rw-r-- 1 <USER> <USER> 414 окт 28 09:19 authorized_keys
```

Если создали папку не под своим пользователем, то меняем владельца и группу
```bash
chown -R $USER:$USER ~/.ssh
```

Далее меняем права на директорию .ssh
```bash
chmod 700 ~/.ssh
```
на всё содержимое внутри директории
```bash
chmod 644 ~/.ssh/*
```
и на сам файл с ключом
```bash
chmod 600 ~/.ssh/authorized_keys
```

Провряем, что изменилось
```bash
$ ls -lha
итого 12K
drwx------   5 <USER> <USER> 103 окт 28 09:15 .
drwxr-xr-x. 11 root        root        155 окт 27 17:08 ..
drwx------   2 <USER> <USER>  29 окт 28 09:19 .ssh

$ ls -lha ./.ssh/
итого 4,0K
drwx------ 2 <USER> <USER>  29 окт 28 09:19 .
drwx------ 5 <USER> <USER> 103 окт 28 09:15 ..
-rw------- 1 <USER> <USER> 414 окт 28 09:19 authorized_keys
```

Перелогиниваемся на сервер и подключение будет уже по ключу.


# Если кратко:
### Права:
* Директория - 700 (drwx------).
* Закрытый ключ (id_rsa или id_dsa) - 600 (-rw------).
* Все остальные файлы в директории - 644 (-rw------).
* Все файлы должны принадлежать текущему пользователю и его группе.

### Команды:
```bash
chown -R $USER:$USER ~/.ssh
chmod 700 ~/.ssh
chmod 644 ~/.ssh/*
chmod 600 ~/.ssh/authorized_keys
```
Опционально:
```bash
chmod 600 ~/.ssh/id_rsa ~/.ssh/id_dsa 
```
