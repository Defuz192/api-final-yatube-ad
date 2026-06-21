# api_final

API для социальной сети Yatube. Позволяет публиковать посты, оставлять комментарии, подписываться на авторов и объединяться в тематические группы.

## Возможности

- Публикация, редактирование и удаление постов
- Комментирование постов
- Подписка на пользователей
- Сообщества (группы)
- JWT-аутентификация

## Стек

- Python 3.x
- Django 3.2
- Django REST Framework
- Simple JWT

## Установка

1. Клонируйте репозиторий:

   git clone <url-репозитория>
   cd yatube_api

2. Создайте и активируйте виртуальное окружение:

   python -m venv venv
   source venv/Scripts/activate  # Windows
   source venv/bin/activate      # Linux/Mac

3. Установите зависимости:

   pip install -r requirements.txt
   

4. Выполните миграции:
   
   python manage.py migrate
   

5. Запустите сервер:
   
   python manage.py runserver
   

## Документация API

После запуска сервера документация доступна по адресу:  
http://127.0.0.1:8000/redoc/

## Примеры запросов

### Получить JWT-токен


POST /api/v1/jwt/create/
Content-Type: application/json

{
  "username": "user1",
  "password": "pass123"
}


Ответ:

{
  "refresh": "string",
  "access": "string"
}


### Список постов


GET /api/v1/posts/


### Создать пост (требуется авторизация)


POST /api/v1/posts/
Authorization: Bearer <access_token>
Content-Type: application/json

{
  "text": "Мой первый пост",
  "group": 1
}


### Подписаться на пользователя


POST /api/v1/follow/
Authorization: Bearer <access_token>
Content-Type: application/json

{
  "following": "username"
}


## Права доступа

- Неавторизованные пользователи — только чтение
- Авторизованные — создание, редактирование и удаление своего контента
- Подписки — только для авторизованных