# О самом файле .gitignore

.gitignore используется для скрытия файлов и папок от системы контроля версий Git. Для описания использует [glob формат](https://www.wikiwand.com/en/Glob_(programming)).

## Основной синтаксис
* каждая строка - отдельный шаблон
* пустые строки - игнорируются
* символ шарп (#) в начале строки - строка комментария
* символ восклицательный знак (!) в начале строки -  инвертирует шаблон (исключение из исключения)
* символ слеша (/) в начале строки - текущая папка (где лежит .gitignore)
* символ звёздочка (*) - любое количество символов
* символ две звёздочки (**) - все подпапки каталога
* правило игнорирования всей директории должно оканчиваться на слэш (/), в противном случае это имя файла
* символ обратный слэш (\\) - экранирование спецсимволов 

## Пример .gitignore
```bash
# Игнорирует файлы .DS_Store и settings.json
.DS_Store
settings.json

# Игнорирует директорию .vscode/
.vscode/

# Не игнорирует конкретный файл в конкретной директории
!.vscode/settings.json

# Игнорирует .json файлы в корне проекта
# Например, файл .vscode/settings.json не игнорируется этим правилом, потому что находится не в корне
/*.json

# Игнорирует .json файлы из папки .vscode не включая подпапки
# Наприме, файл .vscode/project/tasks.json не игнорируется этим правилом, потому что находится в подпапке project
/.vscode/*.json

# Игнорирует .json файлы из папки .vscode и подпапок, если они есть
/.vscode/**.*.json

# Игнорирует все файлы с расширением .json во всём репозитории
*.json

# Игнорирует директорию .vscode/ но не подпапку .vscode/project/
/.vscode/
!/.vscode/project/
```

### Репозиторий с шаблонами .gitignore
https://github.com/github/gitignore


## Мой шаблон файла .gitignore
```bash
# VS Code files for those working on multiple tools
.vscode/*
*.code-workspace
!.vscode/tasks.json
!.vscode/launch.json
!.vscode/extensions.json
#!!! stored credential from sqltools !!!
#!.vscode/settings.json 

# Local History for Visual Studio Code
.history/
*.app
.snapshots/*

# Built Visual Studio Code Extensions
*.vsix


# for MacOS
# General 
.DS_Store
.AppleDouble
.LSOverride
# Thumbnails
._*
# Files that might appear in the root of a volume
.DocumentRevisions-V100
.fseventsd
.Spotlight-V100
.TemporaryItems
.Trashes
.VolumeIcon.icns
.com.apple.timemachine.donotpresent
# Directories potentially created on remote AFP share
.AppleDB
.AppleDesktop
Network Trash Folder
Temporary Items
.apdisk
```