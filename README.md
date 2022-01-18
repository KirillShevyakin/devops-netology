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

2) Какая альтернатива без pipe команде grep <some_string> <some_file> | wc -l? man grep поможет в ответе на этот вопрос. Ознакомьтесь с документом о других подобных некорректных вариантах использования pipe.  
  This is my personal favorite. There is actually a whole class of "Useless Use of (something) | grep (something) | (something)" problems but this one usually manifests itself   in scripts riddled by useless backticks and pretzel logic.
Anything that looks like

	something | grep '..*' | wc -l
can usually be rewritten like something along the lines of
	something | grep -c .   # Notice that . is better than '..*'
or even (if all we want to do is check whether something produced any non-empty output lines)
	something | grep . >/dev/null && ...
(or grep -q if your grep has that).
If something is reasonably coded, it might even already be setting its exit code to tell you whether it succeeded in doing what you asked it to do; in that case, all you have to check is the exit code:

	something && ...
I used to have a really wretched example of clueless code (which I had written up completely on my own, to protect the innocent) which I've moved to a separate page and annotated a little bit. It expands on the above and also has a bit about useless use of backticks  

Вместо grep <some_string> <some_file> | wc -l можно использовать grep -c <some_string> <some_file>  

3) Какой процесс с PID 1 является родителем для всех процессов в вашей виртуальной машине Ubuntu 20.04?  
  ![image](https://user-images.githubusercontent.com/93198418/149890591-0a3d8aab-2fb5-4435-997f-5ea29029a0db.png)  
  systemd - это менеджер начальной загрузки ОС  
  
4) Как будет выглядеть команда, которая перенаправит вывод stderr ls на другую сессию терминала?  

