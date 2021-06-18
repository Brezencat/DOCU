# Разные заметки по использованию GIT

...

---
## Заметки по настройке GIT на локальном компьютере

Настройки GIT находятся в файле gitconfig. \
Через консоль настройки осуществляются командой `git config`

#### Ошибка проверки SSL сертификата
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
