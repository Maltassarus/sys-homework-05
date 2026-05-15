# Домашнее задание к занятию "`Резервное копирование баз данных`" - `Борзенко Андрея`

### Задание 1. Резервное копирование

1.1. Необходимо восстанавливать данные в полном объёме за предыдущий день:

Дифференциальный бэкап и полный бэкап.

Полный бэкап - раз в неделю.
Дифференциальный бэкап - ежедневно.


Либо инкрементные бэкапы ежедневно.

1.2. Необходимо восстанавливать данные за час до предполагаемой поломки

WAL-журналирование и инкрементные бэкапы

Полный бэкап — раз в сутки, инкрементные бэкапы — каждый час или постоянная архивация WAL-логов.

---

### Задание 2. PostgreSQL

Пример команды резервирования и восстановления

Резервное копирование:

```
pg_dump -U postgres -Fc -f backup.dump database
pg_dump -U postgres -t users -Fc -f users_backup.dump database
pg_dump -U postgres -Fp -f backup.sql database
pg_dumpall -U postgres -f all_databases.sql
```

Восстановление:

```
pg_restore -U postgres -d database backup.dump
pg_restore -U postgres -d database --clean --create backup.dump
psql -U postgres -d mydatabase < backup.sql
```

---

### Задание 3. MySQL

Пример команды инкрементного резервного копирования базы данных MySQL:

```
mysqlbackup --host=localhost \
            --user=root \
            --password=password \
            --incremental \
            --incremental-base=history:last_backup \
            --backup-dir=<path> \
            backup
```