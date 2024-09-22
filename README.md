# БАЗОВЫЕ КОМАНДЫ

### ИНИЦИАЛИЗИРОВАТЬ ЛОКАЛЬНЫЙ РЕПОЗИТОРИЙ
```bash
git init
```
### ПРОВЕРИТЬ СОСТОЯНИЕ
```bash
git status
```
### ПРОИНДЕКСИРОВАТЬ ИЗМЕНЕНИЯ ДЛЯ ПОСЛЕДУЮЩЕГО КОММИТА
```bash
git add <название_файла.расширение>
или
git add --all или git add . - проиндексировать сразу все файлы в текущей директории
```

Индекс - это промежуточная зона перед коммитом. В коммит будет внесены только изменения из индекса.

  Команда 'git status' покажет разницу между последним коммитом и текущим состоянием индекса. Вариантов два:

1. В файл внесены изменения, но еще не проиндексированы:

    <span style="color:red">"Changes not staged for commit:"</span> 

2. В файл внесены изменения и проиндексированы:

    <span style="color:green">"Changes to be committed:"</span> 

Важно понять, что отслеживаются не сами файлы, а их изменения.То есть если:

    1. Внести изменения в файл
    2. Проиндексировать эти изменения
    3. Внести другие изменения в файл
    4. Закоммитить изменения

В новый коммит запишутся только ПЕРВЫЕ изменения из пункта №1, а вторые изменения из пункта №3 остануться не тронутыми, потому что не были проиндексированы. Вот как это выглядит:
```bash
$ git status

On branch main

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   hello.html <------

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   hello.html <------
```
Файл hello.html находится в двух состояниях. Этот момент стоит помнить!

### ТЕГИ
```bash
git tag <имя_тега>    - устанавливает тег на текущий коммит
git tag               - посмотреть все теги
git tag -d <имя_тега> - удалить тег

Теги можно использовать вместо хэш кода в команде 'checkout'
```

### ПЕРЕМЕЩЕНИЕ / ПЕРЕИМЕНОВАНИЕ ФАЙЛОВ В ПРЕДЕЛАХ РЕПОЗИТОРИЯ
```bash
git mv <путь/до/файла/имя_файла>  <новый/путь/до/файла/имя_файла> - перемещение файла
git mv <имя_файла>  <новое_имя_файла> - переименование файла
```
Данный способ перемещения и переименование файлов в пределах репозитория используется чтобы не потерять историю изменений.

<br></br>

# КОММИТЫ

### СДЕЛАТЬ КОММИТ
```bash
git commit - m "Сообщение коммита поддерживает 

                перенос строк"
```
или 

```bash
git commit

    1. Открется редактор Vim с таким текстом:

 <Вот сюда пишешь текст коммита>
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch main
# Changes to be committed:
#       modified:   hello.html
#
    2. Затем нажимаешь клавишу "ESC"
    3. Пишешь ":wq"
    4. Нашимаешь клавишу "Enter"
```

### ПОСМОТРЕТЬ ИСТОРИЮ КОММИТОВ
```bash
git log
```
Вывод:
```bash
commit b7614c1aea1ffbc46400fe1a1 <---- ХЭШ КОММИТА
Author: Name <Email> <---- КТО ОПУБЛИКОВАЛ КОММИТ
Date:   Tue Nov 28 05:51:38 2023 -0600

    Added HTML header <---- СООБЩЕНИЕ КОММИТА

commit 46afaff2232fc3d564c40f6 <---- ХЭШ КОММИТА
Author: Name <Email> <---- КТО ОПУБЛИКОВАЛ КОММИТ
Date:   Tue Nov 28 05:51:38 2023 -0600

    Added standard HTML page tags <---- СООБЩЕНИЕ КОММИТА
```
Настрйоки для краткого вывода коммита:
```bash
git config --global format.pretty '%C(bold blue)%h%C(reset) - %C(bold green)(%ad)%C(reset) %C(white)%s%C(reset) %C(bold white)— %an%C(reset)%C(bold yellow)%d%C(reset)'
git config --global log.date short

% git log
c36fe44 2024-09-18 | Супер коммит (main) <-- ИМЯ ВЕТКИ
71fda4b 2024-09-17 | Added HTML header (HEAD) <-- УКАЗАТЕЛЬ НА ТЕКУЩИЙ ВЕТКУ
67de1e6 2024-09-17 | Added standard HTML page tags 
5198079 2024-09-17 | Добавил новый файл 
```

### ПЕРЕХОД К КОММТУ
```bash
git checkout <хэш_коммита> или <имя_тега>
```
После ввода этой команды указатель HEAD переместится на тот коммит, хэш которого был указан. Выйдет сообщение об "оторванной HEAD", но в этом нет ничего страшного. По умолчанию HEAD указывает в своем файле на последний коммит в ветке и "оторванная HEAD" - это просто не стандартное его состояние.

<br></br>

# ВЕТКИ:

### СОЗДАНИЕ ВЕТКИ
```bash
git switch -с <имя_ветки> - создает новую ветку и 
```

### ПЕРЕХОД НА ВЕТКУ
```bash
git switch <имя_ветки>
```

