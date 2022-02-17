# devops-netology  
## Шевякин Кирилл  

### Домашнее задание к занятию "3.7. Компьютерные сети, лекция 2"

1) Проверьте список доступных сетевых интерфейсов на вашем компьютере. Какие команды есть для этого в Linux и в Windows?

Linux  
![image](https://user-images.githubusercontent.com/93198418/154421826-36dcf91f-6802-43ca-bf14-3b9c3357a8ae.png)  

Windows  
![image](https://user-images.githubusercontent.com/93198418/154422236-7b47788d-b4d8-412e-9c56-c00420a6b1ac.png)

2) Какой протокол используется для распознавания соседа по сетевому интерфейсу? Какой пакет и команды есть в Linux для этого?

Link Layer Discovery Protocol (LLDP) — протокол канального уровня, позволяющий сетевому оборудованию оповещать оборудование, работающее в локальной сети, о своём существовании и передавать ему свои характеристики, а также получать от него аналогичные сведения. Описание протокола приводится в стандарте IEEE 802.1AB-2009[1], формально утверждённом в сентябре 2009 года. Протокол не зависит от производителей сетевого оборудования и является заменой аналогичных, но патентованных протоколов, таких как Cisco Discovery Protocol, Extreme Discovery Protocol, Foundry Discovery Protocol и Nortel Discovery Protocol (последний также известен как SONMP).

root@vagrant:/home/vagrant# apt -y install lldpd  
root@vagrant:/home/vagrant# lldpctl  

3) Какая технология используется для разделения L2 коммутатора на несколько виртуальных сетей? Какой пакет и команды есть в Linux для этого? Приведите пример конфига.

VLAN (аббр. от англ. Virtual Local Area Network) — виртуальная локальная компьютерная сеть. Представляет собой группу хостов с общим набором требований, которые взаимодействуют так, как если бы они были подключены к широковещательному домену независимо от их физического местонахождения. VLAN имеет те же свойства, что и физическая локальная сеть, но позволяет конечным членам группироваться вместе, даже если они не находятся в одной физической сети. Такая реорганизация может быть сделана на основе программного обеспечения вместо физического перемещения устройств.

root@vagrant:/home/vagrant# apt install vlan  
```
auto vlan1400  
iface vlan1400 inet static  
        address 192.168.1.1  
        netmask 255.255.255.0  
        vlan_raw_device eth0  
```

4) Какие типы агрегации интерфейсов есть в Linux? Какие опции есть для балансировки нагрузки? Приведите пример конфига.

Основное применение технологии агрегации — объединение каналов в сетевых коммутаторах, но можно настроить агрегирование для компьютерных сетевых адаптеров. Например, в операционной системе Linux можно сконфигурировать агрегированный сетевой адаптер bond0 со стандартным драйвером ядра (англ. bonding driver) как объединяющий Ethernet-адаптеры eth0 и eth1, с назначением ему единого IP-адреса, и для системы и выполняемых на ней программ нет никакой разницы между таким адаптером и физическими (исключая немногие служебные утилиты, которые предназначены для операций непосредственно с адаптерами). При этом значения MAC-адреса bond0 будут чередоваться — периодически будет показываться то MAC-адрес первой сетевой карты eth0, то MAC-адрес адаптера eth1.

Типы агрегации (объединения) интерфейсов в Linux  
mode=0 (balance-rr)  
Этот режим используется по-умолчанию, если в настройках не указано другое. balance-rr обеспечивает балансировку нагрузки и отказоустойчивость. В данном режиме пакеты отправляются "по кругу" от первого интерфейса к последнему и сначала. Если выходит из строя один из интерфейсов, пакеты отправляются на остальные оставшиеся.При подключении портов к разным коммутаторам, требует их настройки.

mode=1 (active-backup)  
При active-backup один интерфейс работает в активном режиме, остальные в ожидающем. Если активный падает, управление передается одному из ожидающих. Не требует поддержки данной функциональности от коммутатора.

mode=2 (balance-xor)  
Передача пакетов распределяется между объединенными интерфейсами по формуле ((MAC-адрес источника) XOR (MAC-адрес получателя)) % число интерфейсов. Один и тот же интерфейс работает с определённым получателем. Режим даёт балансировку нагрузки и отказоустойчивость.

mode=3 (broadcast)  
Происходит передача во все объединенные интерфейсы, обеспечивая отказоустойчивость.

mode=4 (802.3ad)  
Это динамическое объединение портов. В данном режиме можно получить значительное увеличение пропускной способности как входящего так и исходящего трафика, используя все объединенные интерфейсы. Требует поддержки режима от коммутатора, а так же (иногда) дополнительную настройку коммутатора.

mode=5 (balance-tlb)  
Адаптивная балансировка нагрузки. При balance-tlb входящий трафик получается только активным интерфейсом, исходящий - распределяется в зависимости от текущей загрузки каждого интерфейса. Обеспечивается отказоустойчивость и распределение нагрузки исходящего трафика. Не требует специальной поддержки коммутатора.

mode=6 (balance-alb)  
Адаптивная балансировка нагрузки (более совершенная). Обеспечивает балансировку нагрузки как исходящего (TLB, transmit load balancing), так и входящего трафика (для IPv4 через ARP). Не требует специальной поддержки коммутатором, но требует возможности изменять MAC-адрес устройства.

```
auto bond0

iface bond0 inet static
    address 10.31.1.5
    netmask 255.255.255.0
    network 10.31.1.0
    gateway 10.31.1.254
    bond-slaves eth0 eth1
    bond-mode active-backup
    bond-miimon 100
    bond-downdelay 200
    bond-updelay 200
```

5) Сколько IP адресов в сети с маской /29 ? Сколько /29 подсетей можно получить из сети с маской /24. Приведите несколько примеров /29 подсетей внутри сети 10.10.10.0/24.

Сколько IP адресов в сети с маской /29 ?  
Hosts/Net: 6                     Class C, Private Internet  

Сколько /29 подсетей можно получить из сети с маской /24 ?  
root@vagrant:/home/vagrant# ipcalc 192.168.1.0/24 -b -n /29  
Subnets:   32  
Hosts:     192  

Приведите несколько примеров /29 подсетей внутри сети 10.10.10.0/24
![image](https://user-images.githubusercontent.com/93198418/154434850-a2524b65-e7c6-48a4-9737-6b0c79cb3d9f.png)

6) Задача: вас попросили организовать стык между 2-мя организациями. Диапазоны 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16 уже заняты. Из какой подсети допустимо взять частные IP адреса? Маску выберите из расчета максимум 40-50 хостов внутри подсети.

100.64.0.0/26
![image](https://user-images.githubusercontent.com/93198418/154436341-90f95095-a762-4c6f-952d-f4e9357aee28.png)  

7) Как проверить ARP таблицу в Linux, Windows? Как очистить ARP кеш полностью? Как из ARP таблицы удалить только один нужный IP?

Как проверить ARP таблицу в Linux, Windows?  
Linux  
![image](https://user-images.githubusercontent.com/93198418/154442129-cc2555a8-2131-4cdd-ae7f-d7ca031e4a41.png)  

Windows  
![image](https://user-images.githubusercontent.com/93198418/154449327-ebc01858-d9e3-40da-ad29-ff92a8c637fb.png)

Как очистить ARP кеш полностью?  
Linux  
ip neigh flush all  
Windows  
arp -d *  

Как из ARP таблицы удалить только один нужный IP?  
Linux  
ip neigh flush 10.0.2.3  
Windows  
arp -d 10.0.2.3
