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
  
8. Ознакомиться с разделами man bash, почитать о настройках самого bash:  
какой переменной можно задать длину журнала history, и на какой строчке manual это описывается?  
![image](https://user-images.githubusercontent.com/93198418/147567701-a8ccd2a8-6c7f-46dd-88f0-f30c09b73437.png)  
718 строка  
![image](https://user-images.githubusercontent.com/93198418/147567765-b0c61334-dbc2-4628-9857-6a4fb9977d32.png)
что делает директива ignoreboth в bash?  
![image](https://user-images.githubusercontent.com/93198418/147568472-fc378ce1-6ccf-431b-8102-149dc0193658.png)  
710 строка
![image](https://user-images.githubusercontent.com/93198418/147568540-d3b88a04-f326-435f-b2ac-efb45efdf769.png)  

9. В каких сценариях использования применимы скобки {} и на какой строчке man bash это описано?
![image](https://user-images.githubusercontent.com/93198418/147569822-aa1b8964-abc7-4bc5-a629-8f685b3b0f6f.png)  
926 строка  
![image](https://user-images.githubusercontent.com/93198418/147569900-00c9a861-196e-42d5-b0c9-20ac7aecacdd.png)
  
10. С учётом ответа на предыдущий вопрос, как создать однократным вызовом touch 100000 файлов? Получится ли аналогичным образом создать 300000? Если нет, то почему?
<code>
root@vagrant:/home/vagrant# touch {000001..100000}.txt
</code>  
<code>  
root@vagrant:/home/vagrant# touch {100001..400000}.txt
bash: /usr/bin/touch: Argument list too long
</code>  









