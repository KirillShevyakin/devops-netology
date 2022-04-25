# devops-netology  
## Шевякин Кирилл  

# Домашнее задание к занятию "5.3. Введение. Экосистема. Архитектура. Жизненный цикл Docker контейнера"

## Задача 1

Сценарий выполения задачи:

- создайте свой репозиторий на https://hub.docker.com;
- выберете любой образ, который содержит веб-сервер Nginx;
- создайте свой fork образа;
- реализуйте функциональность:
запуск веб-сервера в фоне с индекс-страницей, содержащей HTML-код ниже:
```
<html>
<head>
Hey, Netology
</head>
<body>
<h1>I’m DevOps Engineer!</h1>
</body>
</html>
```
Опубликуйте созданный форк в своем репозитории и предоставьте ответ в виде ссылки на https://hub.docker.com/username_repo.

### Ответ  

https://hub.docker.com/r/kirillshevyakin/nginx

## Задача 2

Посмотрите на сценарий ниже и ответьте на вопрос:
"Подходит ли в этом сценарии использование Docker контейнеров или лучше подойдет виртуальная машина, физическая машина? Может быть возможны разные варианты?"

Детально опишите и обоснуйте свой выбор.

--

Сценарий:

- Высоконагруженное монолитное java веб-приложение;
- Nodejs веб-приложение;
- Мобильное приложение c версиями для Android и iOS;
- Шина данных на базе Apache Kafka;
- Elasticsearch кластер для реализации логирования продуктивного веб-приложения - три ноды elasticsearch, два logstash и две ноды kibana;
- Мониторинг-стек на базе Prometheus и Grafana;
- MongoDB, как основное хранилище данных для java-приложения;
- Gitlab сервер для реализации CI/CD процессов и приватный (закрытый) Docker Registry.

### Ответ  

- Высоконагруженное монолитное java веб-приложение;  
Может быть и отдельная виртуальная машина, и физическая машина. Потому что требуются большие мощности + монолитное приложение, которое невозможно разбить на микросервисы  

- Nodejs веб-приложение;  
Здесь лучше использовать Docker контейнеры. Nodejs веб-приложение можно разбить на микросервисы и разбить на контейнеры. Но также подойдет и виртуальная машина, физическая машина

- Мобильное приложение c версиями для Android и iOS;  
Здесь лучше использовать Docker контейнеры. Мобильное приложение c версиями для Android и iOS можно разбить на разные версии разных ОС и разбить на контейнеры, так будет правильно и приложение будет работать быстрее и лучше  

- Шина данных на базе Apache Kafka;  
У нас она реализована на отдельной виртуальной машине (использование отдельной железной не целесообразно). Приложение монолитное, требуется много разных настроек, не думаю что использование контейнеров тут возможно и необходимо. К тому же шина передает различные файлы с различных источников, тяжело прокинуть все возможные пути в контейнеры  

- Elasticsearch кластер для реализации логирования продуктивного веб-приложения - три ноды elasticsearch, два logstash и две ноды kibana;  
Это высоконагруженные сервисы, использующие одинаковые механизмы. Я бы предложил использование отдельных виртуальных машин под каждый сервис  

- Мониторинг-стек на базе Prometheus и Grafana;  
Это все можно сделать в контейнерах. Сейчас все это уже давно реализовано в контейнарах. Не надо тратить время на установки и настройки

- MongoDB, как основное хранилище данных для java-приложения;
Лучше конечно использовать отдельную виртуальную или физическую машину. Это очень высоконагруженное решение, постоянные чтение/запись БД. Best practices - не устанавливать высоконагруженные БД в контейнеры  

- Gitlab сервер для реализации CI/CD процессов и приватный (закрытый) Docker Registry.  
У нас реализовано в отдельной виртуальной машине. Но не вижу никаких проблем реализовать в контейнерах

## Задача 3

- Запустите первый контейнер из образа ***centos*** c любым тэгом в фоновом режиме, подключив папку ```/data``` из текущей рабочей директории на хостовой машине в ```/data``` контейнера;
- Запустите второй контейнер из образа ***debian*** в фоновом режиме, подключив папку ```/data``` из текущей рабочей директории на хостовой машине в ```/data``` контейнера;
- Подключитесь к первому контейнеру с помощью ```docker exec``` и создайте текстовый файл любого содержания в ```/data```;
- Добавьте еще один файл в папку ```/data``` на хостовой машине;
- Подключитесь во второй контейнер и отобразите листинг и содержание файлов в ```/data``` контейнера.

### Ответ  

