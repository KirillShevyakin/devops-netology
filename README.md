# devops-netology  
## Шевякин Кирилл  

# Домашнее задание к занятию "4.1. Командная оболочка Bash: Практические навыки"

## Обязательная задача 1

Есть скрипт:
```bash
a=1
b=2
c=a+b
d=$a+$b
e=$(($a+$b))
```

Какие значения переменным c,d,e будут присвоены? Почему?

| Переменная  | Значение | Обоснование |
| ------------- | ------------- | ------------- |
| `c`  | a+b  | присвоение строки a+b |
| `d`  | 1+2  | присвоение строки со значениями переменных a и b |
| `e`  | 3    | присвоение переменной значения результата арифметической операции |
![image](https://user-images.githubusercontent.com/93198418/157433187-61430b64-011f-40e0-8ea5-f474452daddc.png)  


## Обязательная задача 2
На нашем локальном сервере упал сервис и мы написали скрипт, который постоянно проверяет его доступность, записывая дату проверок до тех пор, пока сервис не станет доступным (после чего скрипт должен завершиться). В скрипте допущена ошибка, из-за которой выполнение не может завершиться, при этом место на Жёстком Диске постоянно уменьшается. Что необходимо сделать, чтобы его исправить:
```bash
while ((1==1)
do
	curl https://localhost:4757
	if (($? != 0))
	then
		date >> curl.log
	fi
done
```

### Ваш скрипт:
1) вариант
```bash
while ((1==1))
do
	curl https://localhost:4757
	if (($? != 0))
	then
		date >> curl.log
	else
		break
	fi
done
```  
2) вариант
```bash
a=1
while ((a==1))
do
	curl https://localhost:4757
	if (($? != 0))
	then
		date >> curl.log
	else
		a=0
	fi
done
```  
P.S: в заданном скрипте забыли скобку "while ((1==1)"  

## Обязательная задача 3
Необходимо написать скрипт, который проверяет доступность трёх IP: `192.168.0.1`, `173.194.222.113`, `87.250.250.242` по `80` порту и записывает результат в файл `log`. Проверять доступность необходимо пять раз для каждого узла.

### Ваш скрипт:
```bash
#!/bin/bash
echo -n "" > log
hosts=(192.168.0.1 173.194.222.113 87.250.250.242)
for h in ${hosts[@]}
do
        for i in {1..5}
        do
                curl -s $h:80 > /dev/null
                dostup=$?
                if (( $dostup == 0 ))
                then
                        echo "хост $h доступен" >> log
                else
                        echo "хост $h недоступен" >> log
                fi
        done
done
```

## Обязательная задача 4
Необходимо дописать скрипт из предыдущего задания так, чтобы он выполнялся до тех пор, пока один из узлов не окажется недоступным. Если любой из узлов недоступен - IP этого узла пишется в файл error, скрипт прерывается.

### Ваш скрипт:
```bash
#!/bin/bash
echo -n "" > log
echo -n "" > error
hosts=(192.168.0.1 173.194.222.113 87.250.250.242)
for h in ${hosts[@]}
do
        for i in {1..5}
        do
                curl -s $h:80 > /dev/null
                dostup=$?
                if (( $dostup == 0 ))
                then
                        echo "хост $h доступен" >> log
                else
                        echo "хост $h недоступен" >> error
                        exit 0
                fi
        done
done
```

## Дополнительное задание (со звездочкой*) - необязательно к выполнению

Мы хотим, чтобы у нас были красивые сообщения для коммитов в репозиторий. Для этого нужно написать локальный хук для git, который будет проверять, что сообщение в коммите содержит код текущего задания в квадратных скобках и количество символов в сообщении не превышает 30. Пример сообщения: \[04-script-01-bash\] сломал хук.

### Ваш скрипт:
```bash
#!/bin/bash
commitRegex='^(\[[a-zA-Z0-9\-]\]*)'
if ((expr length $commitRegex < 30))
then
        if ((! grep -qE "$commitRegex" "$1"))
        then
                echo "Aborting according commit message policy. Please specify issue [XXXX] and less 30 symbols"
                exit 1
        fi
else
        echo "Aborting according commit message policy. Please specify issue [XXXX] and less 30 symbols"
        exit 1
fi
```
