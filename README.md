# devops-netology  
## Шевякин Кирилл  

# Домашнее задание к занятию "6.5. Elasticsearch"

## Задача 1

В этом задании вы потренируетесь в:
- установке elasticsearch
- первоначальном конфигурировании elastcisearch
- запуске elasticsearch в docker

Используя докер образ [elasticsearch:7](https://hub.docker.com/_/elasticsearch) как базовый:

- составьте Dockerfile-манифест для elasticsearch
- соберите docker-образ и сделайте `push` в ваш docker.io репозиторий
- запустите контейнер из получившегося образа и выполните запрос пути `/` c хост-машины

Требования к `elasticsearch.yml`:
- данные `path` должны сохраняться в `/var/lib`
- имя ноды должно быть `netology_test`

В ответе приведите:
- текст Dockerfile манифеста
- ссылку на образ в репозитории dockerhub
- ответ `elasticsearch` на запрос пути `/` в json виде

Подсказки:
- при сетевых проблемах внимательно изучите кластерные и сетевые настройки в elasticsearch.yml
- при некоторых проблемах вам поможет docker директива ulimit
- elasticsearch в логах обычно описывает проблему и пути ее решения
- обратите внимание на настройки безопасности такие как `xpack.security.enabled`
- если докер образ не запускается и падает с ошибкой 137 в этом случае может помочь настройка `-e ES_HEAP_SIZE`
- при настройке `path` возможно потребуется настройка прав доступа на директорию

Далее мы будем работать с данным экземпляром elasticsearch.

### Ответ  
- текст Dockerfile манифеста  
```
FROM elasticsearch:7.17.4

ENV TZ=Europe/Moscow
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt update -y
RUN apt install mc nano net-tools -y

COPY elasticsearch.yml /usr/share/elasticsearch/config/

ENV ES_HOME=/var/lib/data/elasticsearch

RUN mkdir /var/lib/logs && \
    chown elasticsearch:elasticsearch /var/lib/logs && \
    mkdir /var/lib/nodes && \
    chown elasticsearch:elasticsearch /var/lib/nodes && \
    mkdir /var/lib/data && \
    mkdir /var/lib/data/elasticsearch && \
    mkdir /var/lib/data/elasticsearch/snapshots && \
    chown -R elasticsearch:elasticsearch /var/lib/data

EXPOSE 9200

USER elasticsearch
CMD ["bin/elasticsearch"]
```

- ссылку на образ в репозитории dockerhub  
 docker push kirillshevyakin/elasticsearch:7.17.4 

- ответ `elasticsearch` на запрос пути `/` в json виде  
![image](https://user-images.githubusercontent.com/93198418/174241000-642fb090-d644-471f-9fb5-8eb546ec1152.png)  


## Задача 2

В этом задании вы научитесь:
- создавать и удалять индексы
- изучать состояние кластера
- обосновывать причину деградации доступности данных

Ознакомтесь с [документацией](https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-create-index.html)
и добавьте в `elasticsearch` 3 индекса, в соответствии со таблицей:

| Имя | Количество реплик | Количество шард |
|-----|-------------------|-----------------|
| ind-1| 0 | 1 |
| ind-2 | 1 | 2 |
| ind-3 | 2 | 4 |

Получите список индексов и их статусов, используя API и **приведите в ответе** на задание.

Получите состояние кластера `elasticsearch`, используя API.

Как вы думаете, почему часть индексов и кластер находится в состоянии yellow?

Удалите все индексы.

**Важно**

При проектировании кластера elasticsearch нужно корректно рассчитывать количество реплик и шард,
иначе возможна потеря данных индексов, вплоть до полной, при деградации системы.

### Ответ  
Получите список индексов и их статусов, используя API и **приведите в ответе** на задание.  
![image](https://user-images.githubusercontent.com/93198418/174247855-d043ff1c-de59-4f3c-9f70-5f6d313754d2.png)  

Получите состояние кластера `elasticsearch`, используя API.
![image](https://user-images.githubusercontent.com/93198418/174248078-02218d9d-c9b3-42f5-af3a-68ae3d26180a.png)  

Как вы думаете, почему часть индексов и кластер находится в состоянии yellow?  
Кластер yellow потому что есть "unassigned_shards" : 10  
А некоторые индексы потому что в них указаны реплики, а по факту реплик нет, потому что сервер 1  

Удалите все индексы.  
![image](https://user-images.githubusercontent.com/93198418/174249151-2340e562-2f26-4254-a754-5122fbc3f80f.png)  

## Задача 3

В данном задании вы научитесь:
- создавать бэкапы данных
- восстанавливать индексы из бэкапов

Создайте директорию `{путь до корневой директории с elasticsearch в образе}/snapshots`.

Используя API [зарегистрируйте](https://www.elastic.co/guide/en/elasticsearch/reference/current/snapshots-register-repository.html#snapshots-register-repository)
данную директорию как `snapshot repository` c именем `netology_backup`.

**Приведите в ответе** запрос API и результат вызова API для создания репозитория.

Создайте индекс `test` с 0 реплик и 1 шардом и **приведите в ответе** список индексов.

[Создайте `snapshot`](https://www.elastic.co/guide/en/elasticsearch/reference/current/snapshots-take-snapshot.html)
состояния кластера `elasticsearch`.

**Приведите в ответе** список файлов в директории со `snapshot`ами.

Удалите индекс `test` и создайте индекс `test-2`. **Приведите в ответе** список индексов.

[Восстановите](https://www.elastic.co/guide/en/elasticsearch/reference/current/snapshots-restore-snapshot.html) состояние
кластера `elasticsearch` из `snapshot`, созданного ранее.

**Приведите в ответе** запрос к API восстановления и итоговый список индексов.

Подсказки:
- возможно вам понадобится доработать `elasticsearch.yml` в части директивы `path.repo` и перезапустить `elasticsearch`

### Ответ  
Создайте директорию `{путь до корневой директории с elasticsearch в образе}/snapshots`.  
Уже создана /var/lib/data/elasticsearch/snapshots  
![image](https://user-images.githubusercontent.com/93198418/174253661-7412f111-453e-413f-9dd1-fa105ed7ecdd.png)  

**Приведите в ответе** запрос API и результат вызова API для создания репозитория.  
![image](https://user-images.githubusercontent.com/93198418/174268733-5347c143-a52d-47cc-9ef3-aa46b3c7cd56.png)
![image](https://user-images.githubusercontent.com/93198418/174269559-a514fed5-05fc-42e9-a027-0e365975241f.png)  

Создайте индекс `test` с 0 реплик и 1 шардом и **приведите в ответе** список индексов.  
![image](https://user-images.githubusercontent.com/93198418/174270267-cd2c6c99-e5dd-4731-862a-d38f45de1210.png)  

**Приведите в ответе** список файлов в директории со `snapshot`ами.  
![image](https://user-images.githubusercontent.com/93198418/174270927-7e70732e-1bdc-4525-b012-55e658d46c5b.png)  

Удалите индекс `test` и создайте индекс `test-2`. **Приведите в ответе** список индексов.  
![image](https://user-images.githubusercontent.com/93198418/174271354-4651d3da-bf91-4684-8340-50ff6a64febe.png)  

**Приведите в ответе** запрос к API восстановления и итоговый список индексов.  
![image](https://user-images.githubusercontent.com/93198418/174281805-23fbeb16-4e15-4f62-87f1-c1f0ed38a480.png)
