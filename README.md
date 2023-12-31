# Шпаргалка по Git
## Что такое Git
**Git** (произносится *«гит»*) — распределённая система управления версиями. Система контроля версий, или *VCS*, — это программное обеспечение, которое помогает отслеживать изменения в программах, текстовых файлах, больших документах, веб-сайтах и так далее.  
Одно изменение или группу изменений в VCS называют ревизией или версией. Каждая такая ревизия содержит информацию о том, что изменилось, кто внёс изменения, когда это было и иногда комментарии к изменению.

Основные функции системы контроля версий:
- хранит историю изменений в виде отдельных ревизий;
- позволяет манипулировать историей: например, менять порядок ревизий, полностью удалять версии, возвращаться назад в истории;
- помогает анализировать изменения: например, кто и когда вносит изменения, кто чаще всего вносит изменения в определённый файл и так далее.

Git — незаменимый в команде инструмент, ведь он помогает объединять результаты работы нескольких человек.

## Установка Git
Для ОС Windows необходимо установить пакет `Git for Windows`, в который входит `GitBash` (командная строка).  
Откройте его и выполните команду.
```
git version
```
Если Git установлен правильно, консоль выведет его текущую версию.

## Настройка Git
Сейчас вы работаете в одиночку, но в дальнейшем вам может понадобиться использовать Git в команде. Чтобы участникам проекта было понятно, кто и какие изменения вносил, нужно представиться и указать имя пользователя и адрес электронной почты.

Вы можете указать любую электронную почту и любое имя. Сделать это можно с помощью команды `git config` (от англ. *configuration* — «конфигурация», «настройка») с ключом `--global` (англ. *«глобальный»*). При этом не имеет значения, в какой директории вы находитесь прямо сейчас: вызов `git config --global` сработает везде.
В качестве значения `user.name` нужно указать своё имя или никнейм. Для настройки параметра `user.email` указывают электронную почту.
```
$ git config --global user.name "User Namovich" 
# имя или ник нужно написать латиницей и в кавычках

$ git config --global user.email username@yandex.ru
# здесь нужно указать свой настоящий email 
```

Все глобальные настройки Git хранит в файле `.gitconfig` в домашней директории. Команда запишет в этот файл указанные имя и почту. Чтобы убедиться в этом, можно вызвать команду для чтения файлов. В ответ командная строка покажет текущие значения настроек.

## Работа с коммитами
### Инициализация репозитория
Чтобы Git начал отслеживать изменения в проекте, папку с файлами этого проекта нужно сделать **Git-репозиторием** (от англ. *repository* — «хранилище»). Для этого следует переместиться в неё и ввести команду `git init` (от англ. ***init**ialize* — «инициализировать»).

Например, создайте папку **first-project** и сделайте её Git-репозиторием: перейдите в неё с помощью команды `cd` и выполните `git init`.
```
$ cd ~/dev/first-project # перешли в нужную папку

$ git init # создали репозиторий
```

Если вы случайно сделали Git-репозиторием не ту папку, её можно «разгитить». Для этого нужно удалить скрытую подпапку `.git`.
```
$ cd <папка с репозиторием> # перешли в папку
$ rm -rf .git # удалили подпапку .git
```
> Будьте осторожны: в подпапке .git хранится история изменений. Если удалить .git, то вся история проекта будет стёрта без возможности восстановления — останется только последняя версия файлов.

### Проверить состояние репозитория
После инициализации репозитория *first-project* запустите команду `git status` — она показывает текущее состояние репозитория.

Команда `git status` выведет:
- название текущей ветки: `On branch master` или `On branch main`;
- сообщение о том, что в репозитории ещё нет коммитов: `No commits yet`;
- сообщение, которое говорит: «чтобы что-нибудь закоммитить (то есть зафиксировать), нужно сначала это создать» — `nothing to commit (create/copy files and use "git add" to track)`.

### Подготовить файлы к сохранению
Создайте файлы `todo.txt` и `readme.txt` в папке `first-project` и запустите `git status`, чтобы посмотреть, что изменилось.
Git сообщит, что в папке first-project есть `untracked files` — ещё не отслеживаемые файлы readme.txt и todo.txt.

Сейчас в first-project два файла. Мы хотим отслеживать состояние обоих, поэтому можем использовать команду `git add --all`. Ключ, или флаг, `--all` позволяет подготовить к сохранению все файлы в репозитории.
```
$ git add --all # подготовили к сохранению все файлы в репозитории
$ git status # проверили статус 
```
Добавлять файлы можно и по одному, без ключа `--all`.
```
$ git add todo.txt
$ git add readme.txt
$ git status
```
Также можно добавить текущую папку целиком — в этом случае все файлы в ней тоже будут добавлены. Обратиться к текущей папке в Bash позволяет точка `(.)`.
```
$ git add . # добавить всю текущую папку
$ git status 
```

### Выполнить коммит
Сделать коммит можно командой `git commit` c ключом `-m`, который присваивает коммиту сообщение.
```
$ git commit -m ‘Мой первый коммит!’ 
```
### Просмотреть историю коммитов
Чтобы увидеть историю коммитов, введите команду `git log`.
Обратите внимание, что по умолчанию `git log` выводит коммиты в обратном хронологическом порядке — последние коммиты оказываются первыми сверху. В этом можно убедиться, если посмотреть на дату и время их создания.

