# devops-netology  
## Шевякин Кирилл  

### Домашнее задание к занятию "3.1. Работа в терминале, лекция 1"  
5) Ознакомьтесь с графическим интерфейсом VirtualBox, посмотрите как выглядит виртуальная машина, которую создал для вас Vagrant, какие аппаратные ресурсы ей выделены. Какие ресурсы выделены по-умолчанию?  
![image](https://user-images.githubusercontent.com/93198418/147564583-2ff8f574-319b-4e1a-b274-2cd0cbf6b366.png)  
  
6) Ознакомьтесь с возможностями конфигурации VirtualBox через Vagrantfile: документация. Как добавить оперативной памяти или ресурсов процессора виртуальной машине?  
Изменить в  Vagrantfile  
config.vm.provider "virtualbox" do |v|  
     v.memory = 1024  
     v.cpus = 2  
end  

7) Команда vagrant ssh из директории, в которой содержится Vagrantfile, позволит вам оказаться внутри виртуальной машины без каких-либо дополнительных настроек. Попрактикуйтесь в выполнении обсуждаемых команд в терминале Ubuntu.  
Сделано  

8) Ознакомиться с разделами man bash, почитать о настройках самого bash:  
какой переменной можно задать длину журнала history, и на какой строчке manual это описывается?  
![image](https://user-images.githubusercontent.com/93198418/147567701-a8ccd2a8-6c7f-46dd-88f0-f30c09b73437.png)  
718 строка  
![image](https://user-images.githubusercontent.com/93198418/147567765-b0c61334-dbc2-4628-9857-6a4fb9977d32.png)  
что делает директива ignoreboth в bash?  
![image](https://user-images.githubusercontent.com/93198418/147568472-fc378ce1-6ccf-431b-8102-149dc0193658.png)  
710 строка  
![image](https://user-images.githubusercontent.com/93198418/147568540-d3b88a04-f326-435f-b2ac-efb45efdf769.png)  

9) В каких сценариях использования применимы скобки {} и на какой строчке man bash это описано?
![image](https://user-images.githubusercontent.com/93198418/147569822-aa1b8964-abc7-4bc5-a629-8f685b3b0f6f.png)    
926 строка  
![image](https://user-images.githubusercontent.com/93198418/147569900-00c9a861-196e-42d5-b0c9-20ac7aecacdd.png)  
  
10) С учётом ответа на предыдущий вопрос, как создать однократным вызовом touch 100000 файлов? Получится ли аналогичным образом создать 300000? Если нет, то почему?  
root@vagrant:/home/vagrant# touch {000001..100000}.txt  
root@vagrant:/home/vagrant# touch {100001..400000}.txt  
bash: /usr/bin/touch: Argument list too long  
  
11) В man bash поищите по /\[\[. Что делает конструкция [[ -d /tmp ]]  
![image](https://user-images.githubusercontent.com/93198418/147572177-0e8ae5da-322b-41ed-8374-e90a0eb05660.png)  
Эта команда проверяет наличие каталога tmp в корне

12) Основываясь на знаниях о просмотре текущих (например, PATH) и установке новых переменных; командах, которые мы рассматривали, добейтесь в выводе type -a bash в виртуальной машине наличия первым пунктом в списке:  
bash is /tmp/new_path_directory/bash  
bash is /usr/local/bin/bash  
bash is /bin/bash  
(прочие строки могут отличаться содержимым и порядком) В качестве ответа приведите команды, которые позволили вам добиться указанного вывода или соответствующие скриншоты.   
root@vagrant:/home/vagrant# type -a bash  
bash is /usr/bin/bash  
bash is /bin/bash  
root@vagrant:/home/vagrant# mkdir /tmp/bash  
root@vagrant:/home/vagrant# cp /usr/bin/bash /tmp/bash  
root@vagrant:/home/vagrant# PATH=/tmp/bash/:$PATH  
root@vagrant:/home/vagrant# type -a bash  
bash is /tmp/bash/bash  
bash is /usr/bin/bash  
bash is /bin/bash  

13) Чем отличается планирование команд с помощью batch и at?  
Тогда как cron используется для назначения повторяющихся задач, команда at используется для назначения одноразового задания на заданное время, а команда batch — для назначения одноразовых задач, которые должны выполняться, когда загрузка системы становится меньше 0,8.
Чтобы использовать at или batch, необходимо, чтобы был установлен RPM-пакет at и запущена служба atd. Чтобы узнать, установлен ли этот пакет, выполните команду rpm -q at. Чтобы определить, работает ли служба, воспользуйтесь командой /sbin/service atd status.

14) Завершите работу виртуальной машины чтобы не расходовать ресурсы компьютера и/или батарею ноутбука.  
root@vagrant:/home/vagrant# shutdown -t 0  
PS C:\Virtual> vagrant suspend
