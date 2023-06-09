![Logo](Git-Logo-1788C.png) 
# Работа с Git и GitHub

## 1. Проверка наличия установленного Git
В терминале выполнить команду *git --version*
Если Git установлен, появится сообщение с информацией о версии программыБ иначе будет сообщение об ошибке.


## 2. Установка Git
Загружаем последнюю версию Git https://git-scm.com/downloads
Устанавливаем с настройками по умолчанию.

## 3. Настройка Git
При первом использовании Git необходимо представиться, для этого нужно выполнить в терминале две команды:
```
git config --global user.name «Ваше имя английскими буквами»
git config --global user.email ваша почта@example.com
```
## 4. Инициализация репозитория

![картинка](gitInit.png)

**`Репозиторий Git`** — это виртуальное хранилище проекта. В нем можно хранить версии кода для доступа по мере необходимости.

Для того, чтобы инициализировать наш файл (добавить репозиторий) нужно в терминале ввести команду `git init`. Команду `git init` выполняют только один раз для первоначальной настройки нового репозитория. Выполнение команды приведет к созданию нового подкаталога `.git` в вашем рабочем каталоге. Кроме того, будет создана новая главная ветка.

## 5. Запись изменений в репозиторий

![картинка](gitadd.png)

Для того чтобы подготовить файл к сохранению изменения нужно в терминале ввести команду `git add`  
После этого нужно ввести команду `git commit -a -m` или `git commit -am` и добавить комментарий в ковычках ("")

Команда `git add` добавляет изменение из рабочего каталога в раздел проиндексированных файлов. Она сообщает *Git*, что вы хотите включить изменения в конкретном файле в следующий коммит. Однако на самом деле команда `git add` не оказывает существенного влияния на репозиторий: изменения регистрируются в нем только после выполнения команды `git commit`.

Наряду с этими командами вам понадобится команда `git status`, которая показывает состояние рабочего каталога и раздела проиндексированных файлов.

Работа над проектом ведется по стандартной схеме «редактирование — индексирование — коммит». Сначала вы редактируете файлы в рабочем каталоге. Когда вы будете готовы сохранить копию текущего состояния проекта, вы индексируете изменения командой `git add`. Затем вы вызываете команду `git commit`, которая добавляет проиндексированный снимок состояния в историю проекта. Для отмены коммита или проиндексированного снимка состояния используется команда `git reset`.

## 6. Просмотр истории коммитов

![картинка](commit.png)

Для того, чтобы посмотреть историю сохранений и изменения фалов нужно ввести команду `git log`

![картинка](gitstatus.png)

Каждый коммит имеет уникальный идентифицирующий хеш `SHA-1`. Эти идентификаторы используются для перемещения по временной шкале коммитов и возвращения к коммитам. По умолчанию `git log` показывает только коммиты текущей выбранной ветки. Но не исключено, что искомый коммит находится в другой ветке. Для просмотра всех коммитов во всех ветках используется команда `git log --branches=*`. Команда `git branch` используется для просмотра и посещения других веток. Так, команда `git branch -a` возвращает список имен всех известных веток. Просмотреть весь журнал коммитов одной из этих веток можно с помощью команды `git log <имя_ветки>`.

## 7. Перемещений между сохранениями (коммитами) и ветками

Для начала делаем команду `git log`. После того как вы нашли ссылку на нужный коммит в истории, для перехода к нему можно использовать команду `git checkout`. Команда `git checkout` — это простой способ *«загрузить»* любой из этих сохраненных снимков на компьютер разработчика. При стандартном процессе разработки указатель *HEAD* обычно указывает на главную ветку *main*(или *master*) или другую локальную ветку. Но при переключении на предыдущий коммит *HEAD* указывает уже не на ветку, а непосредственно на сам коммит. Такая ситуация называется состоянием открепленного указателя *HEAD*, и ее можно представить так:

![картинка](main.png)

Переход к старой версии файла не перемещает указатель *HEAD*. Он остается в той же ветке и в том же коммите, что позволяет избежать открепления указателя *HEAD*. После этого можно выполнить коммит старой версии файла в новый снимок состояния, как и в случае других изменений. Соответственно, такое использование команды `git checkout` применительно к файлу позволяет откатиться к прежней версии отдельного файла. 

Перемещение между ветками или коммитами происходит следующим образом:
```
git checkout <имя ветки> или git checkout <код ветки> (например *a1e8fb5*)
```

## 8. Игнорирование файлов

Неотслеживаемые файлы обычно подразделяются на две категории: файлы, недавно добавленные в проект и пока не отправленные в качестве коммитов, либо скомпилированные бинарные файлы (например, .pyc, .obj, .exe и т. д.). Включать файлы первой категории в выходные данные `git status` очень полезно, в то время как файлы второй категории могут затруднить отслеживание изменений в репозитории.

Для того чтобы исключить из отслежвания в репозитории файлы или папки необходимо создать файл ***.gitignore*** и записать в него название или шаблоны, соответствующие таким файлам или папкам

## 9. Создание веток в Git 

По умолчанию имя основной ветки в Git - это *master*.
Создать ветку можно командой:
```
git branch <название ветки>
```
Список веток в репозитории можно посмотреть с помощью команды `git branch`

*Информацию по перемещению между веток можно посмотреть в разделе 7*

## 10. Слияние веток и разрешение конфликтов

Для сливания выбранной ветки с текущей, нужно выбрать команду: 
```
git merge <название выбранной ветки>
```
При возникновении конфликта нужно выбрать тот вариант, ктороый Вас устроит или отредактировать изменения вручную после слияния.

## 11. Работа с удалёнными репозиториями

