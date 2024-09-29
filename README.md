# Система контроля версий Git

## Основные задачи Git

* хранение истории изменений проекта
* манипулирование историей изменений (порядок ревизий, удаление версий, возвращение назад в историю)
* анализ изменений (кто и когда вносил изменения, кто чаще всего вносил изменения и т. д.)

**Ключевая особенность:** поддержка параллельной работы нескольких пользователей, в том числе над одним фалом (проектом).

Управление Git чаще всего производится с помощью командной строки (консоль).  
Один из вариантов консольного инструмента называется Git Bash, его можно установить сразу вместе с Git.  
[Нажмите по этому тексту для установки с официального сайта Git](https://git-scm.com/download/win)  

## Основные команды командной строки

| Команда    | Результат                                                |
|------------|----------------------------------------------------------|
|pwd         | показать текущую директорию                              |
|cd          | сменить директорию (change directory)                    |
|cd ~        | перейти в домашнюю директорию                            |
|cd ..       | вернуться на уровень выше                                |
|cd .        | обратиться к текущей директории                          |
|ls          | Вывести содержимое директории                            |
|ls -a       | Вывести содержимое директории со крытыми файлами         |
|ls ~        | вывод домашней директории из любого места                |
|ls ..       | вывод родительской директории                            |
|touch       | создать файл                                             |
|mkdir       | создать директорию                                       |
|mkdir -p    | создать структуру директорий (внешняя/средняя/внутренняя)|
|mkdir ~/    | создать папку в домашней директории из любого места      |
|touch ../.. | создать файл в папке на одну или несколько выше          |
|cp          | копирование файла или нескольких                         |
|mv          | переместить файл или папку                               |
|cat         | чтение файлов                                            |
|rm          | удаление файла                                           |
|rmdir       | удаление папки                                           |
|rm -r       | удаление папки с вложенными файлами и папками            |

Символы **&&** - используются для введения сразу нескольких команд.  
*Пример:* mkdir "папка" && cd "папка" && touch "файл"

**Tab** - используется для различных вариантов автозаполнения и подсказок.

Стрелками **ВВЕРХ** или **ВНИЗ** на клавиатуре можно вызывать все введенные предыдущие команды.


## Основы работы с Git

Для настройки необходимо указать электронную почту и имя (ник).  
Это можно сделать с помощью команд:  
git config --global user.name "имя"  *(имя указывается в кавычках)*  
git config --global user.email username@yandex.ru

Проверить что данные сохранились можно командами: 
cat ~/.gitconfig
git config --list

## Основные команды для работы с репозиторием

| Команда    | Результат                                                  |
|------------|------------------------------------------------------------|
|git init      | сделать папку репозиторием                               |
|rm -rf .git   | «Разгитить» папку, если что-то пошло не так              |
|git status    | проверить состояние репозитория                          |
|git add       | подготовить файлы к сохранению (в текущей папке)         |
|git add --all | подготовить все файлы к сохранению из текущей папки      |
|git add .     | добавить текущую папку целиком                           |
|git commit    | сделать коммит                                           |
|git commit -m | сделать коммит с комментарием (комментарий в кавычках)   |
|git log       | посмотреть историю коммитов                              |


## Основы работы с GitHub

**GitHub - платформа для удаленного хранения IT-проектов (репозиториев) и их командной разработки с использованием Git.**  
Для работы с GitHub необходимо зарегистрироваться на сайте (ссылка ниже)  
https://github.com/

Создание нового удаленного репозитория производится прямо на странице GitHub с помощью кнопки - **New** (во вкладке Repositories).

Чтобы связать удаленный репозиторий и локальный необходимо:
* создать на компьютере SSH-ключи и связать их с GitHub-аккаунтом
* связать локальный репозиторий с удаленным командой: git remote add origin SSH URL  
  (где SSH URL - это ссылка из удаленного репозитория)
* убедиться, что репозитории связаны командой: git remote -v
* отправить изменение на удаленный репозиторий командой: git push  
  (в первый раз в виде: git push -u origin main)

**Для клонирования** на локальный репозиторий необходимо открыть удаленный репозиторий и на вкладке **Code**,
выбрав SSH скопировать ссылку, далее вставить её после команды /**git clone**/ в командной строке, в той директории, в которую нужно клонировать проект.

**Для копирования** проекта в интересующем проекте необходимо нажать на кнопку **Fork**, и в открывшемся окне выбрав интересующие параметры нажать кнопку **Create fork**. После этого проект можно будет клонировать в локальный репозиторий.

## Хеш, лог и HEAD

**Хеш — идентификатор коммита**
Информация о коммите — это набор данных: когда был сделан коммит, содержимое файлов в репозитории на момент коммита и ссылка на предыдущий, или родительский, коммит. Git хеширует (преобразует) эту информацию с помощью алгоритма SHA-1 и получает для каждого коммита свой уникальный хеш — результат хеширования.

Хеш обладает следующими важными свойствами:
*если хеш получить дважды для одного и того же набора входных данных, то результат будет гарантированно одинаковый;
*если хоть что-то в исходных данных поменяется (хотя бы один символ), то хеш тоже изменится (причём сильно).

После вызова git log появляется список коммитов с их описанием.
Описание состоит из следующих элементов:
*Строка из цифр и латинских букв после слова commit — это уже знакомый вам хеш коммита.
*Author — имя автора и его электронная почта.
*Date — дата и время создания коммита.
*Сообщение к коммиту.

Если в репозитории уже много коммитов можно вызвать сокращенный лог: git log --oneline

Файл HEAD (англ. «голова», «головной») — один из служебных файлов папки .git. Он указывает на коммит, который сделан последним (то есть на самый новый).
Внутри HEAD — ссылка на служебный файл: refs/heads/master (или refs/heads/main в зависимости от названия ветки). Если заглянуть в этот файл, можно увидеть хеш последнего коммита.
Если нужно передать последний коммит, то вместо его хеша можно просто написать слово HEAD — Git поймёт, что вы имели в виду последний коммит.

## Статусы файлов (git status)

Статусы untracked/tracked, staged и modified:
*untracked (англ. «неотслеживаемый») - новые файлы в Git-репозитории, Git не следит за изменениями в них.
*staged (англ. «подготовленный») - после выполнения команды git add. Это список файлов, которые войдут в коммит.
*tracked (англ. «отслеживаемый») - в него попадают файлы, которые уже были зафиксированы с помощью git commit, а также файлы, которые были добавлены в staging area командой git add.
*modified (англ. «изменённый») - Git сравнил содержимое файла с последней сохранённой версией и нашёл отличия.

**Статус состояния файлов показывает команда git status**
*staged (Changes to be committed в выводе git status);
*modified (Changes not staged for commit);
*untracked (Untracked files).

## Оформление сообщений к коммитам

**Общие рекомендации по тому, как правильно составить сообщение**
 Оно должно быть:
*относительно коротким, чтобы его было легко прочитать;
*информативным.

Стили оформления коммитов:
*Корпоративный - команды могут договариваться, с какой части речи начинать сообщения и какой длины они должны быть.
*Conventional Commits - это стандарт коммитов, который отличается качественной документацией и подробной проработкой. Он подходит для репозиториев с исходным кодом программ.
*GitHub-стиль.
GitHub можно использовать не только для хранения файлов проекта, но и для ведения списка задач (англ. issue) этого проекта. Если коммит «закрывает» или «решает» какую-то задачу, то в его сообщении удобно указывать ссылку на неё. Для этого в любом месте сообщения нужно указать #<номер задачи>
