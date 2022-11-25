# Изменить комментарий к коммиту в Git

## Изменить комментарий последнего коммита
Если коммит не был отправлен в удалённый репозиторий
```sh
git commit --amend -m 'New commit message'
```

Если коммит был отправлен в удалённый репозиторий, то придётся принудительно запушить изменения
```sh
git push --force <branch-name>
```
или
```sh
git push -f origin
```

## Изменить комментарий у нескольких (или одного) коммитов (более поздних)
Используем ребеёз в интерактивном режиме. Указываем количество последних коммитов.\
_Например, если требуется изменить более старый коммит, то с мотрим в истории, какой он по счёту от текущего (HEAD) и указваем это число._
```sh
git rebase -i HEAD~3
```
Откроется текстовый редактор с подсказками, примерно такого вида:
```sh
pick 64e2b94 Fix. Table...
pick eb538db Add. New procedure...
pick c427a24 Add. New table...

# Rebase ... onto ... (3 commands)
#
# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into previous commit
# f, fixup = like "squash", but discard this commit's log message
# x, exec = run command (the rest of the line) using shell
# d, drop = remove commit
...
```
Напротив строк с нашими коммитами меняем слово `pick` на `reword` (или сокращённо r).
```sh
pick 64e2b94 Fix. Table...
pick eb538db Add. New procedure...
r c427a24 Add. New table...
```
Сохраняем, закрываем окно текстового редвктора.\
После чего откроется новое окно тестового редактора для каждого коммита, где необходимо произвести изменения (напротив которого проставили r). Правим текст коммита:
```sh
Add. New table...
-->>
Add. New table... and function
```
Сохраняем, закрываем.\
И принудительно отправляем изменения на сервер:
```sh
git push -f origin
```
