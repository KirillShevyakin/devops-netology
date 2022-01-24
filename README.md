# devops-netology  
## Шевякин Кирилл  

### Домашнее задание к занятию "3.4. Операционные системы, лекция 2"
  
1) На лекции мы познакомились с node_exporter. В демонстрации его исполняемый файл запускался в background. Этого достаточно для демо, но не для настоящей production-системы, где процессы должны находиться под внешним управлением. Используя знания из лекции по systemd, создайте самостоятельно простой unit-файл для node_exporter:

поместите его в автозагрузку,
предусмотрите возможность добавления опций к запускаемому процессу через внешний файл (посмотрите, например, на systemctl cat cron),
удостоверьтесь, что с помощью systemctl процесс корректно стартует, завершается, а после перезагрузки автоматически поднимается.

![image](https://user-images.githubusercontent.com/93198418/150731305-096be1fd-d895-4cbe-966c-de3230c22f60.png)  
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

