# devops-netology  
## Шевякин Кирилл  

# Домашнее задание к занятию "6.4. PostgreSQL"

## Задача 1

Используя docker поднимите инстанс PostgreSQL (версию 13). Данные БД сохраните в volume.

Подключитесь к БД PostgreSQL используя `psql`.

Воспользуйтесь командой `\?` для вывода подсказки по имеющимся в `psql` управляющим командам.

**Найдите и приведите** управляющие команды для:
- вывода списка БД
- подключения к БД
- вывода списка таблиц
- вывода описания содержимого таблиц
- выхода из psql

### Ответ  

- вывода списка БД  
\l[+]   [PATTERN]      list databases

- подключения к БД  
\conninfo              display information about current connection

- вывода списка таблиц  
\dt[S+] [PATTERN]      list tables

- вывода описания содержимого таблиц  
\d[S+]  NAME           describe table, view, sequence, or index  

- выхода из psql  
\q                     quit psql

## Задача 2

Используя `psql` создайте БД `test_database`.

Изучите [бэкап БД](https://github.com/netology-code/virt-homeworks/tree/master/06-db-04-postgresql/test_data).

Восстановите бэкап БД в `test_database`.

Перейдите в управляющую консоль `psql` внутри контейнера.

Подключитесь к восстановленной БД и проведите операцию ANALYZE для сбора статистики по таблице.

Используя таблицу [pg_stats](https://postgrespro.ru/docs/postgresql/12/view-pg-stats), найдите столбец таблицы `orders` 
с наибольшим средним значением размера элементов в байтах.

**Приведите в ответе** команду, которую вы использовали для вычисления и полученный результат.

### Ответ

test_database=# SELECT avg_width FROM pg_stats WHERE tablename='orders';  
![image](https://user-images.githubusercontent.com/93198418/172781192-382b971d-ae26-4429-b917-3e4cc33f79af.png)

## Задача 3

Архитектор и администратор БД выяснили, что ваша таблица orders разрослась до невиданных размеров и
поиск по ней занимает долгое время. Вам, как успешному выпускнику курсов DevOps в нетологии предложили
провести разбиение таблицы на 2 (шардировать на orders_1 - price>499 и orders_2 - price<=499).

Предложите SQL-транзакцию для проведения данной операции.

Можно ли было изначально исключить "ручное" разбиение при проектировании таблицы orders?

### Ответ

test_database=# CREATE TABLE orders_1 ( CHECK ( price > 499 ))INHERITS (orders);  
test_database=# CREATE TABLE orders_2 ( CHECK ( price <= 499 ))INHERITS (orders);  

Можно ли было изначально исключить "ручное" разбиение при проектировании таблицы orders?  
Можно. Есть специальная утилита для этого (https://github.com/2gis/partition_magic)  

## Задача 4

Используя утилиту `pg_dump` создайте бекап БД `test_database`.

Как бы вы доработали бэкап-файл, чтобы добавить уникальность значения столбца `title` для таблиц `test_database`?

### Ответ  

Используя утилиту `pg_dump` создайте бекап БД `test_database`.  
root@65aa5a0e8a5d:/var/lib/postgresql/data/pgdata# pg_dump -U test -d test_database > test_database_dump.sql

Как бы вы доработали бэкап-файл, чтобы добавить уникальность значения столбца `title` для таблиц `test_database`?  
Открыть файл  
root@test-netology:/mnt/6_4/pgdata# nano test_database_dump.sql  
Изменить  
```
CREATE TABLE public.orders (  
    id integer NOT NULL,  
    title character varying(80) NOT NULL,  
    price integer DEFAULT 0  
);  
```
На  
```
CREATE TABLE public.orders (  
    id integer NOT NULL,  
    title character varying(80) NOT NULL UNIQUE,  
    price integer DEFAULT 0  
);  
```
---
