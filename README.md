# devops-netology  
## Шевякин Кирилл  

### Домашнее задание к занятию "3.5. Файловые системы"
  
1) Узнайте о sparse (разряженных) файлах.  

![image](https://user-images.githubusercontent.com/93198418/151925249-1a25a88b-bb33-410b-8c94-a4e8db44d7b3.png)  

2) Могут ли файлы, являющиеся жесткой ссылкой на один объект, иметь разные права доступа и владельца? Почему?  

![image](https://user-images.githubusercontent.com/93198418/151926482-8b426d23-8551-4597-ae2b-8b5cf5c6c60e.png)  
Файлы, являющиеся жесткой ссылкой на один объект, не могут иметь разные права доступа и владельца, потому что они ссылаются на один и тот же объект файловой системы - один и тот же device и inode.  

3) Сделайте vagrant destroy на имеющийся инстанс Ubuntu. Замените содержимое Vagrantfile следующим:

```
Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-20.04"
  config.vm.provider :virtualbox do |vb|
    lvm_experiments_disk0_path = "/tmp/lvm_experiments_disk0.vmdk"
    lvm_experiments_disk1_path = "/tmp/lvm_experiments_disk1.vmdk"
    vb.customize ['createmedium', '--filename', lvm_experiments_disk0_path, '--size', 2560]
    vb.customize ['createmedium', '--filename', lvm_experiments_disk1_path, '--size', 2560]
    vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', lvm_experiments_disk0_path]
    vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', lvm_experiments_disk1_path]
  end
end
```  
Данная конфигурация создаст новую виртуальную машину с двумя дополнительными неразмеченными дисками по 2.5 Гб.  

![image](https://user-images.githubusercontent.com/93198418/151956362-8ebb643f-d130-461e-a386-e019be24a591.png)  

4) Используя fdisk, разбейте первый диск на 2 раздела: 2 Гб, оставшееся пространство.  

![image](https://user-images.githubusercontent.com/93198418/151962007-5d950874-763f-454b-97d8-11d158230dec.png)  

5) Используя sfdisk, перенесите данную таблицу разделов на второй диск.  

![image](https://user-images.githubusercontent.com/93198418/151963973-ef3aa576-67a2-4e5a-89ac-c6fefcd1e335.png)  

6) Соберите mdadm RAID1 на паре разделов 2 Гб.

![image](https://user-images.githubusercontent.com/93198418/151971875-cf0fc4c4-81c2-4953-aeab-f957291d0a77.png)  

7) Соберите mdadm RAID0 на второй паре маленьких разделов.

![image](https://user-images.githubusercontent.com/93198418/151974420-a89af1bb-9b34-4ecd-9e3f-dcd7496561b3.png)  

8) Создайте 2 независимых PV на получившихся md-устройствах.

![image](https://user-images.githubusercontent.com/93198418/151976247-e056f89c-04e7-483c-ab23-cf5399d7bbb1.png)  

9) Создайте общую volume-group на этих двух PV.  

![image](https://user-images.githubusercontent.com/93198418/151976793-23c4127e-6f20-4b39-836c-1569bb4e2244.png)  

10) Создайте LV размером 100 Мб, указав его расположение на PV с RAID0.

![image](https://user-images.githubusercontent.com/93198418/151979884-479362a8-7f6b-49b2-bf0e-8851040ef3a9.png)  

11) Создайте mkfs.ext4 ФС на получившемся LV.

![image](https://user-images.githubusercontent.com/93198418/151980759-24fec6a2-20c9-4c6a-8370-f71969141f81.png)  

12) Смонтируйте этот раздел в любую директорию, например, /tmp/new.

![image](https://user-images.githubusercontent.com/93198418/151981209-45329032-9bdb-4bf2-a1b7-021e28562a40.png)  

13) Поместите туда тестовый файл, например wget https://mirror.yandex.ru/ubuntu/ls-lR.gz -O /tmp/new/test.gz.

![image](https://user-images.githubusercontent.com/93198418/151981681-1ab56753-4dc4-456a-af13-1a699e73258d.png)

14) Прикрепите вывод lsblk.

![image](https://user-images.githubusercontent.com/93198418/151981835-5df1e806-3e89-4bf5-9f6e-e45c7c43b045.png)  

15) Протестируйте целостность файла:  
```
root@vagrant:~# gzip -t /tmp/new/test.gz  
root@vagrant:~# echo $?  
0  
```

![image](https://user-images.githubusercontent.com/93198418/152101294-1936d581-036a-42c0-8298-0193ce991f98.png)  

16) Используя pvmove, переместите содержимое PV с RAID0 на RAID1.





