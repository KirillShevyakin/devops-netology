# devops-netology  
## Шевякин Кирилл  

### Домашнее задание к занятию "3.2. Работа в терминале, лекция 2"  
  
1) Какого типа команда cd? Попробуйте объяснить, почему она именно такого типа; опишите ход своих мыслей, если считаете что она могла бы быть другого типа.  
  
![image](https://user-images.githubusercontent.com/93198418/149892155-69640daa-1d1c-4f0b-96f7-8c2dd5ec733f.png)  
        
Команда cd меняет рабочую директорию в shell. Это внутренняя команда в shell, которая вызывает внутренюю функцию в shell изменения рабочей директории. Я думаю, что она не может быть другого типа, потому что если бы она была внешним вызовом, то каждый раз при переходе в другую директорию, приходилось бы запускать новый shell.  

2) Какая альтернатива без pipe команде grep <some_string> <some_file> | wc -l? man grep поможет в ответе на этот вопрос. Ознакомьтесь с документом о других подобных некорректных вариантах использования pipe.  
  
![image](https://user-images.githubusercontent.com/93198418/149892265-3c81f51f-c564-4a52-8527-9f07d741ae58.png)  

Вместо grep <some_string> <some_file> | wc -l можно использовать grep -c <some_string> <some_file>  

3) Какой процесс с PID 1 является родителем для всех процессов в вашей виртуальной машине Ubuntu 20.04?  
  
  ![image](https://user-images.githubusercontent.com/93198418/149890591-0a3d8aab-2fb5-4435-997f-5ea29029a0db.png)  
  systemd - это менеджер начальной загрузки ОС  
  
4) Как будет выглядеть команда, которая перенаправит вывод stderr ls на другую сессию терминала?  

![image](https://user-images.githubusercontent.com/93198418/149893790-fb80a34b-29e9-43d7-986e-168baaa6fac2.png)  
![image](https://user-images.githubusercontent.com/93198418/149893897-d9686f87-6ed6-4014-903e-2bc76b03ca6c.png)  
![image](https://user-images.githubusercontent.com/93198418/149894002-594e10db-89f5-4ad7-b2fa-856d8a745fc2.png)  

5) Получится ли одновременно передать команде файл на stdin и вывести ее stdout в другой файл? Приведите работающий пример.  

![image](https://user-images.githubusercontent.com/93198418/149895163-904f9ae9-a5ec-42dd-bfd3-226b33e7f90a.png)  

6) Получится ли находясь в графическом режиме, вывести данные из PTY в какой-либо из эмуляторов TTY? Сможете ли вы наблюдать выводимые данные?  

![image](https://user-images.githubusercontent.com/93198418/149914773-81645400-b473-4c79-bcc7-489369fbbf99.png)  
![image](https://user-images.githubusercontent.com/93198418/149914835-a3a227b7-c364-4110-bc3a-56518ac3e551.png)  
![image](https://user-images.githubusercontent.com/93198418/149915100-59d64b44-30e3-41da-9f4b-adf260915caf.png)  
![image](https://user-images.githubusercontent.com/93198418/149915161-5a55c017-078b-4fbe-a81f-fc453b830bfc.png)  

Да можно, если перенаправить вывод, вот так например 1>/dev/tty1  

7) Выполните команду bash 5>&1. К чему она приведет? Что будет, если вы выполните echo netology > /proc/$$/fd/5? Почему так происходит?  








