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




