## Инициализировать локальный репозиторий
```bash
git init
```
## Проверить состояние
```bash
git status
```
## Проиндексировать изменения для последующего коммита
```bash
git add <название_файла.расширение>
или
git add --all или git add . - проиндексировать сразу все файлы в текущей директории
```

Индекс - это промежуточная зона перед коммтом. В коммит будет внесены только изменения из индекса.

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

В новый коммит запишутся только ПЕРВЫЕ изменения из пункта №1, а вторые изменения из пункта №3 остануться в неиндексированном состоянии. Вот как это выглядит:
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

<br></br>

# Коммиты
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
    4. нашимаешь клавишу "Enter"
```
<br></br>

# СБРОСЫ:

## Сбросить все изменения ДО индексации
```bash
git checkout <имя_файла>
```

## Сбросить все изменения ПОСЛЕ индексации
```bash
git reset HEAD <имя_файла> - отменяет команду add
git checkout  <имя_файла>

или

git restore <имя_файла> - сразу удалает изменения из индекса и рабочего файла
```

