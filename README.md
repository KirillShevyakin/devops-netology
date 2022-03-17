# devops-netology  
## Шевякин Кирилл  

# Домашнее задание к занятию "4.2. Использование Python для решения типовых DevOps задач"

## Обязательная задача 1

Есть скрипт:
```python
#!/usr/bin/env python3
a = 1
b = '2'
c = a + b
```

### Вопросы:
| Вопрос  | Ответ |
| ------------- | ------------- |
| Какое значение будет присвоено переменной `c`?  | TypeError: unsupported operand type(s) for +: 'int' and 'str'  |
| Как получить для переменной `c` значение 12?  | a = '1' или c=str(a)+b |
| Как получить для переменной `c` значение 3?  | b = 2 или c=a+int(b) |

## Обязательная задача 2
Мы устроились на работу в компанию, где раньше уже был DevOps Engineer. Он написал скрипт, позволяющий узнать, какие файлы модифицированы в репозитории, относительно локальных изменений. Этим скриптом недовольно начальство, потому что в его выводе есть не все изменённые файлы, а также непонятен полный путь к директории, где они находятся. Как можно доработать скрипт ниже, чтобы он исполнял требования вашего руководителя?

```python
#!/usr/bin/env python3

import os

bash_command = ["cd ~/netology/sysadm-homeworks", "git status"]
result_os = os.popen(' && '.join(bash_command)).read()
is_change = False
for result in result_os.split('\n'):
    if result.find('modified') != -1:
        prepare_result = result.replace('\tmodified:   ', '')
        print(prepare_result)
        break
```

### Решение:  
1) убрал переменную is_change  
2) добавил переменную с путем до директории git, чтобы видно было полный путь до файла  
3) убрал break, чтобы выводить все файлы  
### Ваш скрипт:
```python
#!/usr/bin/env python3

import os

git_path = '/home/vagrant/devops-netology/'
bash_command = ["cd "+git_path, "git status"]
result_os = os.popen(' && '.join(bash_command)).read()
for result in result_os.split('\n'):
        if result.find('modified') != -1:
                prepare_result = result.replace('\tmodified:   ', '')
                print(git_path,end="")
                print(prepare_result)

```

### Вывод скрипта при запуске при тестировании:
```
vagrant@vagrant:~$ ./dz.py
/home/vagrant/devops-netology/test/test1.txt
/home/vagrant/devops-netology/test_dz.txt
```

## Обязательная задача 3
1. Доработать скрипт выше так, чтобы он мог проверять не только локальный репозиторий в текущей директории, а также умел воспринимать путь к репозиторию, который мы передаём как входной параметр. Мы точно знаем, что начальство коварное и будет проверять работу этого скрипта в директориях, которые не являются локальными репозиториями.

### Решение:  
Доработка своего скрипта  
1) добавил модуль sys  
2) добавил условие для введенных аргументов  
   если есть аргумент и он правильный, то значение переменной git_path устанавливается на введеный аргумент при запуске  
   если есть аргумент и он неправильный, то выводится сообщение об неверно введенном аргументе  
   если нет аргумента, то значение переменной git_path устанавливается на локальный репозиторий, который был до этого  
### Ваш скрипт:
```python
#!/usr/bin/env python3

import os, sys

if len(sys.argv) > 1:
        git_path = sys.argv[1]
        bash_command = ["cd "+git_path, "git status 2>&1"]
        result_os = os.popen(' && '.join(bash_command)).read()
        if result_os.find('fatal') == -1:
                for result in result_os.split('\n'):
                        if result.find('modified') != -1:
                                prepare_result = result.replace('\tmodified:   ', '')
                                print(git_path,end="")
                                print(prepare_result)
        else:
                print(git_path," не является репозиторием git")
else:
        git_path = '/home/vagrant/devops-netology/'
        bash_command = ["cd "+git_path, "git status"]
        result_os = os.popen(' && '.join(bash_command)).read()
        for result in result_os.split('\n'):
                if result.find('modified') != -1:
                        prepare_result = result.replace('\tmodified:   ', '')
                        print(git_path,end="")
                        print(prepare_result)

```

