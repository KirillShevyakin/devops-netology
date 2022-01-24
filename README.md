# devops-netology  
## Шевякин Кирилл  

### Домашнее задание к занятию "3.4. Операционные системы, лекция 2"
  
1) На лекции мы познакомились с node_exporter. В демонстрации его исполняемый файл запускался в background. Этого достаточно для демо, но не для настоящей production-системы, где процессы должны находиться под внешним управлением. Используя знания из лекции по systemd, создайте самостоятельно простой unit-файл для node_exporter:

поместите его в автозагрузку,
предусмотрите возможность добавления опций к запускаемому процессу через внешний файл (посмотрите, например, на systemctl cat cron),
удостоверьтесь, что с помощью systemctl процесс корректно стартует, завершается, а после перезагрузки автоматически поднимается.

![image](https://user-images.githubusercontent.com/93198418/150731305-096be1fd-d895-4cbe-966c-de3230c22f60.png)  
![image](https://user-images.githubusercontent.com/93198418/150731433-c0b51763-a46f-40ec-96c0-0cec85dd1ca1.png)  
![image](https://user-images.githubusercontent.com/93198418/150731558-0e5d8541-e06d-4405-a0d1-ed1f70022cf6.png)  
![image](https://user-images.githubusercontent.com/93198418/150731635-25bd9bb7-dc59-46ac-aec0-c10fd80de034.png)  
![image](https://user-images.githubusercontent.com/93198418/150731722-19031a91-ca8b-47ca-ae2f-cc2c63cbefaf.png)  

