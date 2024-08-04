- Навигация консоли
    1. `pwd` - выведет путь к папке, в которой вы сейчас находитесь.
    2. `cd` - сменить директорию
    3. `ls` - вывести содержимое директории ( просмотр папки)
    4. `ls -a` - расширенный список (скрытые файлы)
    5. `..` - родительская директория
    6. `cd ..` — перейди на уровень выше, в родительскую папку
    7. `.` - текущая директория
    8. `cd ~` — перейди в домашнюю директорию (/Users/Username)
    9. `~` -  домашняя директория
    10. `cd /` — перейди в корневую директорию
    11. `touch` - создание файла (расширение заполняется вручную `$ touch my-new-file.txt *# создали файл my-new-file.txt`), можно через пробел создавать несколько файлов*
    12. `mkdir` - создание директории (папки)
    13. `mkdir` `-p` - создание структуры директорий (папки в папках)
    14. `cp` - копирование файлов `$ cp что_копируем куда_копируем`
    15. `mv` - перемещение папок,  `$ mv table.csv ./very-important-files` *сначала указываем имя файла, который хотим переместить, потом путь — куда перемещаем*
    16. `cat` - чтение файлов (просмотр содержимого)
    17. `rm` - удалить файл
    18. `rmdir` - удалить папку (пустую)
    19. `rm -r` - удаляет рекурсивно (папки в которой есть файлы)
    20. `&&` - выполняет несколько команд
    21. `↑` и `↓` - история команд
    22. `Tab` - автозаполнение команд
- Настройка GIT
    1. `git version` - проверка версии git
    2. `git config` - конфигурация
    3. `git config --global` - глобальная конфигурация
    4. `git config --global [user.name](http://user.name/)` `"User Namovich”` - настройка имени
    5. `git config --list` - показать настройки конфигурации
    6. `cat ~/.gitconfig` - просмотр файла конфигурации
