# Проект «Infra_sp2»

### Описание

   Проект «Infra_sp2» собирает отзывы пользователей на произведения.  
   Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.<br/>    
   Каждый ресурс описан в документации: указаны эндпоинты (адреса, по которым можно сделать запрос),    
разрешённые типы запросов, права доступа и дополнительные параметры, когда это необходимо.<br/>    
   Добавлять произведения, категории и жанры может только администратор.<br/>    
   Благодарные или возмущённые пользователи оставляют к произведениям текстовые отзывы  
и ставят произведению оценку в диапазоне от одного до десяти (целое число);  
из пользовательских оценок формируется усреднённая оценка произведения — рейтинг (целое число).<br/>  
   Добавлять отзывы, комментарии и ставить оценки могут только аутентифицированные пользователи.<br/>    

### Технологии:
![Python](https://img.shields.io/badge/Python-FFD43B?style=for-the-badge&logo=python&logoColor=blue)
![Django](https://img.shields.io/badge/Django-092E20?style=for-the-badge&logo=django&logoColor=green)
![DRF](https://img.shields.io/badge/django%20rest-ff1709?style=for-the-badge&logo=django&logoColor=white)
![JWT](https://img.shields.io/badge/JWT-000000?style=for-the-badge&logo=JSON%20web%20tokens&logoColor=white)

### Используемые пакеты:
    * requests==2.26.0
    * asgiref==3.2.10
    * Django==2.2.16
    * django-filter==2.4.0
    * djangorestframework==3.12.4
    * djangorestframework-simplejwt==4.8.0
    * gunicorn==20.0.4
    * psycopg2-binary==2.8.6
    * PyJWT==2.1.0
    * pytz==2020.1
    * sqlparse==0.3.1
    * pytest==6.2.4
    * pytest-django==4.4.0
    * pytest-pythonpath==0.7.3
    * python-dotenv==0.21.1


### Установка

1. Клонировать репозиторий:

   ```
   git clone ...
   ```

2. Перейти в папку с проектом:

   ```
   cd infra
   ```

3. Развернуть докер контэйнеры:

   ```
   docker-compose up
   ```

4. Выполнить миграции, создать суперпользователя и собрать статику

   ```
     docker-compose exec web python manage.py makemigrations
     docker-compose exec web python manage.py migrate
     docker-compose exec web python manage.py createsuperuser
     docker-compose exec web python manage.py collectstatic --no-input
   ```

### Дополнительно

* Клонирование базы. В катологе static/data проекта находятся тестовые файлы базы данных. 
  Для их импорта в базу данных выполняется команда:
   ```
   python manage.py import_db
   ```
* Каждый ресурс описан в документации проекта:
   ```
   http://127.0.0.1:8000/redoc/
   ```

* ПО для тестирования API:
   ```
   https://www.postman.com/
   ```

### Примеры запросов

* Пример POST-запроса<br/>   
    Регистрация нового пользователя и получение `confirmation_code`. Доступно без токена.  
    `POST http://127.0.0.1:8000/api/v1/auth/signup/`
    ```json
    {
        "email": "user@example.com",
        "username": "string"
    }
    ```
* Пример ответа:
    ```json
    {
        "email": "string",
        "username": "string"
    }
    ```
  В проекте настроен filebased способ отправки почты, confirmation_code будет находится в папке send_email базовой директории.
* Получение JWT-токена в обмен на `username` и `confirmation_code`. Доступно без токена.  
    `POST http://127.0.0.1:8000/api/v1/auth/token/`
    ```json
    {
        "username": "string",
        "confirmation_code": "string"
    }
    ```
* Пример ответа:
    ```json
    {
        "token": "string"
    }
    ```
  В дальнейшем token передаётся в Header: Bearer
* Создание отзыва к произведению. Необходим токен.  
    `POST http://127.0.0.1:8000/api/v1/titles/{title_id}/reviews/`
    ```json
    {
        "text": "string",
        "score": 1
    }
    ```
* Пример ответа:
    ```json
    {
        "id": 0,
        "text": "string",
        "author": "string",
        "score": 1,
        "pub_date": "2019-08-24T14:15:22Z"
    }
    ```

### Автор проекта
* Артем Вахрушев  
  
