# devops-netology  
## Шевякин Кирилл  

# Домашнее задание к занятию "6.2. SQL"

## Задача 1

Используя docker поднимите инстанс PostgreSQL (версию 12) c 2 volume, 
в который будут складываться данные БД и бэкапы.

Приведите получившуюся команду или docker-compose манифест.

## Ответ
```
version: "3.1"
services:
  postgres:
    image: postgres:12
    restart: always
    environment:
      - POSTGRES_DB=netologydb
      - POSTGRES_USER=netologydbuser
      - POSTGRES_PASSWORD=Jx4LnmGHAPic9g
    ports:
      - ${POSTGRES_PORT:-5432}:5432
    volumes:
      - /mnt/db:/var/lib/postgresql/data
      - /mnt/backup:/backup
```

## Задача 2

В БД из задачи 1: 
- создайте пользователя test-admin-user и БД test_db
- в БД test_db создайте таблицу orders и clients (спeцификация таблиц ниже)
- предоставьте привилегии на все операции пользователю test-admin-user на таблицы БД test_db
- создайте пользователя test-simple-user  
- предоставьте пользователю test-simple-user права на SELECT/INSERT/UPDATE/DELETE данных таблиц БД test_db

Таблица orders:
- id (serial primary key)
- наименование (string)
- цена (integer)

Таблица clients:
- id (serial primary key)
- фамилия (string)
- страна проживания (string, index)
- заказ (foreign key orders)

Приведите:
- итоговый список БД после выполнения пунктов выше,
- описание таблиц (describe)
- SQL-запрос для выдачи списка пользователей с правами над таблицами test_db
- список пользователей с правами над таблицами test_db

### Ответ

- итоговый список БД после выполнения пунктов выше  
![image](https://user-images.githubusercontent.com/93198418/170047020-a981fc17-e70c-4354-951d-0c1530c84ffb.png)  

- описание таблиц (describe)  
![image](https://user-images.githubusercontent.com/93198418/170049334-098e547c-5ece-49b3-900d-ca822e244a68.png)  
![image](https://user-images.githubusercontent.com/93198418/170049616-a022d012-e927-44c2-a32f-c9ebf54acebd.png)  

- SQL-запрос для выдачи списка пользователей с правами над таблицами test_db
![image](https://user-images.githubusercontent.com/93198418/170231304-3741349c-fea4-4081-848b-38c8f00d6a6a.png)  
![image](https://user-images.githubusercontent.com/93198418/170231474-0ca76ffc-1645-4750-8ddf-f010a8cf3e47.png)  

- список пользователей с правами над таблицами test_db  
![image](https://user-images.githubusercontent.com/93198418/170051506-f9e8a6cf-cd56-45f0-98b8-61f1dfadf2db.png)  
![image](https://user-images.githubusercontent.com/93198418/170051651-7ab317e7-7d0b-4d70-a862-088aa965025a.png)  



## Задача 3

Используя SQL синтаксис - наполните таблицы следующими тестовыми данными:

Таблица orders

|Наименование|цена|
|------------|----|
|Шоколад| 10 |
|Принтер| 3000 |
|Книга| 500 |
|Монитор| 7000|
|Гитара| 4000|

Таблица clients

|ФИО|Страна проживания|
|------------|----|
|Иванов Иван Иванович| USA |
|Петров Петр Петрович| Canada |
|Иоганн Себастьян Бах| Japan |
|Ронни Джеймс Дио| Russia|
|Ritchie Blackmore| Russia|

Используя SQL синтаксис:
- вычислите количество записей для каждой таблицы 
- приведите в ответе:
    - запросы 
    - результаты их выполнения.

### Ответ  
- вычислите количество записей для каждой таблицы  
![image](https://user-images.githubusercontent.com/93198418/170188707-2a0d3c0e-b97a-46be-b64f-46b146eaffb9.png)  
![image](https://user-images.githubusercontent.com/93198418/170188860-79b2eaa3-30cc-43d2-9489-80e10b7f09f0.png)  

## Задача 4

Часть пользователей из таблицы clients решили оформить заказы из таблицы orders.

Используя foreign keys свяжите записи из таблиц, согласно таблице:

|ФИО|Заказ|
|------------|----|
|Иванов Иван Иванович| Книга |
|Петров Петр Петрович| Монитор |
|Иоганн Себастьян Бах| Гитара |

Приведите SQL-запросы для выполнения данных операций.

Приведите SQL-запрос для выдачи всех пользователей, которые совершили заказ, а также вывод данного запроса.
 
Подсказка - используйте директиву `UPDATE`.

### Ответ  

update clients set заказ = 3 where фамилия = 'Иванов Иван Иванович';  
update clients set заказ = 4 where фамилия = 'Петров Петр Петрович';  
update clients set заказ = 5 where фамилия = 'Иоганн Себастьян Бах';  
SELECT id, фамилия, "страна проживания", заказ FROM clients WHERE заказ notnull;  
![image](https://user-images.githubusercontent.com/93198418/170244659-085e0963-3bc5-4af6-a9d7-17c1ddcf31ee.png)


## Задача 5

Получите полную информацию по выполнению запроса выдачи всех пользователей из задачи 4 
(используя директиву EXPLAIN).

Приведите получившийся результат и объясните что значат полученные значения.

### Ответ  

Сделаю сразу EXPLAIN ANALYZE для более интересного вывода  
![image](https://user-images.githubusercontent.com/93198418/170247548-aacdd6b0-c92e-4a79-8528-387da954f900.png)  
  Seq Scan on clients  (cost=0.00..18.10 rows=806 width=72) (actual time=0.021..0.024 rows=3 loops=1) - сканирование таблицы clients, на которую будет потрачено 0.00..18.10 ресурсов и 0.021..0.024 времени  
  Filter: ("заказ" IS NOT NULL) - фильтрация по колонке "заказ"  
  Rows Removed by Filter: 2 - удаление строк после фильтрации  
  Planning Time: 0.089 ms - запланированное время  
  Execution Time: 0.046 ms - время исполнения запроса  

## Задача 6

Создайте бэкап БД test_db и поместите его в volume, предназначенный для бэкапов (см. Задачу 1).

Остановите контейнер с PostgreSQL (но не удаляйте volumes).

Поднимите новый пустой контейнер с PostgreSQL.

Восстановите БД test_db в новом контейнере.

Приведите список операций, который вы применяли для бэкапа данных и восстановления. 

### Ответ  

Создайте бэкап БД test_db и поместите его в volume, предназначенный для бэкапов (см. Задачу 1).  
pg_dump test_db > /backup/test_db-backup  

Остановите контейнер с PostgreSQL (но не удаляйте volumes).  
docker stop 6_2_postgres_1  

Поднимите новый пустой контейнер с PostgreSQL.  
root@test-netology:/mnt/6_2# cd 6_2_6/  
root@test-netology:/mnt/6_2/6_2_6# nano docker-compose.yml  
```  
version: "3.1"
services:
  postgres:
    image: postgres:12
    restart: always
    ports:
      - ${POSTGRES_PORT:-5432}:5432
    volumes:
      - /mnt/backup:/backup
```  
root@test-netology:/mnt/6_2/6_2_6# docker-compose up -d  

Восстановите БД test_db в новом контейнере.  



