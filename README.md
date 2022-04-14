# devops-netology  
## Шевякин Кирилл  

# Домашнее задание к занятию "5.2. Применение принципов IaaC в работе с виртуальными машинами"


## Задача 1  

Опишите своими словами основные преимущества применения на практике IaaC паттернов.
Какой из принципов IaaC является основополагающим?

### Ответ  

- CI (Continuous Integration) - Непрерывная интеграция  
  основные преимущества: быстрая проверка работоспособности нового кода, быстрое обнаружение и исправление ошибок и за счет этого снижение трудозатрат  

- CD (Continuous Delivery) – Непрерывная доставка  
  основные преимущества: быстрое добавление новых фичей, быстрый откат, возможность быстрого развертывания небольших изменений  
  
- CD (Continuous Deployment) – Непрерывное развёртывание  
  основные преимущества: автоматическое развертывание на всех нодах, возможность обновления продукта по кнопке  
  
## Задача 2  

Чем Ansible выгодно отличается от других систем управление конфигурациями?  
Какой, на ваш взгляд, метод работы систем конфигурации более надёжный push или pull?  

### Ответ

Ansible выгодно отличается от других систем управление конфигурациями тем, что для его применения достаточно открытого порта ssh и настроенной на вм системы ssh..
С моей точки зрения метод push более надежный, потому что ты можешь контролировать когда и что и куда ты накатываешь.  

## Задача 3  

Установить на личный компьютер:  

VirtualBox  
Vagrant  
Ansible  
Приложить вывод команд установленных версий каждой из программ, оформленный в markdown.  

### Ответ
