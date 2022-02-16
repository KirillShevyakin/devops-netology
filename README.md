# devops-netology  
## Шевякин Кирилл  

### Домашнее задание к занятию "3.6. Компьютерные сети, лекция 1"
  
1) Работа c HTTP через телнет.  
Подключитесь утилитой телнет к сайту stackoverflow.com telnet stackoverflow.com 80  
```
отправьте HTTP запрос  
GET /questions HTTP/1.0  
HOST: stackoverflow.com  
[press enter]  
[press enter]  
```
В ответе укажите полученный HTTP код, что он означает?

![image](https://user-images.githubusercontent.com/93198418/154200574-59bbc26a-b0a0-407b-8491-bf47cd9ecdd5.png)

Метод «GET» просит сервер отправить копию объекта клиенту. В ответ мы получаем в html копию страницы stackoverflow.com/questions

2) Повторите задание 1 в браузере, используя консоль разработчика F12.  
откройте вкладку Network  
отправьте запрос http://stackoverflow.com  
найдите первый ответ HTTP сервера, откройте вкладку Headers  
укажите в ответе полученный HTTP код.  
проверьте время загрузки страницы, какой запрос обрабатывался дольше всего?  
приложите скриншот консоли браузера в ответ.  

![image](https://user-images.githubusercontent.com/93198418/154204075-ea853a0c-a4d1-4869-b2e7-c94dab723488.png)  

Дольше всего выполнялся запрос  
![image](https://user-images.githubusercontent.com/93198418/154204325-e47b1083-6343-4e12-89e0-c1862e17bbcc.png)  

3) Какой IP адрес у вас в интернете?  

![image](https://user-images.githubusercontent.com/93198418/154205467-790a7e1a-16d7-4f6f-a2da-24d04869e170.png)

4) Какому провайдеру принадлежит ваш IP адрес? Какой автономной системе AS? Воспользуйтесь утилитой whois

![image](https://user-images.githubusercontent.com/93198418/154205997-0d6bba3b-0b2e-4c3d-9e65-decc2005cf45.png)

5) Через какие сети проходит пакет, отправленный с вашего компьютера на адрес 8.8.8.8? Через какие AS? Воспользуйтесь утилитой traceroute

![image](https://user-images.githubusercontent.com/93198418/154206509-61adba80-55f5-4222-bd3c-aae1b34f14d4.png)

6) Повторите задание 5 в утилите mtr. На каком участке наибольшая задержка - delay?

![image](https://user-images.githubusercontent.com/93198418/154210526-24ab1d22-ad62-439c-bc2b-e0b948e894a3.png) 

![image](https://user-images.githubusercontent.com/93198418/154210620-8ce61474-f6d8-44de-b788-affd554106ed.png)

7) Какие DNS сервера отвечают за доменное имя dns.google? Какие A записи? воспользуйтесь утилитой dig

![image](https://user-images.githubusercontent.com/93198418/154211136-d6f09a48-7c45-47ad-a231-2cd69a1058b2.png)  
![image](https://user-images.githubusercontent.com/93198418/154211185-8ad8e77e-b39c-42f8-b5a1-67cbc9bd8ed4.png)  

8) Проверьте PTR записи для IP адресов из задания 7. Какое доменное имя привязано к IP? воспользуйтесь утилитой dig

![image](https://user-images.githubusercontent.com/93198418/154211495-8f36c9fb-8f36-4ca0-96dd-c2394522b76f.png)  
![image](https://user-images.githubusercontent.com/93198418/154211587-271881e3-021a-4efa-b8db-aa464cdcd0d2.png)
