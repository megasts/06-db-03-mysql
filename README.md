# Домашнее задание к занятию 3. «MySQL» - `Шульгатый Станислав`

## Введение

Перед выполнением задания вы можете ознакомиться с 
[дополнительными материалами](https://github.com/netology-code/virt-homeworks/blob/virt-11/additional/README.md).

## Задача 1

Используя Docker, поднимите инстанс MySQL (версию 8). Данные БД сохраните в volume.

Изучите [бэкап БД](https://github.com/netology-code/virt-homeworks/tree/virt-11/06-db-03-mysql/test_data) и 
восстановитесь из него.

Перейдите в управляющую консоль `mysql` внутри контейнера.

Используя команду `\h`, получите список управляющих команд.

Найдите команду для выдачи статуса БД и **приведите в ответе** из её вывода версию сервера БД.

Подключитесь к восстановленной БД и получите список таблиц из этой БД.

**Приведите в ответе** количество записей с `price` > 300.

В следующих заданиях мы будем продолжать работу с этим контейнером.


---
### Ответ

1. Версия сервера БД:

![Screenshot1_1](https://github.com/megasts/06-db-03-mysql/blob/main/img/Screenshot1_1.png)

2. Список таблиц:

![Screenshot1_2](https://github.com/megasts/06-db-03-mysql/blob/main/img/Screenshot1_2.png)

3. Количество записей с `price` > 300:

![Screenshot1_3](https://github.com/megasts/06-db-03-mysql/blob/main/img/Screenshot1_3.png)

---

## Задача 2

Создайте пользователя test в БД c паролем test-pass, используя:

- плагин авторизации mysql_native_password
- срок истечения пароля — 180 дней 
- количество попыток авторизации — 3 
- максимальное количество запросов в час — 100
- аттрибуты пользователя:
    - Фамилия "Pretty"
    - Имя "James".

Предоставьте привелегии пользователю `test` на операции SELECT базы `test_db`.
    
Используя таблицу INFORMATION_SCHEMA.USER_ATTRIBUTES, получите данные по пользователю `test` и 
**приведите в ответе к задаче**.

---
### Ответ

1. Создание пользователя test:

![Screenshot2_1](https://github.com/megasts/06-db-03-mysql/blob/main/img/Screenshot2_1.png)

2. Предоставьте привелегии пользователю `test`:

![Screenshot2_2](https://github.com/megasts/06-db-03-mysql/blob/main/img/Screenshot2_2.png)

![Screenshot2_3](https://github.com/megasts/06-db-03-mysql/blob/main/img/Screenshot2_3.png)

3. Данные по пользователю `test`:

![Screenshot2_4](https://github.com/megasts/06-db-03-mysql/blob/main/img/Screenshot2_4.png)

---

## Задача 3

Установите профилирование `SET profiling = 1`.
Изучите вывод профилирования команд `SHOW PROFILES;`.

Исследуйте, какой `engine` используется в таблице БД `test_db` и **приведите в ответе**.

Измените `engine` и **приведите время выполнения и запрос на изменения из профайлера в ответе**:
- на `MyISAM`,
- на `InnoDB`.

---
### Ответ

1. Какой `engine` используется в таблице БД `test_db`:

![Screenshot3_1](https://github.com/megasts/06-db-03-mysql/blob/main/img/Screenshot3_1.png)

2. время выполнения и запрос на изменения из профайлера:

![Screenshot3_2](https://github.com/megasts/06-db-03-mysql/blob/main/img/Screenshot3_2.png)

---

## Задача 4 

Изучите файл `my.cnf` в директории /etc/mysql.

Измените его согласно ТЗ (движок InnoDB):

- скорость IO важнее сохранности данных;
- нужна компрессия таблиц для экономии места на диске;
- размер буффера с незакомиченными транзакциями 1 Мб;
- буффер кеширования 30% от ОЗУ;
- размер файла логов операций 100 Мб.

Приведите в ответе изменённый файл `my.cnf`.

---
### Ответ

Изменённый файл `my.cnf`:

```bash
# For advice on how to change settings please see
# http://dev.mysql.com/doc/refman/8.0/en/server-configuration-defaults.html

[mysqld]
#
# Remove leading # and set to the amount of RAM for the most important data
# cache in MySQL. Start at 70% of total RAM for dedicated server, else 10%.
# innodb_buffer_pool_size = 128M
#
# Remove leading # to turn on a very important data integrity option: logging
# changes to the binary log between backups.
# log_bin
#
# Remove leading # to set options mainly useful for reporting servers.
# The server defaults are faster for transactions and fast SELECTs.
# Adjust sizes as needed, experiment to find the optimal values.
# join_buffer_size = 128M
# sort_buffer_size = 2M
# read_rnd_buffer_size = 2M

# Remove leading # to revert to previous value for default_authentication_plugin,
# this will increase compatibility with older clients. For background, see:
# https://dev.mysql.com/doc/refman/8.0/en/server-system-variables.html#sysvar_default_authentication_plugin
# default-authentication-plugin=mysql_native_password
skip-host-cache
skip-name-resolve
datadir=/var/lib/mysql
socket=/var/run/mysqld/mysqld.sock
secure-file-priv=/var/lib/mysql-files
user=mysql

pid-file=/var/run/mysqld/mysqld.pid


innodb_flush_log_at_trx_commit = 2
innodb_file_per_table = ON
innodb_log_buffer_size = 1M
innodb_buffer_pool_size = 2457M
innodb_log_file_size = 100M

innodb_flush_method = O_DSYNC
query_cache_size = 0

[client]
socket=/var/run/mysqld/mysqld.sock

!includedir /etc/mysql/conf.d/
```
---

---

### Как оформить ДЗ

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---

