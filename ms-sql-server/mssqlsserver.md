# MS SQL Server for Linux

## Установка

### [Установка SQL Server](https://docs.microsoft.com/ru-ru/sql/linux/quickstart-install-connect-ubuntu?view=sql-server-ver15)

Для установки нужно добавить \(зарегистрировать\) репозиторий Microsoft SQL Server Ubuntu: импортировать GPG ключ

```text
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
```

или

```text
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
```

добавить репозиторий

```text
sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/18.04/mssql-server-2019.list)"
```

или

```text
curl https://packages.microsoft.com/config/ubuntu/18.04/mssql-server-2019.list | sudo tee /etc/apt/sources.list.d/mssql-server-2019.list
```

 Установка MS SQL Server \(ключ -y обозначает соглашение со всеми возникающими вопросам\)

```text
sudo apt-get install -y mssql-server
```

После установки переходим к настройке.

### Установка программ командной строки SQL Server

[sqlcmd](https://docs.microsoft.com/ru-ru/sql/tools/sqlcmd-utility?view=sql-server-ver15) и [bcp](https://docs.microsoft.com/ru-ru/sql/tools/bcp-utility?view=sql-server-ver15)\

> С этой частью может быть проблема, если добавить репозиторий не соответствующий версии ОС, то unixodbc-dev не ставится.

Добавит репозиторий

```text
sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/20.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list)"
```

или

```text
curl https://packages.microsoft.com/config/ubuntu/20.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
```

 Установка mssql-tools

```text
sudo apt-get install mssql-tools
```

принимаем условия лицензии msodbcsql17 и mssql-tools. 

Установка unixodbc-dev \([драйвер ODBC](https://docs.microsoft.com/ru-ru/sql/connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server?view=sql-server-ver15)\)

```text
sudo apt-get install unixodbc-dev
```

### [Установка служб SQL Server Integration Services \(SSIS\)](https://docs.microsoft.com/ru-ru/sql/linux/sql-server-linux-setup-ssis?view=sql-server-ver15)

Установка

```text
sudo apt-get install -y mssql-server-is
```

После установки переходим к настройке.

## Настройка

### Настройка MS SQL Server

После окончания установки запускаем настройки MS SQL Server

```text
sudo /opt/mssql/bin/mssql-conf setup
```

Выбираем выпуск SQL Server числовым обозначением: 

_2 - Developer; 3 - Express_ 

Подверждаем лицензионное соглашение: _y_ 

Выбираем язык для SQL Server: _1 - English; 9 - Русский_ 

Создаём и подтверждаем пароль системного администратора SQL Server _\(минимальная длина 8 символов, строчные и прописные буквы, десятичные цифры и \(или\) символы\)._  

Проверяем, что служба mssql-server работает

```text
systemctl status mssql-server --no-pager
```

В терминале должна быть строка: _Active: active \(running\)_

### Настройки для sqlcmd и bcp

Добавить путь _/opt/mssql-tools/bin/_ в переменную среды PATH в оболочке bash. Для сеансов входа в систему

```text
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
```

Для интерактивных сеансов и сеансов без входа в систему

```text
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc

source ~/.bashrc
```

### Локальное подключение с помощью sqlcmd

```text
sqlcmd -S localhost -U SA -P '<YourPassword>'
```

### [Включение агента SQL Server](https://docs.microsoft.com/ru-ru/sql/linux/sql-server-linux-setup-sql-agent?view=sql-server-ver15#EnableAgentAfterCU4)

Для версии от SQL Server 2017 CU4

```text
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
sudo systemctl restart mssql-server
```

[Создание и запуск заданий агента SQL Server в Linux](https://docs.microsoft.com/ru-ru/sql/linux/sql-server-linux-run-sql-server-agent-job?view=sql-server-ver15)

[Агент SQL Server](https://docs.microsoft.com/ru-ru/sql/ssms/agent/sql-server-agent?view=sql-server-ver15) \(эту часть в дальнейшем перенести в раздел по SQL и заменить ссылку\)

### [Настройка SQL Server Integration Services в Linux с помощью ssis-conf](https://docs.microsoft.com/ru-ru/sql/linux/sql-server-linux-configure-ssis?view=sql-server-ver15)

Для настройки необходимо выполнить команду

```text
sudo /opt/ssis/bin/ssis-conf setup
```

Выбираем выпуск SQL Server числовым обозначением: _2 - Developer; 3 - Express_ Подверждаем лицензионное соглашение: _y_ Выбираем язык для SQL Server: _1 - English; 9 - Русский_  Задаём переменную среды PATH

```text
export PATH=/opt/ssis/bin:$PATH
```

[Извлечение, преобразование и загрузка данных в Linux с помощью служб SSIS](https://docs.microsoft.com/ru-ru/sql/linux/sql-server-linux-migrate-ssis?view=sql-server-ver15)

[Планирование выполнения пакетов SQL Server Integration Services в Linux с помощью cron](https://docs.microsoft.com/ru-ru/sql/linux/sql-server-linux-schedule-ssis-packages?view=sql-server-ver15)

