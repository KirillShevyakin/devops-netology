# devops-netology  
## Шевякин Кирилл  

### Домашнее задание к занятию "3.2. Работа в терминале, лекция 2"  
  
1) Какого типа команда cd? Попробуйте объяснить, почему она именно такого типа; опишите ход своих мыслей, если считаете что она могла бы быть другого типа.  
    root@vagrant:/home/vagrant# cd --help
    cd: cd [-L|[-P [-e]] [-@]] [dir]
    Change the shell working directory.

    Change the current directory to DIR.  The default DIR is the value of the
    HOME shell variable.

    The variable CDPATH defines the search path for the directory containing
    DIR.  Alternative directory names in CDPATH are separated by a colon (:).
    A null directory name is the same as the current directory.  If DIR begins
    with a slash (/), then CDPATH is not used.

    If the directory is not found, and the shell option `cdable_vars' is set,
    the word is assumed to be  a variable name.  If that variable has a value,
    its value is used for DIR.
        
    Команда cd меняет рабочую директорию в shell. Это внутренняя команда в shell, которая вызывает внутренюю функцию в shell изменения рабочей директории. Я думаю, что она не может быть другого     типа, потому что если бы она была внешним вызовом, то каждый раз при переходе в другую директорию, приходилось бы запускать новый shell.  

