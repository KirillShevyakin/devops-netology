# devops-netology  
## Шевякин Кирилл  

### Домашнее задание к занятию "3.1. Работа в терминале, лекция 1"  
5. Ознакомьтесь с графическим интерфейсом VirtualBox, посмотрите как выглядит виртуальная машина, которую создал для вас Vagrant, какие аппаратные ресурсы ей выделены. Какие ресурсы выделены по-умолчанию?  
![image](https://user-images.githubusercontent.com/93198418/147564583-2ff8f574-319b-4e1a-b274-2cd0cbf6b366.png)  
  
6. Ознакомьтесь с возможностями конфигурации VirtualBox через Vagrantfile: документация. Как добавить оперативной памяти или ресурсов процессора виртуальной машине?  
Изменить в  Vagrantfile  
config.vm.provider "virtualbox" do |v|  
     v.memory = 1024  
     v.cpus = 2  
end  
  
7. Ознакомиться с разделами man bash, почитать о настройках самого bash:  
какой переменной можно задать длину журнала history, и на какой строчке manual это описывается?  
![image](https://user-images.githubusercontent.com/93198418/147567701-a8ccd2a8-6c7f-46dd-88f0-f30c09b73437.png)  
718 строка  
![image](https://user-images.githubusercontent.com/93198418/147567765-b0c61334-dbc2-4628-9857-6a4fb9977d32.png)