1) root@server1:/home/vagrant# docker pull centos  
2) root@server1:/home/vagrant# docker run -d -it -v /data:/data --name centos_1 centos  
3) root@server1:/home/vagrant# docker pull debian  
4) root@server1:/home/vagrant# docker run -d -it -v /data:/data --name debian_1 debian  
5) root@server1:/home/vagrant# docker exec -it centos_1 /bin/bash  
6) [root@366b60d81236 /]# touch /data/test.txt  
7) [root@366b60d81236 /]# echo 'netology' > /data/test.txt  
8) root@server1:/home/vagrant# touch /data/test1.txt  
9) root@server1:/home/vagrant# docker exec -it debian_1 /bin/bash  
10) ![image](https://user-images.githubusercontent.com/93198418/164449064-079a2c14-f912-44f0-90bc-c0e2f967430b.png)  
11) ![image](https://user-images.githubusercontent.com/93198418/164449179-18ec6d7e-33a4-4875-bea7-8eb5784709e0.png)  

## Задача 4 (*)

Воспроизвести практическую часть лекции самостоятельно.

Соберите Docker образ с Ansible, загрузите на Docker Hub и пришлите ссылку вместе с остальными ответами к задачам.

### Ответ  

https://hub.docker.com/r/kirillshevyakin/ansible


```
# See http://help.ubuntu.com/community/UpgradeNotes for how to upgrade to
# newer versions of the distribution.
deb http://mirror-ubuntu20.vipservice.ru/mirror.yandex.ru/ubuntu focal main restricted
# deb-src http://archive.ubuntu.com/ubuntu focal main restricted

## Major bug fix updates produced after the final release of the
## distribution.
deb http://mirror-ubuntu20.vipservice.ru/mirror.yandex.ru/ubuntu focal-updates main restricted
# deb-src http://archive.ubuntu.com/ubuntu focal-updates main restricted

## N.B. software from this repository is ENTIRELY UNSUPPORTED by the Ubuntu
## team. Also, please note that software in universe WILL NOT receive any
## review or updates from the Ubuntu security team.
deb http://mirror-ubuntu20.vipservice.ru/mirror.yandex.ru/ubuntu focal universe
# deb-src http://archive.ubuntu.com/ubuntu focal universe
deb http://mirror-ubuntu20.vipservice.ru/mirror.yandex.ru/ubuntu focal-updates universe
# deb-src http://archive.ubuntu.com/ubuntu focal-updates universe

## N.B. software from this repository is ENTIRELY UNSUPPORTED by the Ubuntu
## team, and may not be under a free licence. Please satisfy yourself as to
## your rights to use the software. Also, please note that software in
## multiverse WILL NOT receive any review or updates from the Ubuntu
## security team.
deb http://mirror-ubuntu20.vipservice.ru/mirror.yandex.ru/ubuntu focal multiverse
# deb-src http://archive.ubuntu.com/ubuntu focal multiverse
deb http://mirror-ubuntu20.vipservice.ru/mirror.yandex.ru/ubuntu focal-updates multiverse
# deb-src http://archive.ubuntu.com/ubuntu focal-updates multiverse

## N.B. software from this repository may not have been tested as
## extensively as that contained in the main release, although it includes
## newer versions of some applications which may provide useful features.
## Also, please note that software in backports WILL NOT receive any review
## or updates from the Ubuntu security team.
deb http://mirror-ubuntu20.vipservice.ru/mirror.yandex.ru/ubuntu focal-backports main restricted universe multiverse
# deb-src http://archive.ubuntu.com/ubuntu focal-backports main restricted universe multiverse

## Uncomment the following two lines to add software from Canonical's
## 'partner' repository.
## This software is not part of Ubuntu, but is offered by Canonical and the
## respective vendors as a service to Ubuntu users.
# deb http://archive.canonical.com/ubuntu focal partner
# deb-src http://archive.canonical.com/ubuntu focal partner

deb http://mirror-ubuntu20.vipservice.ru/mirror.yandex.ru/ubuntu focal-security main restricted
# deb-src http://archive.ubuntu.com/ubuntu focal-security main restricted
deb http://mirror-ubuntu20.vipservice.ru/mirror.yandex.ru/ubuntu focal-security universe
# deb-src http://archive.ubuntu.com/ubuntu focal-security universe
deb http://mirror-ubuntu20.vipservice.ru/mirror.yandex.ru/ubuntu focal-security multiverse
# deb-src http://archive.ubuntu.com/ubuntu focal-security multiverse

deb http://mirror-ubuntu20.vipservice.ru/repo.zabbix.com/zabbix/5.0/ubuntu focal main
deb-src http://mirror-ubuntu20.vipservice.ru/repo.zabbix.com/zabbix/5.0/ubuntu focal main
```
