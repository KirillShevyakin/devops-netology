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


![image](https://user-images.githubusercontent.com/93198418/176438053-5519b0d5-ad19-432d-b9e6-c57461cb8b23.png)  
![image](https://user-images.githubusercontent.com/93198418/176438269-5abef94a-7155-4962-9e25-7777b2b4d8be.png)  
![image](https://user-images.githubusercontent.com/93198418/176438379-67cc344f-fbd1-46e5-9916-85e74447968f.png)  
![image](https://user-images.githubusercontent.com/93198418/176438519-5892c206-f8dc-4925-aac1-bd0e057e0ea0.png)  



