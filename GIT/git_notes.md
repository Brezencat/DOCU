# Разные заметки по использованию GIT

...

---
## Заметки по настройке GIT на локальном компьютере

### Основные настройки
Настройки GIT находятся в файле .gitconfig. \
Через консоль настройки осуществляются командой `git config`. \
Проверить, какие настройки используются и из каких файлов с конфигурацией можно командой:
```bash
git config --list --show-origin
```
или
```bash
git config --list --show-origin --show-scope
```

#### Настройка отображаемого имени пользователя и e-mail для конкретного репозитория
```bash
git config --local user.name "Brezencat"
git config --local user.email "brezencat@gmail.com"
```

#### Настройка отображаемого имени пользователя и e-mail для коммитах в любых репозиториях, если эти занчения не установлены в локальном конфиге 
```bash
git config --global user.name "Dimon Martovskiy"
git config --global user.email "brezencat@gmail.com"
```

---

### Ошибка проверки SSL сертификата
Если в Windows при клонировании возникает ошибка
>Cloning into 'name_project'...
>fatal: unable to access 'https://git_url_project...': SSL certificate problem: unable to get local issuer certificate
То проблему можно решить двумя способома:
* отключить проверку SSL сертификата непосредственно при клонировании репозитория
```bash
GIT_SSL_NO_VERIFY=true git clone /path/to/repo
```
* настроить GIT на использование SChannel (подробней от [Microsoft](https://docs.microsoft.com/ru-ru/windows/win32/secauthn/secure-channel?redirectedfrom=MSDN))
```bash
git config --global http.sslbackend schannel
```

#### Отключение проверки SSL сертификата (не рекомендуется)
``` bash
git config --global http.sslVerify false
```

---

### Разное
#### Создание git hist (история и граф изменений)
```bash
git config --global alias.hist "log --pretty=format:'%C(yellow)[%ad]%C(reset) %C(green)[%h]%C(reset) | %C(red)%s %C(bold red){{%an}}%C(reset) %C(blue)%d%C(reset)' --graph --date=short"
```


