# devops-netology  
## Шевякин Кирилл  

### Домашнее задание к занятию "3.3. Операционные системы, лекция 1" 
  
1) Какой системный вызов делает команда cd? В прошлом ДЗ мы выяснили, что cd не является самостоятельной программой, это shell builtin, поэтому запустить strace непосредственно на cd не получится. Тем не менее, вы можете запустить strace на /bin/bash -c 'cd /tmp'. В этом случае вы увидите полный список системных вызовов, которые делает сам bash при старте. Вам нужно найти тот единственный, который относится именно к cd. Обратите внимание, что strace выдаёт результат своей работы в поток stderr, а не в stdout.  

![image](https://user-images.githubusercontent.com/93198418/150311164-5cf571e8-45d8-4954-a63a-6dc5dc714494.png)  
chdir("/tmp")  

2) Попробуйте использовать команду file на объекты разных типов на файловой системе. Например:  
```   
vagrant@netology1:~$ file /dev/tty    
/dev/tty: character special (5/0)    
vagrant@netology1:~$ file /dev/sda    
/dev/sda: block special (8/0)  
vagrant@netology1:~$ file /bin/bash  
/bin/bash: ELF 64-bit LSB shared object, x86-64  
```
  
Используя strace выясните, где находится база данных file на основании которой она делает свои догадки.  
  
![image](https://user-images.githubusercontent.com/93198418/150312672-7f42c9df-b1a0-4168-82ae-55c119ff3e8a.png)  
openat(AT_FDCWD, "/usr/share/misc/magic.mgc", O_RDONLY) = 3  

3) Предположим, приложение пишет лог в текстовый файл. Этот файл оказался удален (deleted в lsof), однако возможности сигналом сказать приложению переоткрыть файлы или просто перезапустить приложение – нет. Так как приложение продолжает писать в удаленный файл, место на диске постепенно заканчивается. Основываясь на знаниях о перенаправлении потоков предложите способ обнуления открытого удаленного файла (чтобы освободить место на файловой системе).  

![image](https://user-images.githubusercontent.com/93198418/150329023-9c78e33e-6aed-48b4-9136-baa5ec85d840.png)  
![image](https://user-images.githubusercontent.com/93198418/150329144-8e858135-d659-434f-990c-a39d4b5d22d3.png)  
![image](https://user-images.githubusercontent.com/93198418/150329301-ed406a05-450b-478f-b470-5c0401f41202.png)  
![image](https://user-images.githubusercontent.com/93198418/150329654-21826262-682d-4c72-ac2f-2d39dfe1f53e.png)  
![image](https://user-images.githubusercontent.com/93198418/150329720-6d8783c5-cf48-41a1-9733-2f436a6772ef.png)  

4) Занимают ли зомби-процессы какие-то ресурсы в ОС (CPU, RAM, IO)?  

![image](https://user-images.githubusercontent.com/93198418/150331968-57bf2298-e3cc-4633-9629-98bc2add95cb.png)  
Зомби-процессы ничего не используют, кроме записи в таблице процессов  

5) В iovisor BCC есть утилита opensnoop:  
```
root@vagrant:~# dpkg -L bpfcc-tools | grep sbin/opensnoop  
/usr/sbin/opensnoop-bpfcc  
```  
На какие файлы вы увидели вызовы группы open за первую секунду работы утилиты? Воспользуйтесь пакетом bpfcc-tools для Ubuntu 20.04. Дополнительные сведения по установке.  