Для того, чтобы копировать внешний репозиторий на свой ПК нужно использовать команду `git clone`:
```
git clone <ссылка на внешний репозиторий>
```
Команда `git clone` составная: она не только
загружает все изменения, но и пытается слить 
все ветки на локальном компьютере и в
удаленном репозитории. 

Для того, чтобы скачать все из текущего репозитория и автоматически сделать *merge* (слияние) используется команда `git pull`

Отправить свою версию репозитория во внешний репозиторий поможет команда `git push`.

### Как настроить совместную работу Git и GitHub

1. Создать аккаунт на GitHub.com
2. Создать локальный репозиторий
3. "Подружить" ваш локальный и удалённый репозитории. 
*GitHub при создании нового репозитория подскажет, как это можно сделать*
4. Отправить (*push*) ваш локальный репозиторий в удалённый (на *GitHub*), при этом, возможно, вам нужно будет авторизоваться на удалённом репозитории
5. Провести изменения "с другого компьютера"
6. Выкачать (*pull*) актуальное состояние из удалённого репозитория

### Команда `pull request`

* команда для предложения изменений
* запрос на вливание изменений в репозиторий

В больших компаниях один ответственный за проект создает аккаунт. 
Другие пользователи дают команду `pull request`. 
Предлагать изменения на *GitHub* нужно в отдельной ветке.
Сначала пользователь копирует репозиторий на свой компьютер, делает *fork* репозитория, затем клонирует версию на своём ПК, создаёт ветку с предлагаемыми изменениями, отправляет изменения командой push в свой аккаунт на *GitHub* и даёт команду `pull request`. 

### Как сделать `pull request` 

* Делаем **fork** (ответвление) репозитория
* Делаем `git clone` **своей** версии репозитория
* Создаём новую ветку и в **НЕЁ** вносим свои изменения
* Фиксируем изменения (делаем коммиты)
* Отправляем свою версию в свой GitHub
* На сайте GitHub нажимаем кнопку `pull request` 

### Команда `git remout`

Команда `git remout` позволяет создавать, просматривать и удалять подключения к другим репозиториям. Удаленные подключения скорее похожи на закладки, чем на прямые ссылки на другие репозитории. Они служат удобными именами, с помощью которых можно сослаться на не очень удобный URL-адрес, а не предоставляют доступ к другому репозиторию в режиме реального времени.

По сути, команда `git remote` — это интерфейс для управления списком записей об удаленных подключениях, которые хранятся в файле **/.git/config** репозитория. Для просмотра текущего состояния списка удаленных подключений используются следующие команды.

Для просмотра конфигураций удалённого репозитория используются следующие команды в git:
```
git remote
```
Список ваших удаленных подключений к другим репозиториям.
```
git remote -v
```
Аналогично команде выше, но включает URL-адрес каждого подключения.

Для создания и изменения конфигураций удаленных репозиториев git:
```
git remote add <name> <url>
```

## 12. Основные команды Git

|Задача в Git        |    Заметки    |    Команды Git     |
|--------------------------|-----------------------|-----------------------------|
|Представьтесь ситеме Git|Указать имя автора и адрес электронной почты, которые будут использоваться в коммитах. Обратите внимание, что Git удаляет из user.name некоторые символы, например точки в конце.|git config --global user.name «Ваше имя английскими буквами» git config --global user.email ваша почта@example.com|
|Cоздание нового локального репозитория||git init|
||Если сервер удаленный, использовать следующую команду:|git clone <ссылка на внешний репозиторий>|
|Добавление файлов|Добавить один или несколько файлов в раздел проиндексированных файлов (индекс):|git add <имя_файла>|
|Коммит|Сделать коммит изменений в расположение HEAD (но не в удаленный репозиторий):|git commit -m "Комментарий к коммиту"|
||Сделать коммит файлов, которые вы добавили командой git add, а также файлов, которые вы с тех пор изменили:|git commit -a|
|Отправить|Отправить изменения в главную ветку удаленного репозитория:|git push origin main|
|Состояние|Вывести список всех файлов, которые вы изменили, а также файлов, которые еще нужно добавить или для которых нужно сделать коммит:|git status|
|Подключение к удаленному репозиторию|Если вы еще не подключили локальный репозиторий к удаленному серверу, добавьте сервер, чтобы можно было отправлять туда изменения:|git remote add origin|
||Вывести список всех настроенных на данный момент удаленных репозиториев:|git remote -v|
|Ветки|Создать новую ветку и переключиться на нее:|git checkout -b|
||Переключиться с одной ветки на другую:|git checkout|
||Вывести список всех веток в репозитории с указанием текущей ветки:|git branch|
||Удалить функциональную ветку:|git branch -d|
||Отправить ветку в удаленный репозиторий, чтобы другие разработчики могли с ней работать:|git push origin|
||Отправить все ветки в удаленный репозиторий:|git push --all origin|
||Удалить ветку из удаленного репозитория:|git push origin:|
|Обновление из удаленного репозитория|Получить изменения с удаленного сервера и выполнить их слияние с рабочим каталогом:|git pull|
||Выполнить слияние ветки с активной веткой:|git merge|
||Просмотреть все конфликты слияния: Предварительно просмотреть изменения перед слиянием:|git diff|
||Просмотреть конфликты с базовым файлом:|git diff --base|
||Устранить все конфликты вручную и пометить измененный файл:|git add|

## Заключение

В данной инструкции мы рассмотрели основные команды в Git и GitHub. Надеюсь данная инструкция была понятна и достаточно полноценна для работы с Git.

Желаю Вам такого же хорошего настроения как у этого котика:
![Барсик](IMG_3838.JPG)

## *`Всем спасибо!`*