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

## Ветки

```git branch``` - просмотр веток

```git branch -v``` - просмотр веток c информацией о последнем коммите

```git branch branch-name``` - создать новую ветку

```git checkout branch-name``` - переключиться на ветку

```git checkout @{-1}``` - переключиться на ветку, с которой пришли

```git checkout -b branch-name``` - создать и переключиться на ветку

```git checkout -f branch-name``` - переключиться на ветку при незакоммиченных изменениях (изменения будут удалены)

```git checkout -f HEAD``` - стереть все незакоммиченные изменения

```git stash``` - спрятать изменения

```git stash pop``` - вернуть изменения

```git stash list``` - список спрятанных изменений

```git branch -f branch-name commit-num``` - сдвинуть ветку на определенный коммит (выполняется на другой ветке)

```git checkout -b branch-name commit-num``` - аналог

```git branch -f branch-name another-branch-name``` - сдвинуть ветку к последнему коммиту другой ветки

```git checkout commit-num``` - переход на определенный коммит

```git checkout file.txt``` - восстановление файла (отмена изменений)

```git checkout -- master``` - когда файл (master) совпадает с именем ветки

```git checkout commit-num file.txt``` - восстановление файла до определенного коммита

```git cherry-pick commit-num``` - скопировать коммит на текущую ветку

 ### История

```git log``` - просмотр истории коммитов

```git log --oneline``` - коммиты на одной строчке 

```git log branch-name --oneline``` - коммиты на конкретной ветке 

```git show HEAD~``` - информация по предпоследнему коммиту (```HEAD~~``` или ```HEAD~2```  предпредпоследнему)

```git show commit-name``` - информация по определенному коммиту

```git show HEAD~:file.txt``` - просмотреть файл в определенном коммите

```git show :/search-word``` - найти по слово

### Слияние

```
git checkout master
git merge branch-name
```
добавить в основную ветку master изменения с другой ветки

```.git/ORIG_HEAD``` - посмотреть номер последнего коммита master до изменений

```git branch -f master ORIG_HEAD``` - вернуть в исходное состояние

### Удаление

```git branch -d branch-name``` - удалить ветку (только если ветка объеденена с текущей)

```git reflog``` - лог ссылок, можно посмотреть номера коммитов удаленной ветки (изменения HEAD, хранит данные минимум 30 дней )

```git branch branch-name HEAD@{3}``` - пересоздать удаленную ветку с "недостижимыми" коммитами

```git gc``` - удаляет "недостижимые" коммиты

## Теги

```git tag v1.0.0 commit-name``` - теги создаются для отдельных коммитов (маркировка релизов например)

```git tag  -a -m "message" v1.0.0 commit-name``` - тег с анотацией

```git show --quiet v1.0.0``` - показать

```git tag -d v1.0.0``` - удалить тег

```git describe commit-name``` - показать тег по коммиту

```git describe``` - опишет HEAD

```git archive -o your-path/commit-describe.zip HEAD``` - сформировать архив на определенное состояние