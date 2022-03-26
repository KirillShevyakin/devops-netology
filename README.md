# devops-netology  
## Шевякин Кирилл  

# Домашнее задание к занятию "4.3. Языки разметки JSON и YAML"


## Обязательная задача 1
Мы выгрузили JSON, который получили через API запрос к нашему сервису:
```
    { "info" : "Sample JSON output from our service\t",
        "elements" :[
            { "name" : "first",
            "type" : "server",
            "ip" : 7175 
            }
            { "name" : "second",
            "type" : "proxy",
            "ip : 71.78.22.43
            }
        ]
    }
```
  Нужно найти и исправить все ошибки, которые допускает наш сервис
  
Решение:
1) Поменял форматирование (пробелы, отступы, новые строки)  
2) Добавил / для экранирования \t в 2-ой строке  
3) Добавил "" и . в 8-ой строке для ip (ip - это 4 разряда от 0 до 255 и должно быть строкой)  
4) Добавил , в 9-ой строке (окончание key-value)  
5) Добавил " к "ip и "" к key-value в 13-ой строке  
```  
    { 
      "info" : "Sample JSON output from our service/\t",
      "elements":
      [
        { 
          "name" : "first",
          "type" : "server",
          "ip" : "7.1.7.5" 
        },
        { 
          "name" : "second",
          "type" : "proxy",
          "ip" : "71.78.22.43"
        }
      ]
    }
```  

## Обязательная задача 2
В прошлый рабочий день мы создавали скрипт, позволяющий опрашивать веб-сервисы и получать их IP. К уже реализованному функционалу нам нужно добавить возможность записи JSON и YAML файлов, описывающих наши сервисы. Формат записи JSON по одному сервису: `{ "имя сервиса" : "его IP"}`. Формат записи YAML по одному сервису: `- имя сервиса: его IP`. Если в момент исполнения скрипта меняется IP у сервиса - он должен так же поменяться в yml и json файле.

### Ваш скрипт:
```python
#!/usr/bin/env python3

import socket, time
import json, yaml

srv = { 'drive.google.com':'0.0.0.0', 'mail.google.com':'0.0.0.0', 'google.com':'0.0.0.0' }
json_data = {}
yaml_data = {}
while True:
        for host, ip  in srv.items():
                host_ip = socket.gethostbyname(host)
                if ip != host_ip:
                        srv[host] = host_ip
                        json_data.update({host:ip})
                        yaml_data.update({"- "+host:ip})
                        print(json_data)
                        print(yaml_data)
                else:
                        json_data.update({host:ip})
                        yaml_data.update({"- "+host:ip})
                        print("json ",json_data)
                        print("yaml ",yaml_data)
        time.sleep(5)
with open("hosts.json", 'w') as json_file:
        json.dump(json_data, json_file)
with open("hosts.yaml",'w') as yaml_file:
        yaml.dump(yaml_data, yaml_file)
```

### Вывод скрипта при запуске при тестировании:
```
vagrant@vagrant:~$ ./dz4.py
{'drive.google.com': '0.0.0.0'}
{'- drive.google.com': '0.0.0.0'}
{'drive.google.com': '0.0.0.0', 'mail.google.com': '0.0.0.0'}
{'- drive.google.com': '0.0.0.0', '- mail.google.com': '0.0.0.0'}
{'drive.google.com': '0.0.0.0', 'mail.google.com': '0.0.0.0', 'google.com': '0.0.0.0'}
{'- drive.google.com': '0.0.0.0', '- mail.google.com': '0.0.0.0', '- google.com': '0.0.0.0'}
json  {'drive.google.com': '108.177.14.194', 'mail.google.com': '0.0.0.0', 'google.com': '0.0.0.0'}
yaml  {'- drive.google.com': '108.177.14.194', '- mail.google.com': '0.0.0.0', '- google.com': '0.0.0.0'}
json  {'drive.google.com': '108.177.14.194', 'mail.google.com': '74.125.131.83', 'google.com': '0.0.0.0'}
yaml  {'- drive.google.com': '108.177.14.194', '- mail.google.com': '74.125.131.83', '- google.com': '0.0.0.0'}
json  {'drive.google.com': '108.177.14.194', 'mail.google.com': '74.125.131.83', 'google.com': '173.194.222.100'}
yaml  {'- drive.google.com': '108.177.14.194', '- mail.google.com': '74.125.131.83', '- google.com': '173.194.222.100'}
json  {'drive.google.com': '108.177.14.194', 'mail.google.com': '74.125.131.83', 'google.com': '173.194.222.100'}
yaml  {'- drive.google.com': '108.177.14.194', '- mail.google.com': '74.125.131.83', '- google.com': '173.194.222.100'}
json  {'drive.google.com': '108.177.14.194', 'mail.google.com': '74.125.131.83', 'google.com': '173.194.222.100'}
yaml  {'- drive.google.com': '108.177.14.194', '- mail.google.com': '74.125.131.83', '- google.com': '173.194.222.100'}
json  {'drive.google.com': '108.177.14.194', 'mail.google.com': '74.125.131.83', 'google.com': '173.194.222.100'}
yaml  {'- drive.google.com': '108.177.14.194', '- mail.google.com': '74.125.131.83', '- google.com': '173.194.222.100'}
^CTraceback (most recent call last):
  File "./dz4.py", line 23, in <module>
    time.sleep(5)
KeyboardInterrupt
```

### json-файл(ы), который(е) записал ваш скрипт:
```json
vagrant@vagrant:~$ cat hosts.json
{"drive.google.com": "108.177.14.194", "mail.google.com": "74.125.131.18", "google.com": "173.194.222.113"}
```

### yml-файл(ы), который(е) записал ваш скрипт:
```yaml
vagrant@vagrant:~$ cat hosts.yaml
'- drive.google.com': 108.177.14.194
'- google.com': 173.194.222.113
'- mail.google.com': 74.125.131.18
```