### ИСТОРИЯ КОММИТОВ С ОТОБРАЖЕНИЕМ ВЕТОК
```bash
git log --all --graph
```
Пример:
```bash
* b8c5608 2024-09-19 | Добавил файл README (HEAD -> main) [EredinHawk]
| * 8c28207 2024-09-19 | Renamed hello.html; moved style.css (style) [EredinHawk]
| * 04e4fe8 2024-09-19 | Included stylesheet into hello.html [EredinHawk]
| * 9476f1b 2024-09-19 | Added css stylesheet [EredinHawk]

|/  <------- РАЗДЕЛЕНИЕ НА ВЕТКИ ОТ РОДИТЕЛЬСКОГО КОММИТА

* 4261eaa 2024-09-18 | Исправил коммит чутка [EredinHawk]
* c36fe44 2024-09-18 | Супер коммит [EredinHawk]
* 71fda4b 2024-09-17 | Added HTML header (tag: v1) [EredinHawk]
* 67de1e6 2024-09-17 | Added standard HTML page tags (tag: v1-beta) [EredinHawk]
* 5198079 2024-09-17 | Добавил новый файл [EredinHawk]
```

### СЛИЯНИЕ (MERGE)
```bash
git switch main
git merge <имя_ветки>
```
Результат:
```bash
git log --all --graph

*   8a17c5f 2024-09-19 | Merge branch 'main' into style (HEAD -> style) [EredinHawk]

|\  <------- СЛИЯНИЕ 

| * b8c5608 2024-09-19 | Добавил файл README (main) [EredinHawk]
* | 8c28207 2024-09-19 | Renamed hello.html; moved style.css [EredinHawk]
* | 04e4fe8 2024-09-19 | Included stylesheet into hello.html [EredinHawk]
* | 9476f1b 2024-09-19 | Added css stylesheet [EredinHawk]
|/  
* 4261eaa 2024-09-18 | Исправил коммит чутка [EredinHawk]
```

Чтобы не запутаться!

Есть ветка main и ветка X. Если нужно слить ветку X в main, то сначала нужно перейти в main c помощью switch команды, а затем выполнить:
```bash
git merge X
```

### ПЕРЕБАЗИРОВАНИЕ (REBASE)
```bash
git rebase <имя_ветки>

Reabase также призводит слияние двух веток, но иначе. 

1. git switch X - Переходим на ветку, которую хотим слить с main
2. git rebase main - перебазируем Х ветку в main
3. git switch main - вернемся в main ветку
4. git merge X - сольем изменения, чтобы указатель HEAD перешел на перебазированный коммит
5. git branch -d X - удалим ветку, оставим только main
```
Данный способ делает слияние визуально чище. Вместо двух веток, остается только main, как будто мы не делали новых веток, а коммитили последовательно.


### ОТМЕНА СЛИЯНИЯ
```bash
git merge --abort
```

### УДАЛИТЬ ВЕТКУ
```bash
git branch -d <имя_ветки>
```

### УДАЛИТЬ ИЗ ИСТОРИИ УСТАРЕВШИЕ ВЕТКИ
```bash
git remote prune origin
```

<br></br>

# УДАЛЕННЫЕ РЕПОЗИТОРИИ
УДАЛЕННЫЕ - иметь ввиду те, которые размещены на платформе как публичные репозитории (тот же GitHub, GitLab, или на отдельном сервере)
### УЗНАТЬ ИМЕНА УДАЛЕННЫХ РЕПОЗИТОРИЕВ
```bash
git remote
git remote show origin 

Результат:

remote origin
  Fetch URL: /Users/eredinhawk/repositories/git
  Push  URL: /Users/eredinhawk/repositories/git
  HEAD branch: main
  Remote branch:
    main tracked
  Local branch configured for 'git pull':
    main merges with remote main
  Local ref configured for 'git push':
    main pushes to main (up to date)
```

### ПРОСМОТР УДАЛЕННЫХ ВЕТОК
```bash
git branch -a
```

### КЛОНИРОВАНИЕ
```bash
git clone <url_репозитория>
```

### ПОДГРУЗКА ИЗМЕНЕНИЙ С УДАЛЕННОГО НА ЛОКАЛЬНЫЙ РЕПОЗИТОРИЙ
```bash
git fetch - подгрузка изменений из remote
git merge origin/main - слияние подгруженных изменений с локальной main

или 

git pull - это 2 в 1 (fetch + merge)

git pull origin <имя_ветки> - подгружает конкретную ветку и сразу сливает ее с локальной
```

### ВЕТКА НАБЛЮДАТЕЛЬ
```bash
git branch --track <имя_локальной_ветки> origin/имя_удаленной_ветки

По умолчанию только ветка main отслеживает состояние origin/main. Данный способ создаст новую ветку локальном репозитории, которая будет отслеживать изменения в удаленной ветке.

Так же валидный метод:

git fetch origin <имя_ветки> - создаст новую ветку и начнет отслеживать ее изменения в удаленной ветке
```

### ПОДТЯГИВАНИЕ ОБЩИХ ИЗМЕНЕНИЙ
```bash
git remote add shared /url/общего/репозитория.git
git branch --track shared main
git pull shared main
```

<br></br>

# СБРОСЫ:

### СБРОСИТЬ ВСЕ ИЗМЕНЕНИЯ ДО ИНДЕКСАЦИИ
```bash
git checkout <имя_файла>
```

### СБРОСИТЬ ВСЕ ИЗМЕНЕНИЯ ПОСЛЕ ИНДЕКСАЦИИ
```bash
git reset HEAD <имя_файла> - отменяет команду add
git checkout  <имя_файла>

или

git restore <имя_файла> - сразу удалает изменения из индекса и рабочего файла
```

### СБРОСИТЬ КОММИТ

Есть два основных способа отменить коммит:

1. Создать новый коммит в котором отсутствуют изменения:
```bash
git revert <хэш_коммита_к_состоянию_которого_нужно_вернуться>
```
2. Жесткий способ, который полностью удаляет все изменения, как будто ничего и не было:
```bash
git reset --hard <хэш_коммита_к_состоянию_которого_нужно_вернуться>
```

ПРАВИЛО: reset используем только в локальном репозитории! В удаленном можно использовать только revert!