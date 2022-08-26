# `Foodgram` - сайт 'Продуктовый помощник'

![foodgram-project-react workflow](https://github.com/SergeyViskov/foodgram-project-react/actions/workflows/foodgram_workflow.yml/badge.svg?)

### О проекте:
 Онлайн-сервис и API для него. На этом сервисе пользователи могут публиковать рецепты, подписываться на публикации других пользователей, добавлять понравившиеся рецепты в список «Избранное», а перед походом в магазин скачивать сводный список продуктов, необходимых для приготовления одного или нескольких выбранных блюд.
 
### Технологии:
```
- Python
- Django
- Django REST Framework
- PostgreSQL
- Nginx
- Gunicorn
- Docker
```
### Как запустить проект:

* Выполните вход на свой удаленный сервер

* Установите docker на сервер:
```
sudo apt install docker.io 
```
* Установите docker-compose на сервер:
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
* Cоздайте .env файл и впишите:
    ```
    DB_ENGINE=<django.db.backends.postgresql>
    POSTGRES_DB=<имя базы данных postgres>
    POSTGRES_USER=<пользователь бд>
    POSTGRES_PASSWORD=<пароль>
    DB_HOST=<db>
    DB_PORT=<5432>
    SECRET_KEY=<секретный ключ проекта django>
    ```
* Для работы с Workflow добавьте в Secrets GitHub переменные окружения для работы:
    ```
    DB_ENGINE=<django.db.backends.postgresql>
    POSTGRES_DB=<имя базы данных postgres>
    POSTGRES_USER=<пользователь бд>
    POSTGRES_PASSWORD=<пароль>
    DB_HOST=<db>
    DB_PORT=<5432>
    
    DOCKER_PASSWORD=<пароль от DockerHub>
    DOCKER_USERNAME=<имя пользователя>
    
    SECRET_KEY=<секретный ключ проекта django>
    USER=<username для подключения к серверу>
    HOST=<IP сервера>
    PASSPHRASE=<пароль для сервера, если он установлен>
    SSH_KEY=<ваш SSH ключ (для получения команда: cat ~/.ssh/id_rsa)>
    TELEGRAM_TO=<ID чата, в который придет сообщение>
    TELEGRAM_TOKEN=<токен вашего бота>
    ```
*Workflow состоит из трёх шагов:
    ```
     - Проверка кода на соответствие PEP8
     - Сборка и публикация образа бекенда на DockerHub.
     - Автоматический деплой на удаленный сервер.
     - Отправка уведомления в телеграм-чат.  
    ```
* Запуск контейнера:
```
docker-compose up -d --build
```
* После успешной сборки на сервере выполните команды:
- Соберите статические файлы:
```
sudo docker-compose exec backend python manage.py collectstatic --no-input
```
- Примените миграции:
```
sudo docker-compose exec backend python manage.py makemigrations --noinput

sudo docker-compose exec backend python manage.py migrate --noinput

sudo docker-compose exec backend python manage.py createsuperuser
```
- Загрузите БД:
```
sudo docker-compose exec backend python manage.py load_json_data
```
или
```
sudo docker-compose exec backend python manage.py load_csv_data
```

* Докуметация API:

http://51.250.100.101/api/docs/redoc.html

* Проект:

http://51.250.100.101

* Суперпользователь:

`name: admin@admin.ru`

`password: admin`

### Об авторе:

Висков Сергей Николаевич

Ученик Яндекс-практикума, когорта №9 +