## GitHub
### Что такое GitHub
**GitHub** — платформа для хранения IT-проектов и совместной работы над ними с использованием Git. По сути, это сайт, куда можно загрузить файлы своего проекта для обмена с другими людьми. Кроме GitHub, существуют и другие подобные платформы, например GitLab, Bitbucket и так далее.
Git и GitHub — это два разных проекта, которые развиваются независимо друг от друга. 
Git:
- консольный инструмент для работы с локальными и удалёнными репозиториями;
- проект с открытым исходным кодом.

GitHub:
- платформа для размещения удалённых репозиториев;
- принадлежит компании Microsoft.

### Инструкция по созданию репозитория на GitHub
1. Предварительно зарегистривовшись, зайдите в свой профиль по ссылке `https://github.com/username`, где `username` — имя, которое вы указали при регистрации.
2. Создайте репозиторий. Для этого перейдите на вкладку **Repositories** (англ. «репозитории»), а затем нажмите на зелёную кнопку **New** (англ. «новый») справа. 
3. Открылось окно создания нового репозитория. Назовите его *first-project*. Название удалённого репозитория необязательно должно совпадать с именем папки проекта у вас на компьютере. Но чтобы не путаться, будем называть их одинаково. 
 Другие поля вам пока не понадобятся. Смело нажимайте на зелёную кнопку **Create repository** (англ. «создать репозиторий») внизу.
4. Готово! Удалённый репозиторий создан.

### Генерация SSH-ключа
Выполнить генерацию и привязку ключа в соответствии с интсрукцией на Яндекс-практикуме.

### Связывание локального и удаленного репозитория
Перейдите на страницу удалённого репозитория, выберите тип `SSH` и скопируйте URL. Кнопка справа позволит сделать это мгновенно.

Откройте консоль, перейдите в каталог локального репозитория и введите команду `git remote add` (от англ. remote — «удалённый» и add — «добавить»).
```
$ cd ~/dev/first-project
$ git remote add origin git@github.com:%ИМЯ_АККАУНТА%/first-project.git 
```
Осталось убедиться, что всё работает, с помощью следующей команды.
```
$ git remote -v
```
### Отправка изменений на удаленный репозиторий
Осталось загрузить содержимое локального репозитория на GitHub. За это отвечает команда `git push` (от англ. push — «толкать»).
В первый раз эту команду нужно вызвать с флагом `-u` и параметрами `origin` (имя удалённого репозитория) и `main` или `master` (название текущей ветки). Флаг `-u` свяжет локальную ветку с одноимённой удалённой. Как вы связывали локальный и удалённый репозитории в предыдущем уроке, так же и здесь нужно дополнительно связать ветки.
```
$ git push -u origin main # Если команда приведёт к ошибке, попробуйте 
                          # заменить main на master. 
```
В дальнейшем при работе с удалённым репозиторием флаг `-u` можно опустить и писать просто `git push`.

## Навигация по коммитам. Статусы файлов
### Хеш — идентификатор коммита
Информация о коммите — это набор данных: когда был сделан коммит, содержимое файлов в репозитории на момент коммита и ссылка на предыдущий, или родительский (англ. *parent*), коммит.

Git хеширует (преобразует) информацию о коммите с помощью алгоритма **SHA-1** (от англ. **S**ecure **H**ash **A**lgorithm — «безопасный алгоритм хеширования») и получает для каждого коммита свой уникальный хеш — результат хеширования.

Обычно хеш — это короткая (4040 символов в случае SHA-1) строка, которая состоит из цифр **0—9** и латинских букв **A—F** (неважно, заглавных или строчных). Она обладает следующими важными свойствами:
- если хеш получить дважды для одного и того же набора входных данных, то результат будет гарантированно одинаковый;
- если хоть что-то в исходных данных поменяется (хотя бы один символ), то хеш тоже изменится (причём сильно).

Git хранит таблицу соответствий `хеш → информация о коммите.` Если вы знаете хеш, вы можете узнать всё остальное: автора и дату коммита и содержимое закоммиченных файлов. Можно сказать, что хеш — основной идентификатор коммита.
При работе с Git хеши будут встречаться вам регулярно. Их можно будет передавать в качестве параметра разным Git-командам, чтобы указать, с каким коммитом нужно произвести то или иное действие.
Все хеши и таблицу `хеш → информация о коммите `Git сохраняет в служебные файлы. Они находятся в скрытой папке .git в репозитории проекта.

### Исследуем лог
После вызова `git log` появляется список коммитов.

Разберём элементы, из которых состоит описание:
- строка из цифр и латинских букв после слова **commit** — это хеш коммита;
- **Author** — имя автора и его электронная почта;
- **Date** — дата и время создания коммита;
- в конце находится сообщение коммита.

Получить сокращённый лог можно с помощью команды `git log` с флагом `--oneline` (англ. «*одной строкой*»). В терминале появятся только первые несколько символов хеша каждого коммита и их комментарии.

