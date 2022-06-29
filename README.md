# devops-netology  
## Шевякин Кирилл  

# Домашнее задание к занятию "7.2. Облачные провайдеры и синтаксис Terraform."

## Задача 1 (Вариант с Yandex.Cloud). Регистрация в ЯО и знакомство с основами (необязательно, но крайне желательно).

1. Подробная инструкция на русском языке содержится [здесь](https://cloud.yandex.ru/docs/solutions/infrastructure-management/terraform-quickstart).
2. Обратите внимание на период бесплатного использования после регистрации аккаунта. 
3. Используйте раздел "Подготовьте облако к работе" для регистрации аккаунта. Далее раздел "Настройте провайдер" для подготовки
базового терраформ конфига.
4. Воспользуйтесь [инструкцией](https://registry.terraform.io/providers/yandex-cloud/yandex/latest/docs) на сайте терраформа, что бы 
не указывать авторизационный токен в коде, а терраформ провайдер брал его из переменных окружений.

## Задача 2. Создание yandex_compute_instance через терраформ. 

1. В каталоге `terraform` вашего основного репозитория, который был создан в начале курса, создайте файл `main.tf` и `versions.tf`.
2. Зарегистрируйте провайдер 
   [yandex.cloud](https://registry.terraform.io/providers/yandex-cloud/yandex/latest/docs). Подробную инструкцию можно найти 
   [здесь](https://cloud.yandex.ru/docs/solutions/infrastructure-management/terraform-quickstart).
3. Внимание! В гит репозиторий нельзя пушить ваши личные ключи доступа к аккаунту. Поэтому в предыдущем задании мы указывали
их в виде переменных окружения.   
4. В файле `main.tf` создайте рессурс 
   [yandex_compute_image](https://registry.terraform.io/providers/yandex-cloud/yandex/latest/docs/resources/compute_image).
5. Если вы выполнили первый пункт, то добейтесь того, что бы команда `terraform plan` выполнялась без ошибок. 


В качестве результата задания предоставьте:
1. Ответ на вопрос: при помощи какого инструмента (из разобранных на прошлом занятии) можно создать свой образ ami?
1. Ссылку на репозиторий с исходной конфигурацией терраформа.  
 
### Ответ  

Ответ на вопрос: при помощи какого инструмента (из разобранных на прошлом занятии) можно создать свой образ ami?  
Packer  

Ссылку на репозиторий с исходной конфигурацией терраформа.  
Файл main.tf в этом репозитории  

Если вы выполнили первый пункт, то добейтесь того, что бы команда `terraform plan` выполнялась без ошибок.  
![image](https://user-images.githubusercontent.com/93198418/176438741-956436b6-af4b-4fab-9173-2cf0a793df1a.png)    
![image](https://user-images.githubusercontent.com/93198418/176438269-5abef94a-7155-4962-9e25-7777b2b4d8be.png)  
![image](https://user-images.githubusercontent.com/93198418/176438379-67cc344f-fbd1-46e5-9916-85e74447968f.png)  
![image](https://user-images.githubusercontent.com/93198418/176438519-5892c206-f8dc-4925-aac1-bd0e057e0ea0.png)  

Вот созданная машина  
![image](https://user-images.githubusercontent.com/93198418/176452574-79efaf46-f2d4-4c89-a7db-18a32b5c57b5.png)

Удалил все  
![image](https://user-images.githubusercontent.com/93198418/176453015-705ee630-3e42-40d7-b4e8-bd9def7bb0b9.png)  
![image](https://user-images.githubusercontent.com/93198418/176453937-92c188be-c972-413a-bf60-5a8083c81582.png)  
![image](https://user-images.githubusercontent.com/93198418/176454079-6b2dd995-8f0e-4bb6-b2b7-b5bc45b9fe49.png)  



