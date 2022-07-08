# devops-netology  
## Шевякин Кирилл  

# Домашнее задание к занятию "7.4. Средства командной работы над инфраструктурой."

## Задача 1. Настроить terraform cloud (необязательно, но крайне желательно).

В это задании предлагается познакомиться со средством командой работы над инфраструктурой предоставляемым
разработчиками терраформа. 

1. Зарегистрируйтесь на [https://app.terraform.io/](https://app.terraform.io/).
(регистрация бесплатная и не требует использования платежных инструментов).
1. Создайте в своем github аккаунте (или другом хранилище репозиториев) отдельный репозиторий с
 конфигурационными файлами прошлых занятий (или воспользуйтесь любым простым конфигом).
1. Зарегистрируйте этот репозиторий в [https://app.terraform.io/](https://app.terraform.io/).
1. Выполните plan и apply. 

В качестве результата задания приложите снимок экрана с успешным применением конфигурации.

### Ответ  

В cloud зарегистрировался
![image](https://user-images.githubusercontent.com/93198418/177744947-f92d6175-0de0-4e28-b878-3b83ab1231c3.png)  
![image](https://user-images.githubusercontent.com/93198418/177745171-2df5b5f7-de2b-44e1-9b5b-7febbee9530b.png)  

При выполнении скрипта - ошибка 403  
![image](https://user-images.githubusercontent.com/93198418/177745398-4e2c76a0-8f1f-4c80-90a6-2787c4a75169.png)

## Задача 2. Написать серверный конфиг для атлантиса. 

Смысл задания – познакомиться с документацией 
о [серверной](https://www.runatlantis.io/docs/server-side-repo-config.html) конфигурации и конфигурации уровня 
 [репозитория](https://www.runatlantis.io/docs/repo-level-atlantis-yaml.html).

Создай `server.yaml` который скажет атлантису:
1. Укажите, что атлантис должен работать только для репозиториев в вашем github (или любом другом) аккаунте.  
![image](https://user-images.githubusercontent.com/93198418/177938068-a58b356e-7138-46a9-bd65-2ba5a5778cc1.png)  

1. На стороне клиентского конфига разрешите изменять `workflow`, то есть для каждого репозитория можно 
будет указать свои дополнительные команды.  
![image](https://user-images.githubusercontent.com/93198418/177938217-fec58b71-61aa-4235-a7ec-8ede96312680.png)  

1. В `workflow` используемом по-умолчанию сделайте так, что бы во время планирования не происходил `lock` состояния.
![image](https://user-images.githubusercontent.com/93198418/177938480-8d4484af-e7ac-4f13-8bc9-f69335235673.png)  

Создай `atlantis.yaml` который, если поместить в корень terraform проекта, скажет атлантису:
1. Надо запускать планирование и аплай для двух воркспейсов `stage` и `prod`.
1. Необходимо включить автопланирование при изменении любых файлов `*.tf`.  
![image](https://user-images.githubusercontent.com/93198418/177942073-fd2b926f-ccd5-4ba9-8847-21a72a19a6ca.png)  

В качестве результата приложите ссылку на файлы `server.yaml` и `atlantis.yaml`.  
https://github.com/KirillShevyakin/devops-netology.git  

## Задача 3. Знакомство с каталогом модулей. 

1. В [каталоге модулей](https://registry.terraform.io/browse/modules) найдите официальный модуль от aws для создания
`ec2` инстансов. 
2. Изучите как устроен модуль. Задумайтесь, будете ли в своем проекте использовать этот модуль или непосредственно 
ресурс `aws_instance` без помощи модуля?
3. В рамках предпоследнего задания был создан ec2 при помощи ресурса `aws_instance`. 
Создайте аналогичный инстанс при помощи найденного модуля.   

В качестве результата задания приложите ссылку на созданный блок конфигураций.   

### Ответ  

![image](https://user-images.githubusercontent.com/93198418/177944734-b9878709-ed21-40e2-9a4f-35398aa888d9.png)  

Задумайтесь, будете ли в своем проекте использовать этот модуль или непосредственно 
ресурс `aws_instance` без помощи модуля?  
Мне кажется, использование модулей сильно облегчает работу. Я буду использовать модули в работе.  



