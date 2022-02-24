# devops-netology  
## Шевякин Кирилл  

### Домашнее задание к занятию "3.9. Элементы безопасности информационных систем"

1) Установите Bitwarden плагин для браузера. Зарегестрируйтесь и сохраните несколько паролей.

![image](https://user-images.githubusercontent.com/93198418/155091793-2de00e57-42ee-4a80-b21b-e5f293dc4850.png)

2) Установите Google authenticator на мобильный телефон. Настройте вход в Bitwarden акаунт через Google authenticator OTP.

У меня телефон Huawei, там, к сожалению, нет google autentification. Поэтому настроил двухфакторную аутентификацию через почту.

![image](https://user-images.githubusercontent.com/93198418/155515899-2a5f714f-87b9-493d-b510-f46accbbb43c.png)

3) Установите apache2, сгенерируйте самоподписанный сертификат, настройте тестовый сайт для работы по HTTPS.

Сделано  
![image](https://user-images.githubusercontent.com/93198418/155521036-4fa739ec-49d6-4099-ad0d-0d06b2657cf3.png)  

4) Проверьте на TLS уязвимости произвольный сайт в интернете (кроме сайтов МВД, ФСБ, МинОбр, НацБанк, РосКосмос, РосАтом, РосНАНО и любых госкомпаний, объектов КИИ, ВПК ... и тому подобное).

![image](https://user-images.githubusercontent.com/93198418/155521913-a85c5538-bad2-4e62-ac08-7fe381403428.png)

5) Установите на Ubuntu ssh сервер, сгенерируйте новый приватный ключ. Скопируйте свой публичный ключ на другой сервер. Подключитесь к серверу по SSH-ключу.

![image](https://user-images.githubusercontent.com/93198418/155525387-638bcff9-a766-4860-bcc6-6351c2cbf9a3.png)  

Ключ сгенерирован в Putty  

![image](https://user-images.githubusercontent.com/93198418/155525719-cea1cac8-1960-4a7d-8710-92a0ed6e8622.png)  

![image](https://user-images.githubusercontent.com/93198418/155526019-d1df9cc9-fab9-4bd4-b0ae-447ba0a06d90.png)

6) Переименуйте файлы ключей из задания 5. Настройте файл конфигурации SSH клиента, так чтобы вход на удаленный сервер осуществлялся по имени сервера.

![image](https://user-images.githubusercontent.com/93198418/155527614-a87ccc0c-999c-4754-851f-12137c26ddd1.png)  
![image](https://user-images.githubusercontent.com/93198418/155527852-8e63a2bf-d7a8-413b-a7c4-0083bc1be527.png)  
![image](https://user-images.githubusercontent.com/93198418/155527667-d273952f-d01d-4a5f-a1f6-d398828a5d5b.png)  

7) Соберите дамп трафика утилитой tcpdump в формате pcap, 100 пакетов. Откройте файл pcap в Wireshark.

![image](https://user-images.githubusercontent.com/93198418/155531122-3149057e-765d-483f-8b3a-35ce829271db.png)  
![image](https://user-images.githubusercontent.com/93198418/155531045-8219bd55-88ea-4abc-bec0-b3399f2ed2a4.png)

8*) Просканируйте хост scanme.nmap.org. Какие сервисы запущены?

9*) Установите и настройте фаервол ufw на web-сервер из задания 3. Откройте доступ снаружи только к портам 22,80,443

