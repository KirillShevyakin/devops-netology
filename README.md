# devops-netology  
## Шевякин Кирилл  

### Домашнее задание к занятию "3.8. Компьютерные сети, лекция 3"

1) Подключитесь к публичному маршрутизатору в интернет. Найдите маршрут к вашему публичному IP  

```  
telnet route-views.routeviews.org  
Username: rviews  
show ip route x.x.x.x/32  
show bgp x.x.x.x/32  
```

![image](https://user-images.githubusercontent.com/93198418/154643704-a9a04ad2-4e92-415a-938f-bee7983373f5.png)  
![image](https://user-images.githubusercontent.com/93198418/154644366-2f2fae3b-af1e-4b97-a951-dece1fac64ca.png)  

2) Создайте dummy0 интерфейс в Ubuntu. Добавьте несколько статических маршрутов. Проверьте таблицу маршрутизации.


