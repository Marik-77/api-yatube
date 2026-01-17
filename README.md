# api_yatube

REST API для социальной сети Yatube. Позволяет управлять постами, комментариями и подписками пользователей.

## Описание проекта

**api_yatube** - это REST API на основе Django Rest Framework для платформы Yatube. API предоставляет полный набор эндпоинтов для работы с постами, группами, комментариями и подписками.

### Основные возможности

- Создание и управление постами
- Добавление комментариев к постам
- Подписка на авторов
- Группировка постов по категориям
- JWT аутентификация

## Требования

- Python 3.9+
- Django 4.0+
- Django Rest Framework 3.14+
- djangorestframework-simplejwt

## Установка и запуск

### 1. Клонирование репозитория

```bash
git clone <repository-url>
cd api-yatube
```

### 2. Создание виртуального окружения

```bash
python -m venv venv
source venv/bin/activate  # для Linux/Mac
# или
venv\Scripts\activate  # для Windows
```

### 3. Установка зависимостей

```bash
pip install -r requirements.txt
```

### 4. Миграции и подготовка БД

```bash
python manage.py migrate
python manage.py createsuperuser
```

### 5. Запуск сервера

```bash
python manage.py runserver
```

API будет доступен по адресу `http://127.0.0.1:8000/api/`

## Примеры запросов и ответов

### Получение списка постов

**Запрос:**
```http
GET /api/v1/posts/ HTTP/1.1
Host: 127.0.0.1:8000
Authorization: Bearer <token>
```

**Ответ:**
```json
{
  "count": 5,
  "next": null,
  "previous": null,
  "results": [
    {
      "id": 1,
      "text": "Мой первый пост",
      "author": "john_doe",
      "group": 1,
      "created": "2024-01-15T10:30:00Z",
      "image": null
    }
  ]
}
```

### Создание поста

**Запрос:**
```http
POST /api/v1/posts/ HTTP/1.1
Host: 127.0.0.1:8000
Authorization: Bearer <token>
Content-Type: application/json

{
  "text": "Новый пост",
  "group": 1
}
```

**Ответ:**
```json
{
  "id": 2,
  "text": "Новый пост",
  "author": "john_doe",
  "group": 1,
  "created": "2024-01-16T14:20:00Z",
  "image": null
}
```

### Добавление комментария

**Запрос:**
```http
POST /api/v1/posts/1/comments/ HTTP/1.1
Host: 127.0.0.1:8000
Authorization: Bearer <token>
Content-Type: application/json

{
  "text": "Отличный пост!"
}
```

**Ответ:**
```json
{
  "id": 1,
  "text": "Отличный пост!",
  "author": "jane_smith",
  "post": 1,
  "created": "2024-01-16T15:45:00Z"
}
```

### Подписка на автора

**Запрос:**
```http
POST /api/v1/follow/ HTTP/1.1
Host: 127.0.0.1:8000
Authorization: Bearer <token>
Content-Type: application/json

{
  "following": "john_doe"
}
```

**Ответ:**
```json
{
  "user": "jane_smith",
  "following": "john_doe",
  "created": "2024-01-16T16:00:00Z"
}
```

## Аутентификация

API использует JWT токены. Для получения токена:

```http
POST /api/v1/jwt/create/ HTTP/1.1
Host: 127.0.0.1:8000
Content-Type: application/json

{
  "username": "john_doe",
  "password": "password123"
}
```

Полученный токен передавайте в заголовке `Authorization: Bearer <token>`

## Об авторе

- Email: marikp20@gmale.com

