#Команды PosgreSQL
\
Смена пароля для пользователя БД postgres
```
psql -c "ALTER USER postgres WITH PASSWORD ‘PaSsWoRd;"
```
\
Переключиться на пользователя postgres в Linux
```
sudo su - postgres
```
\
Подключиться к БД в терминале
```
psql
```
\
Список БД
```
\l
```
или расширенная информация
```
\l+
```
\
Список пользователей БД
```
\du
```
\
Создаём нового пользователя БД
```
create user <USER_NAME> with login password 'PaSsWoRd';
```
\
Даём пользователю права админа
```
alter role <USER_NAME> with superuser;
```
\
Создаём учётную запись etl с ограничением по коннектам
```
create role etl with connection limit 50;
```
\
Показывает максимальное число конектов к серверу (БД)
```
show max_connections;
```
\
В какой директории хранятся данные (файлы БД)
```
show data_directory
```
\
Посмотреть схемы базы даных
```
\dn
```
\
Выход из psql (отключение от БД)
```
\q 
```
\
Директория с данным PGSQL
```
/var/lib/postgresql/11/main
```
\
Посмотреть файл postmaster.pid
\
Файлы журнала транзакций в дирректории
```
pg_wal
```
\
Конфиги и файл hba хранятся в дирректории
```
/etc/postgresql/11/main/
```
\
В postgresql.conf раскомментировать и изменить строку listen_addresses = '*' - подключаться из любого места. 
Конфигурационные файлы можно сформировать на https://pgtune.leopard.in.ua/
\
В pg_hba.conf добавить строку для подключения по конкретному логину из любого места по паролю
```
host	all		<user_name>	0.0.0.0/0		md5
```
\
Системный каталог отображает все подключения
```
pg_stat_activity
```
\
Функции возвращают инфо о сессии
```
pg_backend_pid()  - id текущей сессии 
```
