# Мои запросы для поиска (фильтрации) и составления отчётов

Запросы на JQL не сложные, но каждый раз их написание занимает значительное время.

#### Мои открытые задачи
Чаще всего это стандартный отчёт
```sql
assignee = currentUser() AND resolution = Unresolved order by updated DESC
```

#### Мои задачи - Все
```sql
assignee = currentUser() ORDER BY updated DESC
```

#### Мои задачи - Назначенные
Фильтры в status могут меняться от компании к компании.
```sql
assignee = currentUser() AND status in ("Select for development", Backlog, "To Do")
```

#### Мои задачи - Тестирование
```sql
assignee = currentUser() AND status = "Code review"
```

#### Я наблюдатель, не я исполнитель
```sql
(assignee != currentUser() OR assignee is EMPTY) AND watcher = currentUser() ORDER BY priority ASC, updated DESC
```
