#devops-netology
#Шевякин Кирилл

#Домашнее задание к занятию «2.1. Системы контроля версий.»

#Local .terraform directories
**/.terraform/*
Исключаются локальные директории в каталоге .terraform

#.tfstate files
*.tfstate
*.tfstate.*
Исключаются файлы с расширением tfstate

#Crash log files
crash.log
Исключаются файлы crash.log

#Exclude all .tfvars files, which are likely to contain sentitive data, such as
#password, private keys, and other secrets. These should not be part of version
#control as they are data points which are potentially sensitive and subject
#to change depending on the environment.
*.tfvars
Исключаются все файлы tfvars, в которых находятся секретные данные (ключи, пароли и т.д.)

#Ignore override files as they are usually used to override resources locally and so
#are not checked in
override.tf
override.tf.json
*_override.tf
*_override.tf.json
Исключаются все файлы, которые используются для переопределения локальных ресурсов

#Ignore CLI configuration files
.terraformrc
terraform.rc
Исключаются конфигурационные файлы terraformrc и terraform.rc

