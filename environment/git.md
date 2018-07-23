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

## Reset

```git reset commit-name``` - вернуться на определенный коммит

```git reset @~``` - вернуться на предыдущий коммит

```git reset --hard commit-name``` - сбрасывает и рабочую директорию и индекс

```git reset --hard HEAD``` - сбросить изменения (в т.ч. в индексе)

```git reset --hard ORIG_HEAD``` - вернуть состояние, до отката

```git reset --soft commit-name``` - не сбрасывает рабочую директорию и индекс

```git commit -c ORIG_HEAD``` - взять описание коммита, с которого откатились

```git commit --amend``` - правка последнего коммита

```git reset --mixed commit-name``` - сбрасывает индекс (значение reset по умолчанию )

```git reset HEAD``` - очистка индекса

```git reset commit-name file.txt``` - получить файл из коммита и сделать его текущим (обновляется только в индексе)

```git reset --keep @~``` - если файл не менялся между коммитами, файл остается в рабочей директории, сбрасывает индекс 

```git reset --merge``` - отмена конфликтного слияния, сбрасывает индекс

```git clean -f``` - удаление не отслеживаемых файлов

```git clean -df``` - удаление не отслеживаемых файлов и директорий

## Сравнение

```git diff commit-name commit-name``` - сравнение коммитов

```git diff commit-name:file.txt commit-name:file.txt``` - сравнение file.txt из разных коммитов

```git diff commit-name..commit-name``` - аналог

```git diff master...branch-name``` - что изменилось в ветке c момента расхождения с master

```git diff``` - изменения в рабочей директории с индексом (игнорирует неотслеживаемые файлы)

```git diff commit-name``` - изменения в рабочей директории с коммитом)

```git diff HEAD``` - изменения в рабочей директории с момента последнего коммита

```git diff --cached``` - изменения индекса с момента последнего коммита

```git commit -v``` - показывает изменения, которые хотим закоммитить

```git diff file.txt``` - вывод разницы конкретного файла

```git diff commit-name commit-name file.txt``` - сравнение file.txt из разных коммитов

```git diff --name-only commit-name commit-name``` - выводит имена файлов, которые различаются

```git diff --word-diff``` - сравнение по словам

```.gitattributes``` - настройки сравнения по словам (например: *.html diff=html)

```.git/config``` - создание своих настроек 

```
[diff "markdown"]
    # POSIX extended - синтаксис регулярных выражений
    xfuncname = "^#[[:space:]]+.+$"
    # Проверка для *word*
    wordRegex = "\\*+|[^[:space:]*]+"
    # Или любой символ - независимое слово (wordRegex = .)
```
пример для markdown
 
```git diff --word-diff-regex``` - передать регулярное выражение

##  История

```git log``` - просмотр истории (или ```git log --pretty=medium```)

```git log --pretty=oneline``` - одной строкой

```git log --pretty=oneline --abbrev-commit``` - скоращенный номер коммита (или ```git log --oneline```)

```
git log --pretty=format:'%h %cd | %s%d [%an]'
commit-name date | commit-description [author]

git log --pretty=format:'%h %cd | %s%d [%an] --date=short'
```

```git log -p``` - добаляет diff к каждому коммиту

```git log branch-name``` - вывод коммитов из ветки

```git log branch-name branch-name --graph``` - вывод коммитов из веток со структурой

```git log --all --graph``` - вывод стуктуры веток

```git log branch-name ^branch-name2``` - кроме коммитов из ветки 2 (или ```git log branch-name2..branch-name```)

```git log branch-name branch-name2``` - выведет уникальные коммиты

```git log branch-name branch-name2 --boundary``` - с пограничным коммитом

```git log file.txt``` - выведет коммиты где изменялся указанный файл

```git log --grep fix``` - вывод всех коммитов со словом fix в описании

```git log --Gfix``` -  поиск по изменениям

```git log --L 2,7:file.txt``` - вывод всех коммитов с изменениями со 2 по 7 строку файла

```git log --L '/<nav>/','/<\/nav>/':file.txt``` - с регулярными выражениями

```git log --before '2018-06-06'``` -  до определенной даты

```git blame``` - автор кода