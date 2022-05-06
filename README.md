# devops-netology  
## Шевякин Кирилл  

# Домашнее задание к занятию "5.5. Оркестрация кластером Docker контейнеров на примере Docker Swarm"  

## Задача 1  

Дайте письменые ответы на следующие вопросы:  

- В чём отличие режимов работы сервисов в Docker Swarm кластере: replication и global?  
- Какой алгоритм выбора лидера используется в Docker Swarm кластере?  
- Что такое Overlay Network?  

### Ответ  

- В чём отличие режимов работы сервисов в Docker Swarm кластере: replication и global?   
  Реплицированные service: указанное количество реплицируемых контейнеров распределяются между узлами на основе стратегии планированния  
  Глобальные service: один контейнер запускается на каждом доступном узле в кластере  
  
- Какой алгоритм выбора лидера используется в Docker Swarm кластере?  
  Используется алгоритм поддержания распределенного консенсуса — Raft. 
  
- Что такое Overlay Network?  
  Это сеть, построенная поверх других сетей. Для docker - это сеть, для общения нод между собой.  

## Задача 2  

Создать ваш первый Docker Swarm кластер в Яндекс.Облаке  

Для получения зачета, вам необходимо предоставить скриншот из терминала (консоли), с выводом команды:  
``` 
docker node ls
```

### Ответ  

![image](https://user-images.githubusercontent.com/93198418/166879860-8d333a0d-080c-4677-a3a7-aad22d161175.png)  

## Задача 3

Создать ваш первый, готовый к боевой эксплуатации кластер мониторинга, состоящий из стека микросервисов.  

Для получения зачета, вам необходимо предоставить скриншот из терминала (консоли), с выводом команды:  
```
docker service ls
```

### Ответ  

![image](https://user-images.githubusercontent.com/93198418/166880131-1b01d4a2-f3ec-418c-a995-e781a8dc1d32.png)  

## Задача 4 (*)

Выполнить на лидере Docker Swarm кластера команду (указанную ниже) и дать письменное описание её функционала, что она делает и зачем она нужна:  
```
# см.документацию: https://docs.docker.com/engine/swarm/swarm_manager_locking/  
docker swarm update --autolock=true
```

### Ответ  

docker swarm update --autolock=true - это включение автоблокировки существующего роя. Это нужно для того, чтобы изменения в рое можно было делать только по специальному ключу, сгенерированному docker.
