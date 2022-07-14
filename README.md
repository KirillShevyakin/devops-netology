# devops-netology  
## Шевякин Кирилл  

# Домашнее задание к занятию "7.6. Написание собственных провайдеров для Terraform."

Бывает, что 
* общедоступная документация по терраформ ресурсам не всегда достоверна,
* в документации не хватает каких-нибудь правил валидации или неточно описаны параметры,
* понадобиться использовать провайдер без официальной документации,
* может возникнуть необходимость написать свой провайдер для системы используемой в ваших проектах.   

## Задача
Давайте потренируемся читать исходный код AWS провайдера, который можно склонировать от сюда: 
[https://github.com/hashicorp/terraform-provider-aws.git](https://github.com/hashicorp/terraform-provider-aws.git).
Просто найдите нужные ресурсы в исходном коде и ответы на вопросы станут понятны.  


1. Найдите, где перечислены все доступные `resource` и `data_source`, приложите ссылку на эти строки в коде на 
гитхабе.   
1. Для создания очереди сообщений SQS используется ресурс `aws_sqs_queue` у которого есть параметр `name`. 
    * С каким другим параметром конфликтует `name`? Приложите строчку кода, в которой это указано.
    * Какая максимальная длина имени? 
    * Какому регулярному выражению должно подчиняться имя? 

### Ответ

1) Найдите, где перечислены все доступные `resource` и `data_source`, приложите ссылку на эти строки в коде на 
гитхабе.   

resource - https://github.com/hashicorp/terraform-provider-aws/blob/8e4d8a3f3f781b83f96217c2275f541c893fec5a/aws/provider.go#L411  
ResourcesMap: map[string]*schema.Resource{  
![image](https://user-images.githubusercontent.com/93198418/178953130-94eabc88-8144-4f4f-8b37-19ed88fedc05.png)  

data_source - https://github.com/hashicorp/terraform-provider-aws/blob/8e4d8a3f3f781b83f96217c2275f541c893fec5a/aws/provider.go#L169  
DataSourcesMap: map[string]*schema.Resource{  
![image](https://user-images.githubusercontent.com/93198418/178953477-4d20ea7d-600d-4468-9dfc-0ad17b953a89.png)  

2) Для создания очереди сообщений SQS используется ресурс `aws_sqs_queue` у которого есть параметр `name`.  

С каким другим параметром конфликтует `name`? Приложите строчку кода, в которой это указано.  
'name' конфликтует с 'name_prefix'  
ConflictsWith: []string{"name_prefix"},  
![image](https://user-images.githubusercontent.com/93198418/178954510-38087ac7-1263-4885-8bfa-3a3eed06cbee.png)  

Какая максимальная длина имени?  
Длина имени не может быть больше 80 символов  
errors = append(errors, fmt.Errorf("%q cannot be longer than 80 characters", k))  
![image](https://user-images.githubusercontent.com/93198418/178955256-5125fd73-6f51-47b9-9095-921c0d4dd5d0.png)  

Какому регулярному выражению должно подчиняться имя?  
Латинские большие-маленькие буквы , цифры, знак подчеркивания + .fifo в конце  
if !regexp.MustCompile(`^[0-9A-Za-z-_]+(\.fifo)?$`).MatchString(value) {  
![image](https://user-images.githubusercontent.com/93198418/178957153-719b5f24-6651-4529-ad30-e6082e696bae.png)  



