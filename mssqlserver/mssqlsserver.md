# MS SQL Server. Установка и настройка на Linux Ubuntu.

## Утсановка

### [Установка служб SQL Server Integration Services (SSIS)](https://docs.microsoft.com/ru-ru/sql/linux/sql-server-linux-setup-ssis?view=sql-server-ver15)
Установка `sudo apt-get install -y mssql-server-is`
продолжить установку

## Настройка

### [Включение агента SQL Server](https://docs.microsoft.com/ru-ru/sql/linux/sql-server-linux-setup-sql-agent?view=sql-server-ver15#EnableAgentAfterCU4)
Для версии от SQL Server 2017 CU4
```
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
sudo systemctl restart mssql-server
```
[Создание и запуск заданий агента SQL Server в Linux](https://docs.microsoft.com/ru-ru/sql/linux/sql-server-linux-run-sql-server-agent-job?view=sql-server-ver15)\
[Агент SQL Server](https://docs.microsoft.com/ru-ru/sql/ssms/agent/sql-server-agent?view=sql-server-ver15) (эту часть в дальнейшем перенести в раздел по SQL и заменить ссылку)

### [Настройка SQL Server Integration Services в Linux с помощью ssis-conf](https://docs.microsoft.com/ru-ru/sql/linux/sql-server-linux-configure-ssis?view=sql-server-ver15)