### Вывод скрипта при запуске при тестировании:
```
vagrant@vagrant:~$ ./dz.py
/home/vagrant/devops-netology/test/test1.txt
/home/vagrant/devops-netology/test_dz.txt
vagrant@vagrant:~$ ./dz.py /home/vagrant/
/home/vagrant/  не является репозиторием git
vagrant@vagrant:~$ ./dz.py /home/vagrant/devops-netology/
/home/vagrant/devops-netology/test/test1.txt
/home/vagrant/devops-netology/test_dz.txt
```

## Обязательная задача 4
1. Наша команда разрабатывает несколько веб-сервисов, доступных по http. Мы точно знаем, что на их стенде нет никакой балансировки, кластеризации, за DNS прячется конкретный IP сервера, где установлен сервис. Проблема в том, что отдел, занимающийся нашей инфраструктурой очень часто меняет нам сервера, поэтому IP меняются примерно раз в неделю, при этом сервисы сохраняют за собой DNS имена. Это бы совсем никого не беспокоило, если бы несколько раз сервера не уезжали в такой сегмент сети нашей компании, который недоступен для разработчиков. Мы хотим написать скрипт, который опрашивает веб-сервисы, получает их IP, выводит информацию в стандартный вывод в виде: <URL сервиса> - <его IP>. Также, должна быть реализована возможность проверки текущего IP сервиса c его IP из предыдущей проверки. Если проверка будет провалена - оповестить об этом в стандартный вывод сообщением: [ERROR] <URL сервиса> IP mismatch: <старый IP> <Новый IP>. Будем считать, что наша разработка реализовала сервисы: `drive.google.com`, `mail.google.com`, `google.com`.

### Ваш скрипт:
```python
#!/usr/bin/env python3

import socket, time, datetime

srv = { 'drive.google.com':'0.0.0.0', 'mail.google.com':'0.0.0.0', 'google.com':'0.0.0.0' }
while 1==1:
        for host, ip  in srv.items():
                host_ip = socket.gethostbyname(host)
                if ip != host_ip:
                        srv[host] = host_ip
                        print("[ERROR] ",host," IP mismatch: ", ip, host_ip)
                else:
                        print(str(datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")),ip)
        time.sleep(5)
done
```

### Вывод скрипта при запуске при тестировании:
```
vagrant@vagrant:~$ ./dz4.py
[ERROR]  drive.google.com  IP mismatch:  0.0.0.0 173.194.222.194
[ERROR]  mail.google.com  IP mismatch:  0.0.0.0 142.251.1.17
[ERROR]  google.com  IP mismatch:  0.0.0.0 64.233.162.100
2022-03-17 13:51:03 173.194.222.194
2022-03-17 13:51:03 142.251.1.17
2022-03-17 13:51:03 64.233.162.100
2022-03-17 13:51:08 173.194.222.194
2022-03-17 13:51:08 142.251.1.17
2022-03-17 13:51:08 64.233.162.100
2022-03-17 13:51:13 173.194.222.194
2022-03-17 13:51:13 142.251.1.17
2022-03-17 13:51:13 64.233.162.100
2022-03-17 13:51:18 173.194.222.194
2022-03-17 13:51:18 142.251.1.17
[ERROR]  google.com  IP mismatch:  64.233.162.100 64.233.162.102
2022-03-17 13:51:23 173.194.222.194
2022-03-17 13:51:23 142.251.1.17
[ERROR]  google.com  IP mismatch:  64.233.162.102 64.233.162.139
2022-03-17 13:51:28 173.194.222.194
2022-03-17 13:51:28 142.251.1.17
2022-03-17 13:51:28 64.233.162.139
2022-03-17 13:51:33 173.194.222.194
2022-03-17 13:51:33 142.251.1.17
2022-03-17 13:51:33 64.233.162.139

```

