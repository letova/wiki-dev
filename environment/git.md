# GIT

Краткий справочник

## Конфигурация

### Общие настройки

``` /etc/gitconfig``` системный конфигурационный файл (```--system```);

```~ /.gitconfig``` глобальный конфигурационный файл (```--global```, ```~``` - домашняя директория);

```cat .git/config``` локальный конфигурационный файл (```--local``);

```git config -h``` посмотреть все команды;

```git config --list``` посмотреть параметры всех конфигураций;

```git config --list --global``` посмотреть конкретную конфигурацию;

```git config --global user.name "your name"``` записать имя пользователя;

```git config --global user.email your@email.com``` записать емаил пользователя;

```git config --unset user.name ``` удалить имя пользователя;

```git config --remove-section user``` удалить всю секцию ```user```;

### Псевдонимы для команд

```git config --global alias.cf config``` создать алиас ```git cf``` === ```git config```

```git config --global alias.cfg 'config --global'``` создать алиас c параметрами

```git config --global alias.do '!git command; git another command;'```  создать алиас с несколькими командами

### Игнорирование файлов

```touch .gitignore``` - создать .gitignore

```# Something``` - комментарий

```file.txt``` -  игнорировать файл

```folder/``` - игнорировать все папки folder

```/folder/``` - игнорировать корневую папку folder

```*.exe``` - игнорировать файлы по фрагменту имени (NOT!!! file.exec или file.exe.txt);

```*.ex[ez]``` - один символ из нескольких (*.exe или *.exz, NOT!!! *.exez);

```file_201[5-9]``` - диапазон

```*.ex?``` - один произваольный символ

```**/*.html``` - произвольный путь 

```
.*
!.another_file
```
игнорируем все кроме .another_file

```
/folder/*
!filder/file.txt
```