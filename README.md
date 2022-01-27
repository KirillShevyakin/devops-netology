# devops-netology  
## Шевякин Кирилл  

### Домашнее задание к занятию "3.4. Операционные системы, лекция 2"
  
1) На лекции мы познакомились с node_exporter. В демонстрации его исполняемый файл запускался в background. Этого достаточно для демо, но не для настоящей production-системы, где процессы должны находиться под внешним управлением. Используя знания из лекции по systemd, создайте самостоятельно простой unit-файл для node_exporter:

поместите его в автозагрузку,
предусмотрите возможность добавления опций к запускаемому процессу через внешний файл (посмотрите, например, на systemctl cat cron),
удостоверьтесь, что с помощью systemctl процесс корректно стартует, завершается, а после перезагрузки автоматически поднимается.

![image](https://user-images.githubusercontent.com/93198418/151307958-94f8468b-8d81-46c8-9897-e3e72ad0341b.png)  
![image](https://user-images.githubusercontent.com/93198418/151308801-ccfa88e5-e5e2-4fea-9268-f04e5ccc53dc.png)  
![image](https://user-images.githubusercontent.com/93198418/150731433-c0b51763-a46f-40ec-96c0-0cec85dd1ca1.png)  
![image](https://user-images.githubusercontent.com/93198418/150731558-0e5d8541-e06d-4405-a0d1-ed1f70022cf6.png)  
![image](https://user-images.githubusercontent.com/93198418/150731635-25bd9bb7-dc59-46ac-aec0-c10fd80de034.png)  
![image](https://user-images.githubusercontent.com/93198418/150731722-19031a91-ca8b-47ca-ae2f-cc2c63cbefaf.png)  

2) Ознакомьтесь с опциями node_exporter и выводом /metrics по-умолчанию. Приведите несколько опций, которые вы бы выбрали для базового мониторинга хоста по CPU, памяти, диску и сети.  

CPU:  
node_cpu_seconds_total{cpu="0",mode="idle"} 1.17889732e+06  
node_cpu_seconds_total{cpu="0",mode="iowait"} 109.02  
node_cpu_seconds_total{cpu="0",mode="irq"} 0  
node_cpu_seconds_total{cpu="0",mode="nice"} 1.9  
node_cpu_seconds_total{cpu="0",mode="softirq"} 64.2  
node_cpu_seconds_total{cpu="0",mode="steal"} 0  
node_cpu_seconds_total{cpu="0",mode="system"} 13843.17  
node_cpu_seconds_total{cpu="0",mode="user"} 7354.54  

Memory:  
node_memory_MemFree_bytes 1.16965376e+08  
node_memory_MemAvailable_bytes 5.11209472e+08  
node_memory_MemTotal_bytes 1.028685824e+09  

Disk:  
node_disk_io_time_seconds_total{device="dm-0"} 354.856  
node_disk_io_time_seconds_total{device="dm-1"} 0.336  
node_disk_io_time_seconds_total{device="sda"} 355.036  

node_disk_read_time_seconds_total{device="dm-0"} 297.672  
node_disk_read_time_seconds_total{device="dm-1"} 0.28800000000000003  
node_disk_read_time_seconds_total{device="sda"} 135.499  

node_disk_write_time_seconds_total{device="dm-0"} 1832.06  
node_disk_write_time_seconds_total{device="dm-1"} 0  
node_disk_write_time_seconds_total{device="sda"} 345.059  

Network:  
node_network_receive_bytes_total{device="eth0"} 1.1063333e+07  
node_network_receive_bytes_total{device="lo"} 376387  
node_network_transmit_bytes_total{device="eth0"} 3.168707e+06  
node_network_transmit_bytes_total{device="lo"} 376387  
node_network_transmit_errs_total{device="eth0"} 0  
node_network_transmit_errs_total{device="lo"} 0  
node_network_transmit_packets_total{device="eth0"} 27575  
node_network_transmit_packets_total{device="lo"} 807  

3) Установите в свою виртуальную машину Netdata. Воспользуйтесь готовыми пакетами для установки (sudo apt install -y netdata). После успешной установки:

в конфигурационном файле /etc/netdata/netdata.conf в секции [web] замените значение с localhost на bind to = 0.0.0.0,
добавьте в Vagrantfile проброс порта Netdata на свой локальный компьютер и сделайте vagrant reload:  
```
config.vm.network "forwarded_port", guest: 19999, host: 19999  
```  
После успешной перезагрузки в браузере на своем ПК (не в виртуальной машине) вы должны суметь зайти на localhost:19999. Ознакомьтесь с метриками, которые по умолчанию собираются Netdata и с комментариями, которые даны к этим метрикам.  

![image](https://user-images.githubusercontent.com/93198418/150759298-0137d4d6-e834-4326-a724-d756fe909222.png)  

4) Можно ли по выводу dmesg понять, осознает ли ОС, что загружена не на настоящем оборудовании, а на системе виртуализации?

Можно  
![image](https://user-images.githubusercontent.com/93198418/150760492-cc0aeb20-f6bb-45f5-8078-09b45f50e7f3.png)  

5) Как настроен sysctl fs.nr_open на системе по-умолчанию? Узнайте, что означает этот параметр. Какой другой существующий лимит не позволит достичь такого числа (ulimit --help)?

![image](https://user-images.githubusercontent.com/93198418/150761208-ded9de2e-4085-431c-8543-be5e0ae3b709.png)  
fs.nr_open - это лимит открытия файлов в 1 процессе

![image](https://user-images.githubusercontent.com/93198418/150762481-cc3b4dae-c1cb-422d-966a-00bda48fb2a8.png)  
Поскольку в ulimit количество всего открытых файлов 1024, то это не даст сработать fs.nr_open

6) Запустите любой долгоживущий процесс (не ls, который отработает мгновенно, а, например, sleep 1h) в отдельном неймспейсе процессов; покажите, что ваш процесс работает под PID 1 через nsenter. Для простоты работайте в данном задании под root (sudo -i). Под обычным пользователем требуются дополнительные опции (--map-root-user) и т.д.

![image](https://user-images.githubusercontent.com/93198418/150772857-249ebd89-4a5b-48e2-836b-769c9199efb6.png)  
![image](https://user-images.githubusercontent.com/93198418/150772914-89afa0e4-bea6-44b3-a874-f3f70184cde9.png)  

7) Найдите информацию о том, что такое :(){ :|:& };:. Запустите эту команду в своей виртуальной машине Vagrant с Ubuntu 20.04 (это важно, поведение в других ОС не проверялось). Некоторое время все будет "плохо", после чего (минуты) – ОС должна стабилизироваться. Вызов dmesg расскажет, какой механизм помог автоматической стабилизации. Как настроен этот механизм по-умолчанию, и как изменить число процессов, которое можно создать в сессии?

:(){ :|:& };: - это функция, которая параллельно пускает два своих экземпляра. Каждый пускает ещё по два и т.д.

![image](https://user-images.githubusercontent.com/93198418/150776011-ae54589a-8ad1-45ba-8e2e-bff7e09f3a97.png)  
![image](https://user-images.githubusercontent.com/93198418/150781023-e43d3302-2f12-4f03-b97a-1e1d323aa509.png)  
![image](https://user-images.githubusercontent.com/93198418/150781639-15d15cc4-848c-49aa-98d0-21dd3e1653b4.png)  
cgroup: fork rejected by pids controller in /user.slice/user-1000.slice/session-9.scope  

![image](https://user-images.githubusercontent.com/93198418/150781255-c083ddc4-3f86-436d-afde-1c17dd1faf85.png)  
limit на количество task в сессии не позволил сделать больше  
Для того, чтобы увеличить или уменьшить этот limit, нужно поменять это значение: /sys/fs/cgroup/pids/user.slice/user-1000.slice/pids.max  





