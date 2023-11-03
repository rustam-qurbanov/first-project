

----

# Шпаргалка по Markdown:

[Github](https://gist.github.com/fomvasss/8dd8cd7f88c67a4e3727f9d39224a84c)

[Markdownguide](https://www.markdownguide.org/cheat-sheet/)

-----

# Шпаргалка. Базовые команды в консоли.


## Навигация:

- `pwd`     (от англ. **print working directory**, _«показать рабочую папку»_)     — покажи, в какой я папке;
- `ls`    (от англ. **list directory contents**, *«отобразить содержимое директории»*)      — покажи файлы и папки в текущей папке;
- `ls -a`         — покажи также скрытые файлы и папки, названия которых начинаются с символа « . » ;
- `cd first-project`     (от англ. **change directory**, *«сменить директорию»*)     — перейди в папку **first-project**;
- `cd first-project/html`         — перейди в папку **html**, которая находится в папке **first-project**;
- `cd ..`         — перейди на уровень выше, в родительскую папку;
- `cd` ~         — перейди в домашнюю директорию **(/Users/Username)**;
- `cd /`         — перейди в корневую директорию.

----

## Работа с файлами и папками.

## Создание:

- `touch index.html`     (англ. **touch**, *«коснуться»*)     — создай файл **index.html** в текущей папке;
- `touch index.html style.css script.js`         — если нужно создать сразу несколько файлов, можно напечатать их имена в одну строку через пробел;
- `mkdir second-project`    (от англ. **make directory**, *«создать директорию»*)      — создай папку с именем **second-project** в текущей папке.


## Копирование и перемещение:

- `cp file.txt ~/my-dir`     (от англ. **copy**, *«копировать»*)     — скопируй файл в другое место;
- `mv file.txt ~/my-dir`    (от англ. **move**, *«переместить»*)     — перемести файл или папку в другое место.

## Чтение:

- `cat file.txt`     (от англ. **concatenate and print**, *«объединить и распечатать»*)     — распечатай содержимое текстового файла **file.txt**.

## Удаление:

- `rm about.html`     (от англ. **remove**, *«удалить»*)     — удали файл **about.html**;
- `rmdir images`     (от англ. **remove directory**, *«удалить директорию»*)     — удали папку **images**;
- `rm -r second-project`     (от англ. **remove**, _«удалить»_ + **recursive**, _«рекурсивный»_)     — удали папку **second-project** и всё, что она содержит.

----
----

# Что такое хеш. Хеширование коммитов.

`Хеширование` (от англ. **hash**, *«рубить», «крошить», «мешанина»*) — это способ преобразовать набор данных и получить их `«отпечаток»` (англ. **fingerprint**).

Информация о коммите — это набор данных: когда был сделан коммит, содержимое файлов в репозитории на момент коммита и ссылка на предыдущий, или *родительский* (англ. **parent**), коммит.

**Git хеширует** (преобразует) информацию о коммите с помощью алгоритма **SHA-1** (от англ. **Secure Hash Algorithm** — *«безопасный алгоритм хеширования»*) и получает для каждого коммита свой уникальный хеш — результат хеширования.

Обычно хеш — это короткая (40 символов в случае **SHA-1**) строка, которая состоит из цифр 0 — 9 и латинских букв A - F (неважно, заглавных или строчных). Она обладает следующими важными свойствами:

- если хеш получить дважды для одного и того же набора входных данных, то результат будет гарантированно одинаковый;
- если хоть что-то в исходных данных поменяется (хотя бы один символ), то хеш тоже изменится (причём сильно).

Чтобы убедиться в этом, можно поэкспериментировать с **SHA-1**  [на этом сайте](https://emn178.github.io/online-tools/sha1.html) — попробуйте ввести в поле **input** (англ. *«ввод»*) разные символы, слова или предложения и понаблюдайте, как меняется хеш в поле **output** (англ. *«вывод»*).


## Хеш — основной идентификатор коммита.

**Git** хранит таблицу соответствий `хеш → информация о коммите.` Если вы знаете хеш, вы можете узнать всё остальное: автора и дату коммита и содержимое закоммиченных файлов. Можно сказать, что хеш — основной идентификатор коммита.

При работе с **Git** хеши будут встречаться вам регулярно. Их можно будет передавать в качестве параметра разным **Git-командам**, чтобы указать, с каким коммитом нужно произвести то или иное действие.

Все хеши и таблицу `хеш → информация о коммите Git` сохраняет в служебные файлы. Они находятся в скрытой папке `.git` в репозитории проекта.


### Теперь вы знаете, что такое хеш коммита и для чего он нужен. Подведём итоги:

- Git преобразует информацию о коммитах с помощью алгоритма **SHA-1** и для каждого из них рассчитывает уникальный идентификатор — хеш.
- Хеш — основной идентификатор коммита и позволяет узнать его автора, дату и содержимое закоммиченных файлов.
- Все хеши, а также таблицу соответствий `хеш → информация о коммите` Git хранит в папке `.git`.

----
----

# Исследуем лог.

> В этом уроке рассмотрим подробнее, из каких элементов состоит описание коммита, а также как вывести сокращённый лог (от англ. **log** — *«журнал записей»*). Сокращённый лог полезен, если нужно быстро найти нужный коммит среди сотни других.

## Элементы описания коммита.

После вызова `git log` появляется список коммитов.

![git log](/images/git-log.png)

Разберём элементы, из которых состоит описание:

- строка из цифр и латинских букв после слова **commit** — это хеш коммита;
- **Author** — имя автора и его электронная почта;
- **Date** — дата и время создания коммита;
- в конце находится сообщение коммита.

----
Вот так выглядит описание самого первого коммита в репозитории Git. Изучите его.

```
commit e83c5163316f89bfbde7d9ab23ca2e25604af290
Author: Linus Torvalds <torvalds@linux-foundation.org>
Date:   Thu Apr 7 15:13:13 2005 -0700

    Initial revision of "git", the information manager from hell
```

- Автор проекта Git — Linus Torvalds
> Это тот же Линус, который создал Linux.
- Git появился в апреле 2005 года
> Об этом сообщает поле **Date**.
- Автор описал Git как the information manager from hell
> Буквально так и написано!
----

## Получить сокращённый лог — `git log --oneline`

Получить сокращённый лог можно с помощью команды `git log` с флагом `--oneline` (англ. _«одной строкой»_). В терминале появятся только первые несколько символов хеша каждого коммита и их комментарии.

![git log --oneline](/images/git-log--oneline.png)

Сокращённый лог полезен, если в репозитории уже много коммитов — например, сотни или тысячи. В этом случае можно быстро найти нужный по описанию.

Сокращённый хеш (то есть первые несколько символов полного) можно использовать точно так же, как и полный. Для этого команда `git log --oneline` автоматически подбирает такую длину сокращённых хешей, чтобы они были уникальными в пределах репозитория и **Git** всегда мог понять, о каком коммите идёт речь.

>💡 Обратите внимание: если выход из просмотра логов не произошёл автоматически, нажмите клавишу `Q` (от англ. **Quit** — *«выйти»*) в английской раскладке клавиатуры.

----
----

# HEAD — всему голова.

При вызове команды `git log` вы также могли заметить надпись `(HEAD -> master)` после хеша одного из коммитов. В этом уроке расскажем, что она означает.

![git log HEAD](/images/git-log-head.png)

## Файл `HEAD`

Файл `HEAD` (англ. *«голова», «головной»*) — один из служебных файлов папки `.git`. Он указывает на коммит, который сделан последним (то есть на самый новый).

В этом можно убедиться с помощью терминала. Перейдите в папку `.git` командой `cd`. Посмотрите содержимое файла `HEAD` командой `cat`.

```
$ pwd # посмотрели, где мы
/Users/user/dev/first-project

$ cd .git/
$ ls # посмотрели, какие есть файлы
COMMIT_EDITMSG  ORIG_HEAD  description  index  logs/     refs/
HEAD            config     hooks/       info/  objects/

$ cat HEAD # команда cat показывает содержимое файла
ref: refs/heads/master # в файле вот такая ссылка
```

Внутри `HEAD` — ссылка на служебный файл: `refs/heads/master` (или `refs/heads/main` в зависимости от названия ветки). Если заглянуть в этот файл, можно увидеть хеш последнего коммита.

```
$ cat refs/heads/master # взяли ссылку из файла HEAD
# внутри хеш
e007f5035f113f9abca78fe2149c593959da5eb7

$ git log 
# сверяем с хешем последнего коммита
commit e007f5035f113f9abca78fe2149c593959da5eb7
Author: John Doe <johndoe@example.com>
Date:   Tue Mar 28 00:26:53 2023 +0300

    Добавить амбиций в список дел

... # другие коммиты
```

Когда вы делаете коммит, **Git** обновляет `refs/heads/master` — записывает в него хеш последнего коммита. Получается, что HEAD тоже обновляется, так как ссылается на `refs/heads/master`.

При работе с **Git** указатель `HEAD` используется довольно часто. Мы уже упоминали, что многие команды **Git** принимают в качестве параметра хеш коммита. Если нужно передать последний коммит, то вместо его хеша можно просто написать слово `HEAD` — **Git** поймёт, что вы имели в виду последний коммит.

### Подытожим:

- В числе прочих файлов в папке `.git` есть служебный файл **HEAD**. Он указывает на самый свежий коммит.
- Вместо хеша последнего коммита можно написать слово `HEAD` — **Git** вас поймёт.

----
----

# Статусы файлов в Git.

До появления **Git** системы контроля версий выделяли только два статуса у файлов: *«уже закоммичен» и «ещё не закоммичен»*. Например, в **Subversion** (самой популярной **VCS** до эпохи **Git**) не нужно было выполнять команду — аналог `git add`, а можно было просто сделать коммит (`svn commit`). Эта команда по умолчанию добавляла в коммит все новые и изменённые файлы.

Такое поведение интуитивно более понятно. Зато Git даёт больше контроля за состоянием файлов. Хотя сначала это может показаться сложным, со временем вы оцените удобство более явного подхода.

## Статусы `untracked` / `tracked`, `staged` и `modified`.

Одна из ключевых задач Git — отслеживать изменения файлов в репозитории. Для этого каждый файл помечается каким-либо статусом. Рассмотрим основные:

- `untracked` (англ. *«неотслеживаемый»*)

 Мы говорили, что новые файлы в **Git-репозитории** помечаются как `untracked`, то есть неотслеживаемые. *Git «видит»*, что такой файл существует, но не следит за изменениями в нём. У `untracked`-файла нет предыдущих версий, зафиксированных в коммитах или через команду `git add`.

- `staged` (англ. *«подготовленный»*)

 После выполнения команды `git add` файл попадает в **staging area** (от англ. **stage** — _«сцена», «этап [процесса]»_ и **area** — _«область»_), то есть в список файлов, которые войдут в коммит. В этот момент файл находится в состоянии `staged`.

 В одном из предыдущих уроков мы сравнили коммит с фотографией. Можно развить эту аналогию и сказать, что команда `git add` добавляет персонажей (текущее содержимое файла или нескольких файлов) на сцену (англ. **stage**) для общей фотографии, а `git commit` делает снимок всей сцены целиком. 

> 💡 **Staging area, index и cache**
**Staging area** также называют **index** (англ. _«каталог»_) или **cache** (англ. _«кеш»_), а состояние файла `staged` иногда называют `indexed` или `cached`.
Все три варианта могут встречаться в документации и в качестве флагов команд **Git**. А также в интернете — например, в вопросах и ответах [на сайте Stack Overflow](https://stackoverflow.com/).

- `tracked` (англ. _«отслеживаемый»_)

 Состояние `tracked` — это противоположность `untracked`. Оно довольно широкое по смыслу: в него попадают файлы, которые уже были зафиксированы с помощью `git commit`, а также файлы, которые были добавлены в **staging area** командой `git add`. То есть все файлы, в которых **Git** так или иначе отслеживает изменения.

- `modified` (англ. _«изменённый»_)

 Состояние `modified` означает, что **Git** сравнил содержимое файла с последней сохранённой версией и нашёл отличия. Например, файл был закоммичен и после этого изменён.

> 💡 Для файлов в состояниях `staged` и `modified` обычно не указывают, что они также `tracked`, потому что это состояние подразумевается.

----
## Про `staged` и `modified`.

Команда `git add` добавляет в **staging area** только текущее содержимое файла. Если вы, например, сделаете `git add file.txt`, а затем измените `file.txt`, то новое содержимое файла не будет находиться в **staging**.

Git сообщит об этом с помощью статуса `modified`: файл изменён относительно той версии, которая уже в **staging**. Чтобы добавить в **staging** последнюю версию, нужно выполнить `git add file.txt` ещё раз.

## Типичный жизненный цикл файла в Git.

> Может показаться, что файлы в репозитории попадают в разные состояния хаотично. На практике это не так, и у большинства файлов вполне предсказуемый путь.

![git status](/images/git-status.png)

1. Файл только что создали. **Git** ещё не отслеживает содержимое этого файла. Состояние: `untracked`.
2. Файл добавили в staging area с помощью `git add`. Состояние: `staged` (+ `tracked`).
    - Возможно, изменили файл ещё раз. Состояния: `staged`, `modified` (+ `tracked`).
    
        > Обратите внимание: `staged` и `modified` у одного файла, но у разных его версий.
    - Ещё раз выполнили `git add`. Состояние: `staged` (+ `tracked`).

3. Сделали коммит с помощью `git commit`. Состояние: `tracked`.
4. Изменили файл. Состояние: `modified` (+ `tracked`).
5. Снова добавили в **staging area** с помощью `git add`. Состояния: `staged` (+ `tracked`).
6. Сделали коммит. Состояния: `tracked`.
7. Повторили пункты 4−7 много-много раз.

----
> Ура! Это был сложный урок, зато теперь вы знаете о состояниях и жизненном цикле файлов в Git чуть больше. Важное:

- Статусом `untracked` помечается файл, о существовании которого **Git** знает, но не следит за изменениями в нём. Этот статус — противоположность `tracked`, в который попадают все файлы, отслеживаемые **Git**.
- Файл переходит в статус `staged` после выполнения `git add`.
- Статус `modified` означает, что файл был изменён.
- Большинство файлов в проектах _«шагает»_ по следующему циклу: `«изменён» → «добавлен в список на коммит» → «закоммичен» → «изменён» →` и так далее.

----
----

