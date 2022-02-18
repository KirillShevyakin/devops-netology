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

![image](https://user-images.githubusercontent.com/93198418/154659820-39942599-a7ef-4245-9d4f-96329dd76f0d.png)  

3) Проверьте открытые TCP порты в Ubuntu, какие протоколы и приложения используют эти порты? Приведите несколько примеров.

![image](https://user-images.githubusercontent.com/93198418/154660912-c81129d9-27c0-436f-8400-1f3fe41f173b.png)  
111 port - служба rpcbind (используется для nfs)  
53 port - служба systemd-resolve (внутренний dns)  
22 port - служба sshd (подключение по ssh)

4) Проверьте используемые UDP сокеты в Ubuntu, какие протоколы и приложения используют эти порты?

![image](https://user-images.githubusercontent.com/93198418/154663035-5b46cbec-5995-4e38-a9d4-fe00320ba9c7.png)  
111 port - служба rpcbind (используется для nfs)  
68 port - служба systemd-network (dhcp клиент)  
22 port - служба sshd (подключение по ssh)

5) Используя diagrams.net, создайте L3 диаграмму вашей домашней сети или любой другой сети, с которой вы работали.  

Вот созданная мной карта нашей сети из zabbix  
![image](https://user-images.githubusercontent.com/93198418/154664319-3a2239a2-f01b-429d-a8bd-50e1296796e9.png)  

6*) Установите Nginx, настройте в режиме балансировщика TCP или UDP.

Вот, написанный мной, промышленный конфиг nginx-web-proxy
```
root@vxus0108:/home/k.shevyakin# cat /etc/nginx/nginx.conf
user www-data;
worker_processes auto;
pid /run/nginx.pid;
include /etc/nginx/modules-enabled/*.conf;

events {
        worker_connections 768;
        # multi_accept on;
}

http {

        ##
        # Basic Settings
        ##

        sendfile on;
        tcp_nopush on;
        tcp_nodelay on;
        keepalive_timeout 65;
        types_hash_max_size 2048;
        # server_tokens off;

        # server_names_hash_bucket_size 64;
        # server_name_in_redirect off;

        include /etc/nginx/mime.types;
        default_type application/octet-stream;

        proxy_next_upstream error timeout invalid_header http_500 http_502; #http_404 ;

        log_format with_upstream '$remote_addr - $remote_user [$time_local] '
                    '"$request" $status $body_bytes_sent '
                    '"$http_referer" "$http_user_agent" upstream:$upstream_addr';

        ##
        # SSL Settings
        ##

        ssl_protocols TLSv1 TLSv1.1 TLSv1.2 TLSv1.3; # Dropping SSLv3, ref: POODLE
        ssl_prefer_server_ciphers on;

        ##
        # Logging Settings
        ##

#       access_log /var/log/nginx/access.log;
#       error_log /var/log/nginx/error.log;

        ##
        # Gzip Settings
        ##

#       gzip on;

        # gzip_vary on;
        # gzip_proxied any;
        # gzip_comp_level 6;
        # gzip_buffers 16 8k;
        # gzip_http_version 1.1;
        # gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;

        ##
        # Virtual Host Configs
        ##

        include /etc/nginx/conf.d/*.conf;
        include /etc/nginx/sites-enabled/*;
}


#mail {
#       # See sample authentication script at:
#       # http://wiki.nginx.org/ImapAuthenticateWithApachePhpScript
#
#       # auth_http localhost/auth.php;
#       # pop3_capabilities "TOP" "USER";
#       # imap_capabilities "IMAP4rev1" "UIDPLUS";
#
#       server {
#               listen     localhost:110;
#               protocol   pop3;
#               proxy      on;
#       }
#
#       server {
#               listen     localhost:143;
#               protocol   imap;
#               proxy      on;
#       }
#}
```
```
root@vxus0108:/home/k.shevyakin# cat /etc/nginx/conf.d/upstreams.conf
upstream upstream_obt {
    server 10.4.3.62 max_fails=2 fail_timeout=60s;
    server 10.4.3.63 max_fails=2 fail_timeout=60s;
    server 10.4.3.69 max_fails=2 fail_timeout=60s;
    server 10.4.3.70 max_fails=2 fail_timeout=60s;
}
```