- Последовательность работы с Git
    1. `git status` - просмотр статуса
    2. `git init` - инициализация папки
    3. `git add`  readme.md - добавление документа
    4. `git commit` -m “Сообщение” - фиксирование изменения файла
    5. `git remote add origin` [git@github.com](mailto:git@github.com):AlexMesherjakov/Practical-work-No.-1..git - связь локального и удаленного репозитория
    6. `git remote -v` - просмотр связи локального и удаленного
    7. `git push` -u origin main - отправить изменения на удаленный репозиторий
    - Статусы файлов в Git
        
        ### Статусы `untracked`/`tracked`, `staged` и `modified`
        
        Одна из ключевых задач Git — отслеживать изменения файлов в репозитории. Для этого каждый файл помечается каким-либо статусом. Рассмотрим основные.
        
        - **`untracked`** (англ. «неотслеживаемый»)
        Мы говорили, что новые файлы в Git-репозитории помечаются как `untracked`, то есть неотслеживаемые. Git «видит», что такой файл существует, но не следит за изменениями в нём. У `untracked`файла нет предыдущих версий, зафиксированных в коммитах или через команду `git add`.
        - **`staged`** (англ. «подготовленный»)
            
            После выполнения команды `git add` файл попадает в **staging area** (от англ. *stage* — «сцена», «этап [процесса]» и *area* — «область»), то есть в список файлов, которые войдут в коммит. В этот момент файл находится в состоянии `staged`.
            
            В одном из предыдущих уроков мы сравнили коммит с фотографией. Можно развить эту аналогию и сказать, что команда `git add` добавляет персонажей (текущее содержимое файла или нескольких файлов) на **сцену** (англ. *stage*) для общей фотографии, а `git commit` делает снимок всей сцены целиком.
            
            <aside>
            💡  **Staging area, index и cache**
            Staging area также называют **index** (англ. «каталог») или **cache** (англ. «кеш»), а состояние файла `staged` иногда называют `indexed` или `cached`.
            
            Все три варианта могут встречаться в документации и в качестве флагов команд Git. А также в интернете — например, в вопросах и ответах [на сайте Stack Overflow](https://stackoverflow.com/).
            
            </aside>
            
        - **`tracked`** (англ. «отслеживаемый»)
        Состояние `tracked` — это противоположность `untracked`. Оно довольно широкое по смыслу: в него попадают файлы, которые уже были зафиксированы с помощью `git commit`, а также файлы, которые были добавлены в staging area командой `git add`. То есть все файлы, в которых Git так или иначе отслеживает изменения.
        - **`modified`** (англ. «изменённый»)
        Состояние `modified` означает, что Git сравнил содержимое файла с последней сохранённой версией и нашёл отличия. Например, файл был закоммичен и после этого изменён.
        
        <aside>
        💡 Для файлов в состояниях `staged` и `modified` обычно не указывают, что они также `tracked`, потому что это состояние подразумевается.
        
        </aside>
        
        ### Про `staged` и `modified`
        
        Команда `git add` добавляет в staging area только текущее содержимое файла. Если вы, например, сделаете `git add file.txt`, а затем измените `file.txt`, то новое содержимое файла не будет находиться в staging.
        
        Git сообщит об этом с помощью статуса `modified`: файл изменён относительно той версии, которая уже в staging. Чтобы добавить в staging последнюю версию, нужно выполнить `git add file.txt` ещё раз.
        
        ### Типичный жизненный цикл файла в Git
        
        Может показаться, что файлы в репозитории попадают в разные состояния хаотично. На практике это не так, и у большинства файлов вполне предсказуемый путь.
        
        !https://pictures.s3.yandex.net/resources/M2_T5_1686651284.png
        
        1. Файл только что создали. Git ещё не отслеживает содержимое этого файла. Состояние: `untracked`.
        2. Файл добавили в staging area с помощью `git add`. Состояние: `staged` (+ `tracked`).
            - Возможно, изменили файл ещё раз. Состояния: `staged`, `modified` (+ `tracked`).
            Обратите внимание: `staged` и `modified` у одного файла, но у разных его версий.
            - Ещё раз выполнили `git add`. Состояние: `staged` (+ `tracked`).
        3. Сделали коммит с помощью `git commit`. Состояние: `tracked`.
        4. Изменили файл. Состояние: `modified` (+ `tracked`).
        5. Снова добавили в staging area с помощью `git add`. Состояния: `staged` (+ `tracked`).
        6. Сделали коммит. Состояния: `tracked`.
        7. Повторили пункты 4−7 много-много раз.
        
        ---
        
        Важное:
        
        - Статусом `untracked` помечается файл, о существовании которого Git знает, но не следит за изменениями в нём. Этот статус — противоположность `tracked`, в который попадают все файлы, отслеживаемые Git.
        - Файл переходит в статус `staged` после выполнения `git add`.
        - Статус `modified` означает, что файл был изменён.
        - Большинство файлов в проектах «шагает» по следующему циклу: «изменён» → «добавлен в список на коммит» → «закоммичен» → «изменён» → и так далее.
        
        ---
        
        `git status` показывает только следующие состояния файлов:
        
        - `staged` (`Changes to be committed` в выводе `git status`);
        - `modified` (`Changes not staged for commit`);
        - `untracked` (`Untracked files`).

        ```mermaid
        graph LR;
        untracked -- "git add" --> staged;
        staged    -- "git commit"     --> tracked/comitted;
        tracked/comitted    -- "Изменения"  --> modified;
        staged    -- "Изменения"  --> modified;
        modified -- "git add" --> staged;
        ```

- Навигация по коммитам
    1. `git log` - история коммитов (тут можно посмотреть хеш коммита)
    2. **`git log --oneline`** - сокращенный лог (сокращенный хеш + коммент коммита)
    - Просмотр файла HEAD
        1. `cd .git/` - зайти в папку git
        2. `ls` - посмотреть, какие файлы есть `.git` 
        3. `cat HEAD` - просмотреть содержимое папки `HEAD`
        4. `cat` `refs/heads/master` - *взяли ссылку из файла HEAD*
        5. `git log` - с*веряем с хешем последнего коммита*
        
        При работе с Git указатель `HEAD` используется довольно часто. Мы уже упоминали, что многие команды Git принимают в качестве параметра хеш коммита. Если нужно передать последний коммит, то вместо его хеша можно просто написать слово `HEAD` — Git поймёт, что вы имели в виду последний коммит.
        
        • Вместо хеша последнего коммита можно написать слово `HEAD` — Git вас поймёт.