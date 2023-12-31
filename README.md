# Помощник Git и GitHub by Sharp

## Содержание:
1. Инициализация локального репозитория.
2. Добавление файлов, состояние репозитория, коммит, история коммитов.
3. Создание удалённого репозитория на GitHub.
4. SSH. Обеспечение безопасности репозиториев.
5. Синхронизация локального и удалённого репозиториев. Отправление изменений на удалённый репозиторий.
6. Что такое хеш. Хеширование коммитов.
7. Статусы файлов в Git.
---
## 1. Инициализация локального репозитория
   Для того чтобы начать пользоваться локальным репозиторием,  
   нужно:
1. Создать папку, в которой будут храниться нужные файлы.
   Например ваша папка будет находиться в каталоге `~/dev`, создадим её:
   ```bash
   mkdir название_папки
   ```
2. Перейти в папку и инициализировать локальный репозиторий:
   Чтобы перейти в папку воспользуемся данной командой:
   ```bash
   cd название_папки
   ```
   Затем, находясь в данной папке, инициализируем локальный репозиторий командой:
   ```bash
   git init
   ```
В вашей папке появится скрытый каталог `.git` в котором содержится вся служебная информация.

### Если вы инциализировали не ту папку её можно удалить
  Для этого введите данную команду, находясь в папке:
  ```bash
  rm -rf .git
  ```
  Ключ `-rf` позволяет удалить папку рекурсивно(`-r`) и принудительно, т.е. избавит  
  от вопросов *Удалить ли этот файл?*, *Удалить ли эту папку?* и т.п.

## 2. Добавление файлов, состояние репозитория, коммит, история коммитов.
   
### Добавление файлов
   Для того, чтобы подготовить файлы к сохранению, их нужно *добавить*.
   Находясь в папке с локальным репозиторием введите команду:
   ```bash
   git add --all # Добавит все файлы
   ```
   или
   ```bash
   git add имя_файла
   ```

### Состояние репозитория
   Чтобы проверить состояние репозитория можно использовать команду:
   ```bash
   git status
   ```
   Она покажет текущее состояние файлов и репозитория.

### Коммит
   Коммит - сохраняет изменения в истории и при необходимости возвращает старые версии изменений.
   
   Чтобы выполнить коммит выполните следующую команду:
   ```bash
   git commit -m "Сообщение, которое содержит суть изменения"
   ```

### История коммитов
   Для того чтобы посмотреть историю коммитов введите следующую команду:
   ```bash
   git log
   ```

## 3. Создание удалённого репозитория на GitHub.
   Для начала нужно создать аккаунт на платформе [GitHub](https://github.com/)

   Нажмите на иконку справа сверху экрана, перейдите в **Your repositories** и создайте новый репозиторий **New**.
   Введите название репозитория и создайте репозиторий **Create repository**.

## 4. SSH. Обеспечение безопасности репозиториев.
   **SSH** (от англ. *Secure Shell Protocol*) - он обеспечивает безопасный обмен данными в сети.
   
   SSH использует пару ключей для обеспечения безопасности - *публичный* и *приватный*:
   * **Приватный ключ** (англ. *private key*) хранится только на вашем компьютере и не должен передаваться кому-либо ещё.  
   Он используется для расшифровки данных.
   * **Публичный ключ** (англ. *public key*) доступен всем и используется для шифрования данных.  
   Они могут быть расшифрованы парным приватным ключом.

   Чтобы сгенерировать ssh-ключ введите следующую команду:
   ```bash
   ssh-keygen -t ed25519 -C "Эл. почта вашего аккаунт GitHub"
   ```
   или
   ```bash
   ssh-keygen -t rsa -b 4096 -C "Эл. почта вашего аккаунт GitHub"
   ```
   Везде где просят что-то ввести нажмите **Enter**.
   В каталоге `/.ssh` будут храниться ваши ключи. файл с расширением `.pub` хранит публичный ключ, а без расширения приватый.

   Выведите ключ с помощью команды:
   ```bash
   cat название_алгоритма.pub
   ```
   и скопируйте данный ключ.

   Перейдите на GitHub и выберите пункт **Settings**. В левом меню выберите **SSH and GPG keys**.  
   В открывшемся окне нажмите **New SSH key**
   Введите название в поле **Title**, в поле **Key type** выберите **Authentication Key**.
   В поле **Key** вставьте ваш скопированный ключ и нажмите **Add SSH key**

   Чтобы проверить правильность установки ключа введите:
   ```bash
   ssh -T git@github.com
   ```

## 5. Синхронизация локального и удалённого репозиториев. Отправление изменений на удалённый репозиторий.
   Для того, чтобы связать локальный и удалённый репозиторий введите:
   ```bash
   git remote add origin git@github.com:%имя_аккаунта%/имя_проекта.git 
   ```
   
### Отправление изменений на удалённый репозиторий.
   Для того, чтобы отправить изменения на удалённый репозиторий введите:
   ```bash
   git push -u origin main # Если выдаст ошибку введите master вместо main
   ```

   Затем можно посмотреть изменения в репозитории на **GitHub**.

   В дальнейшем при работе флаг `-u` можно опустить и писать `git push`

## 6. Что такое хеш. Хеширование коммитов
   Хеширование (*hash*, "рубить", "крошить") - это способ преобразовать набор данных и получить их "отпечаток"(*fingerprint*)

   Git хеширует информацию о коммите(содержание файлов, ссылка на предыдущий, или родительский(*parent*) коммит) с помощью алгоритма **SHA-1**(*Secure Hash Algorithm*)  
   и получает для каждого коммита свой уникальный хеш.

   Хеш - это основной индентификатор коммита, короткая строка, которая состоит из цифр 0-9 и латинских букв A-F.

   * Если хешировать один и тот же набор данных, результат будет одинаковым.
   * Если данные поменять, то хеш изменится.
   
### Скоращенный лог.
   Чтобы получить сокращенный лог, нужно ввести:
   ```bash
   git log --oneline
   ```
   В терминале выведет несколько символов хеша каждого коммита и их комментарии.
   Сокращенный хеш можно использовать также, как и полный.

### Файл HEAD.
   Файл HEAD - служебный файл в папке `.git`. Он указывает на самый последний коммит.

   Если заглянуть в этот файл, можно увидеть ссылку на другой служебный файл, который хранит хеш служебного коммита.
   ```bash
   $ cat HEAD # команда cat показывает содержимое файла
   ref: refs/heads/master # (main) в файле вот такая ссылка 
   ```
   
## 7. Статусы файлов в Git.
   Одна из задач git - отслеживать изменения файлов в репозитории.
   Для этого существуют следующие статусы файлов:
   * untracked (*"неотслеживаемый"*)
   Так помечаются новый файлы, которые git "видит", но не следит за изменениями.
   * staged (*"подготовленный"*)
   Это файлы, которые попадут в коммит. Командой `git add` файл помещается в staging area(*indexed* или *cached*)
   * tracked (*"отслеживаемый"*)
   В него попадают файлы, которые были зафиксированы с помощью `git commit`, а также файлы, которые были добавлены в **staging area** командой `git add`.
   * modified (*"изменённый"*)
   Данное состояние означает, что файл был изменён.

   ```mermaid
   flowchart TD
    a["untracked
    (неотслеживаемый)"] -- git add --> b["staged
    (в списке на коммит)
    + tracked"]
    b & d -- Изменения --> c["modified
    (изменённый)"]
    c -- git add --> b
    b -- git commit --> d["tracked
    (отслеживаемый)"]
   ```


