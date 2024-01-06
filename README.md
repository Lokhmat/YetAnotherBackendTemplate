# FastAPI+PostgreSQL+NGINX docker template
(Русская версия ниже)

Hello!
This is a working template of a backend server on FastAPI with a PostgreSQL database. Pretty much everything is already set up and ready to use.

What it can do:
-
- Backend FastAPI with a ready-made file structure. Add your routers and you can start writing your business logic immediately.
- Configured proxy balancer in the form of NGINX. All requests on port 80 will be accepted by it and forwarded to your backend.
- PostgreSQL 14.10 version database. To interact with the database from the backend, SQL Alchemy _non_-ORM models are used. *Why:* It seems that the code becomes cleaner, and it's more convenient to write complex SQL transactions in SQL than through ORM.
- The database saves data after restart, so you can safely stop your container.
- Migrations using yandex-pgmigrate for even more pure SQL!
- Logging set up in the backend using the logging package.
- Everything is containerized for your convenience and wrapped in one startup script.

To launch:
-
1. Clone the repository.
2. Fill in the .env file. An example is provided in env-example.txt.
3. Install Python, Docker, and dependencies from app/requirements.txt.
4. Run startup.sh.
5. Make sure everything has started up 🙂

What can be improved:
-
- Currently, the server and balancer workstreams are set up quite incorrectly.
- SQLAlchemy is used as the database driver - by default, it is not asynchronous. It has an asynchronous engine, so there is an opportunity to make it asynchronous.

**Possible FAQs:**
-
1. How to add a migration?
Write it in a new file under database/migrations. Important: the name should match the pattern: `V{XX}__{name}.sql
Where:
    - XX - the version of your migration
    - name - its name

    After that, you can update your models. Changes will be automatically applied after restarting the container.

This section can be updated as the repository evolves.

--------------
Привет!
Это рабочий теплейт бекенд сервера на FastAPI с базой данных PostgreSQL. Тут уже все настроено и можно пользоваться

**Что он умеет:**
-
- Бекенд FastApi с готовой файловой структурой. Добавляйте ваши роутеры и можно сразу писать бизнес логику
- Настроенный прокси балансер в виде NGINX. Все запросы на 80 порту будет принимать сразу он и пробрасывает запросы до вашего бека
- База PostgreSQL 14.10 версии. Для работы с базой из бека используется SQL алхимия **не** ORM модели. *Почему:* Кажется код так получается чище, а сложные SQL транзакции писать удобнее на самом SQL а не через ORM.
- База сохраняет данные после перезапуска так что можете смело стопать ваш контейнер
- Миграции с помощью yandex-pgmigrate для еще большего количества чистого SQL!
- Настроено логирование из бекенда с помощью logging пакета
- Все контейнеризовано для вашего удобства и обернуто в один стартовый скрипт

**Для запуска:**
-
1. Склонировать репозиторий
2. Заполнить .env файл. Пример есть в env-example.txt
3. Установить Python, Docker и зависимости из app/requirements.txt
4. Запустить startup.sh
5. Убедиться что все запустилось :)

**Что можно улучшить:**
-
- Пока что абсолютно неграмотно настроены потоки работы сервера и балансера
- В качестве драйвера для работы с базой использована SQLAlchemy - по дефолту она **не** асинхронна. У нее есть асинхронный движок, так что существует возможность перевезти ее на асинхронщину.

**Возможные вопросы:**
-
1. Как добавить миграцию?
Написать ее в новый файл database/migrations. **Важно:** название должно отвечать паттерну ```V{XX}__{name}.sql```
Где:
    - XX - версия вашей миграции
    - name - ее название
    После этого можно обновлять ваши модели. Изменения автоматически подтянуться после перезапуска контейнера

Этот раздел может обновляться по ходу жизни репозитория 
