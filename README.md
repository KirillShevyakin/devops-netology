# devops-netology  
## Шевякин Кирилл  

### Домашнее задание к занятию «2.4. Инструменты Git»  
1. Найдите полный хеш и комментарий коммита, хеш которого начинается на aefea.  
commit aefead2207ef7e2aa5dc81a34aedf0cad4c32545  
Update CHANGELOG.md  
  

2. Какому тегу соответствует коммит 85024d3?  
commit 85024d3100126de36331c6982bfaac02cdab9e76 (tag: v0.12.23)
v0.12.23  

  
3. Сколько родителей у коммита b8d720? Напишите их хеши.  
56cd7859e05c36c06b56d013b55a252d0bb7e158 9ea88f22fc6269854151c571162c5bcf958bee2b  


4. Перечислите хеши и комментарии всех коммитов которые были сделаны между тегами v0.12.23 и v0.12.24.  
b14b74c49 [Website] vmc provider links  
3f235065b Update CHANGELOG.md  
6ae64e247 registry: Fix panic when server is unreachable  
5c619ca1b website: Remove links to the getting started guide's old location  
06275647e Update CHANGELOG.md  
d5f9411f5 command: Fix bug when using terraform login on Windows  
4b6d06cc5 Update CHANGELOG.md  
dd01a3507 Update CHANGELOG.md  
225466bc3 Cleanup after v0.12.23 release  


5. Найдите коммит в котором была создана функция func providerSource, ее определение в коде выглядит так func providerSource(...) (вместо троеточего перечислены аргументы).    
C:\git\tf\terraform> git log 8c928e835  
commit 8c928e83589d90a031f811fae52a81be7153e82f  
Author: Martin Atkins <mart@degeneration.co.uk>  
Date:   Thu Apr 2 18:04:39 2020 -0700  


    main: Consult local directories as potential mirrors of providers

    This restores some of the local search directories we used to include when
    searching for provider plugins in Terraform 0.12 and earlier. The
    directory structures we are expecting in these are different than before,
    so existing directory contents will not be compatible without
    restructuring, but we need to retain support for these local directories
    so that users can continue to sideload third-party provider plugins until
    the explicit, first-class provider mirrors configuration (in CLI config)
    is implemented, at which point users will be able to override these to
    whatever directories they want.

    This also includes some new search directories that are specific to the
    operating system where Terraform is running, following the documented
    layout conventions of that platform. In particular, this follows the
    XDG Base Directory specification on Unix systems, which has been a
    somewhat-common request to better support "sideloading" of packages via
    standard Linux distribution package managers and other similar mechanisms.
    While it isn't strictly necessary to add that now, it seems ideal to do
    whatever directories they want.

    This also includes some new search directories that are specific to the
    operating system where Terraform is running, following the documented
    layout conventions of that platform. In particular, this follows the
    XDG Base Directory specification on Unix systems, which has been a
    somewhat-common request to better support "sideloading" of packages via
    standard Linux distribution package managers and other similar mechanisms.
    While it isn't strictly necessary to add that now, it seems ideal to do
    all of the changes to our search directory layout at once so that our
    documentation about this can cleanly distinguish "0.12 and earlier" vs.
    "0.13 and later", rather than having to document a complex sequence of
    smaller changes.

    Because this behavior is a result of the integration of package main with
    package command, this behavior is verified using an e2etest rather than
    a unit test. That test, TestInitProvidersVendored, is also fixed here to
    create a suitable directory structure for the platform where the test is
    being run. This fixes TestInitProvidersVendored.
  
6. Найдите все коммиты в которых была изменена функция globalPluginDirs  
78b122055 Remove config.go and update things using its aliases  
52dbf9483 keep .terraform.d/plugins for discovery  
41ab0aef7 Add missing OS_ARCH dir to global plugin paths  
66ebff90c move some more plugin search path logic to command
8364383c3 Push plugin discovery down into command package  


7. Кто автор функции synchronizedWriters?  
C:\git\tf\terraform> git log 5ac311e2a  
commit 5ac311e2a91e381e2f52234668b49ba670aa0fe5  
Author: Martin Atkins <mart@degeneration.co.uk>  
Date:   Wed May 3 16:25:41 2017 -0700  


    main: synchronize writes to VT100-faker on Windows

    We use a third-party library "colorable" to translate VT100 color
    sequences into Windows console attribute-setting calls when Terraform is
    running on Windows.

    colorable is not concurrency-safe for multiple writes to the same console,
    because it writes to the console one character at a time and so two
    concurrent writers get their characters interleaved, creating unreadable
    garble.

    Here we wrap around it a synchronization mechanism to ensure that there
    can be only one Write call outstanding across both stderr and stdout,
    mimicking the usual behavior we expect (when stderr/stdout are a normal
    file handle) of each Write being completed atomically.

