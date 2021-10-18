# Сравнить изменения между двумя ветками

### Посмотреть отличия между двумя ветками
```bash
git diff branch1 branch2
```

### Посмотреть не сами изменения, а список отличающихся файлов
```bash
git diff --name-only branch1 branch2
```

### Посмотреть список отличающихся файлов со статусом изменения (добавлен/удалён/модифицирован)
```bash
git diff --name-status branch1 branch2
```

___
[Мануал git-diff](https://mirrors.edge.kernel.org/pub/software/scm/git/docs/git-diff.html)