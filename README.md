# devops-netology  
## Шевякин Кирилл  

# Домашнее задание к занятию "08.01 Введение в Ansible"

## Подготовка к выполнению
1. Установите ansible версии 2.10 или выше.
2. Создайте свой собственный публичный репозиторий на github с произвольным именем.
3. Скачайте [playbook](./playbook/) из репозитория с домашним заданием и перенесите его в свой репозиторий.

## Основная часть
1. Попробуйте запустить playbook на окружении из `test.yml`, зафиксируйте какое значение имеет факт `some_fact` для указанного хоста при выполнении playbook'a.  
![image](https://user-images.githubusercontent.com/93198418/179488952-d14d70e0-28bc-425f-b37e-20800b008277.png)  

2. Найдите файл с переменными (group_vars) в котором задаётся найденное в первом пункте значение и поменяйте его на 'all default fact'.  
group_vars/all/examp.yml  
![image](https://user-images.githubusercontent.com/93198418/179489306-7fc35e71-6205-4204-bb5f-919813e55dd7.png)  
![image](https://user-images.githubusercontent.com/93198418/179489800-b07aeb43-271c-4c87-b388-17736f5a96c7.png)  

3. Воспользуйтесь подготовленным (используется `docker`) или создайте собственное окружение для проведения дальнейших испытаний.  
![image](https://user-images.githubusercontent.com/93198418/179491254-e4eb86f2-9156-478b-92d3-1bc15d643436.png)

4. Проведите запуск playbook на окружении из `prod.yml`. Зафиксируйте полученные значения `some_fact` для каждого из `managed host`.  
![image](https://user-images.githubusercontent.com/93198418/179500664-15d34bef-d2d1-483a-a3d7-5b0f98380fdf.png)  

5. Добавьте факты в `group_vars` каждой из групп хостов так, чтобы для `some_fact` получились следующие значения: для `deb` - 'deb default fact', для `el` - 'el default fact'.  
nano group_vars/deb/examp.yml  
nano group_vars/el/examp.yml  
![image](https://user-images.githubusercontent.com/93198418/179501438-46001f2c-a09e-440f-9107-ebdec4dab42f.png)  

6. Повторите запуск playbook на окружении `prod.yml`. Убедитесь, что выдаются корректные значения для всех хостов.
![image](https://user-images.githubusercontent.com/93198418/179502226-3234004a-6ec4-4f5a-8abe-83a539d15895.png)  

7. При помощи `ansible-vault` зашифруйте факты в `group_vars/deb` и `group_vars/el` с паролем `netology`.
![image](https://user-images.githubusercontent.com/93198418/179503054-2c11f9ae-997e-4ad4-92c3-494c439488ab.png)  

8. Запустите playbook на окружении `prod.yml`. При запуске `ansible` должен запросить у вас пароль. Убедитесь в работоспособности.
![image](https://user-images.githubusercontent.com/93198418/179503659-2c5a6d9d-c1f2-4f74-9f29-f4adcda2b717.png)  

9. Посмотрите при помощи `ansible-doc` список плагинов для подключения. Выберите подходящий для работы на `control node`.  
local                          execute on controller  
![image](https://user-images.githubusercontent.com/93198418/179505278-d85d6203-0aa2-4a8d-9d62-582726a7f8df.png)

10. В `prod.yml` добавьте новую группу хостов с именем  `local`, в ней разместите localhost с необходимым типом подключения.
![image](https://user-images.githubusercontent.com/93198418/179505833-4dc78d40-9ff0-45f4-be12-a80f44374054.png)

11. Запустите playbook на окружении `prod.yml`. При запуске `ansible` должен запросить у вас пароль. Убедитесь что факты `some_fact` для каждого из хостов определены из верных `group_vars`.
![image](https://user-images.githubusercontent.com/93198418/179505993-61270926-3231-4392-b4eb-c88b07670e10.png)

12. Заполните `README.md` ответами на вопросы. Сделайте `git push` в ветку `master`. В ответе отправьте ссылку на ваш открытый репозиторий с изменённым `playbook` и заполненным `README.md`.  