Сокращённый лог полезен, если в репозитории уже много коммитов — например, сотни или тысячи. В этом случае можно быстро найти нужный по описанию.
Сокращённый хеш (то есть первые несколько символов полного) можно использовать точно так же, как и полный. Для этого команда `git log --oneline` автоматически подбирает такую длину сокращённых хешей, чтобы они были уникальными в пределах репозитория и Git всегда мог понять, о каком коммите идёт речь.

> Обратите внимание: если выход из просмотра логов не произошёл автоматически, нажмите клавишу `Q` (от англ. **Q**uit — «выйти») в английской раскладке клавиатуры.

### HEAD — всему голова
При вызове команды `git log` вы также могли заметить надпись `(HEAD -> master)` после хеша одного из коммитов.

Файл `HEAD` (англ. «голова», «головной») — один из служебных файлов папки `.git`. Он указывает на коммит, который сделан последним (то есть на самый новый).
В этом можно убедиться с помощью терминала. Перейдите в папку `.git` командой `cd`. Посмотрите содержимое файла `HEAD` командой `cat`.

Внутри HEAD — ссылка на служебный файл: `refs/heads/master` (или refs/heads/main в зависимости от названия ветки). Если заглянуть в этот файл, можно увидеть хеш последнего коммита.

Когда вы делаете коммит, Git обновляет `refs/heads/master` — записывает в него хеш последнего коммита. Получается, что `HEAD` тоже обновляется, так как ссылается на `refs/heads/master`.
При работе с Git указатель `HEAD` используется довольно часто. Мы уже упоминали, что многие команды Git принимают в качестве параметра хеш коммита. Если нужно передать последний коммит, то вместо его хеша можно просто написать слово `HEAD` — Git поймёт, что вы имели в виду последний коммит.

### Статусы файлов в Git
Одна из ключевых задач Git — отслеживать изменения файлов в репозитории. Для этого каждый файл помечается каким-либо статусом. Рассмотрим основные.
- `untracked` (англ. «неотслеживаемый»)
Мы говорили, что новые файлы в Git-репозитории помечаются как untracked, то есть неотслеживаемые. Git «видит», что такой файл существует, но не следит за изменениями в нём. У `untracked`-файла нет предыдущих версий, зафиксированных в коммитах или через команду `git add`.
- `staged` (англ. «подготовленный»)
После выполнения команды `git add` файл попадает в `staging area` (от англ. stage — «сцена», «этап [процесса]» и area — «область»), то есть в список файлов, которые войдут в коммит. В этот момент файл находится в состоянии `staged`.
 В одном из предыдущих уроков мы сравнили коммит с фотографией. Можно развить эту аналогию и сказать, что команда `git add` добавляет персонажей (текущее содержимое файла или нескольких файлов) на сцену (англ. stage) для общей фотографии, а `git commit` делает снимок всей сцены целиком. 
- `tracked` (англ. «отслеживаемый»)
Состояние `tracked` — это противоположность `untracked`. Оно довольно широкое по смыслу: в него попадают файлы, которые уже были зафиксированы с помощью `git commit`, а также файлы, которые были добавлены в `staging area` командой `git add`. То есть все файлы, в которых Git так или иначе отслеживает изменения.
- `modified` (англ. «изменённый»)
Состояние `modified` означает, что Git сравнил содержимое файла с последней сохранённой версией и нашёл отличия. Например, файл был закоммичен и после этого изменён.

> Для файлов в состояниях staged и modified обычно не указывают, что они также tracked, потому что это состояние подразумевается.

Команда `git add` добавляет в **staging area** только текущее содержимое файла. Если вы, например, сделаете `git add file.txt`, а затем измените **file.txt**, то новое содержимое файла не будет находиться в **staging**.
Git сообщит об этом с помощью статуса `modified`: файл изменён относительно той версии, которая уже в **staging**. Чтобы добавить в **staging** последнюю версию, нужно выполнить `git add file.txt` ещё раз.

![image](https://pictures.s3.yandex.net/resources/M2_T5_1686651284.png "Жизненный цикл")

### Какие состояния показывает `git status`
Большинство файлов в типичном проекте будут находиться в состоянии `tracked` (то есть закоммичены и не изменены после коммита). Вы не увидите это состояние в выводе команды `git status` — иначе она бы каждый раз выводила список вообще всех файлов проекта.
В итоге git status показывает только следующие состояния файлов:
- `staged` (`Changes to be committed` в выводе `git status`);
- `modified` (`Changes not staged for commit`);
- `untracked` (`Untracked files`).

## Работа над ошибками в коммитах
### Оформление сообщений к коммитам
То, как написаны сообщения коммитов, тоже может подчиняться определённым правилам. Иногда эти правила продиктованы культурой команды, а иногда техническими ограничениями.
Например, в выводе команды `git log --oneline` умещается максимум 72 первых символа сообщения, поэтому многие правила включают пункт: «Сообщение не должно быть длиннее 72 символов».
Хорошо, когда:
- сообщение коммита легко читается;
- оно информативное;
- все сообщения оформлены в одном стиле.