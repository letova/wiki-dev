# GIT

Краткий справочник

## Конфигурация

### Общие настройки

``` /etc/gitconfig``` системный конфигурационный файл (```--system```);

```~ /.gitconfig``` глобальный конфигурационный файл (```--global```, ```~``` - домашняя директория);

```.git/config``` локальный конфигурационный файл (```--local```);

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

```/.gitignore``` - файл для записи игнорируемых файлов или папок, изменения доступны всем

```/.git/info/exclude``` - измененения доступны только мне

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
игнорируем все папки и файлы в folder, кроме file.txt

```git check-ignore -v file-or-folder-path``` - вернет номер строки из .gitignore с записью, затрагивающей указанный файл или папку, если такая есть

## Старт

```git init``` - создать репозиторий

```git status``` - статус

```git add file.html``` -  добавить в индекс файл file.html

```git add .``` -  добавить все файлы

```git add -f file.txt``` - добавить файл минуя ```.gitignore```

```git reset HEAD file.html``` - убрать файл из индекса

```git rm file.css``` - удаляет файл и добавляет изменение в индекс (плюс ```-r``` для папок)

```git rm --cached file.css``` - удаляет только из индекса (плюс ```-r``` для папок)

```git commit -m "message"``` - коммит

```git commit -am "message"``` - сделать коммит минуя ```git add``` (игнорирует неотслеживаемые файлы)

```git commit -m "message" another-file.txt``` - сделать коммит минуя ```git add``` (файлы в индексе не попадут в коммит, игнорирует неотслеживаемые файлы)

```git commit --author='Person name <his@email.com>'``` - указать автора изменений

```git show --pretty=fuller``` - информация по последнему коммиту

```git mv read.txt readme.txt``` - переименовать и добавить в индекс