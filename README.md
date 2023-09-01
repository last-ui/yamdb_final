**[Server address](http://51.250.67.63/redoc/)**

![workflow](https://github.com/last-ui/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)


<h1 align="center"> Проект YaMDb </h1>
<h3 align="center">Отзывы пользователей на фильмы, музыку и книги</h3>

___
<h4>Авторы:</h4>

**Изимов Арсений**  - тимлид, студент Яндекс.Практикума Когорта 17+
https://github.com/Arseny13

**Сластухин Александр** - студент Яндекс.Практикума Когорта 17+
https://github.com/last-ui

**Зайцев Иван** - студент Яндекс.Практикума Когорта 17+
https://github.com/IvanZaycev0717

<h2>Описание проекта</h2>

Проект хранит отзывы пользователей на фильмы, музыку и книги. Пользователи могут оставлять отзывы и ставить оценку в диапазоне от одного до десяти, по результатам которых формируется рейтинг.

<h2>Алгоритм регистрации пользователей</h2>

Регистрация пользователей происходит через направление пользователем POST-запроса на добавление нового пользователя с параметрами email и username на эндпоинт /api/v1/auth/signup/. Проект отправляет письмо с кодом подтверждения на адрес электронной почты, после чего пользователь отправляет POST-запрос с параметрами username и кодом подтверждения на на эндпоинт /api/v1/auth/token/, в ответе на запрос ему приходит JWT-токен. В результате пользователь получает токен и может работать с API проекта, отправляя этот токен с каждым запросом. Пользователь может отправить PATCH-запрос на эндпоинт /api/v1/users/me/ для заполнения своего профайла.

<h2>Ресурсы API YaMDb</h2>

- Ресурс **AUTH**: аутентификация.

- Ресурс **USERS**: пользователи.

- Ресурс **TITLES**: произведения, к которым пишут отзывы (определённый фильм, книга или песенка).

- Ресурс **CATEGORIES**: категории (типы) произведений («Фильмы», «Книги», «Музыка»).

- Ресурс **GENRES**: жанры произведений. Одно произведение может быть привязано к нескольким жанрам.

- Ресурс **REVIEWS**: отзывы на произведения. Отзыв привязан к определённому произведению.

- Ресурс **COMMENTS**: комментарии к отзывам. Комментарий привязан к определённому отзыву.

<h2>Установка проекта на OS Windows</h2>

**1. Клонировать репозиторий, создать и активировать виртуальное окружение:**

_git clone https://github.com/Arseny13/api_yamdb.git_

_cd api_yatube_

_python -m venv venv_

_source venv/Scripts/activate_



**2. Установить зависимости из файла requirements.txt:**

_pip install -r requirements.txt_

**3. Перейти в папку с manage.py и выполнить миграции:**

_cd api_yatube_

_python manage.py makemigrations_

_python manage.py migrate_

**4. Создать сепурпользователя и запустить проект:**

_python manage.py createsuperuser_

_python manage.py runserver_

<h2>Техническая документация</h2>

Для того чтобы получить, описанные понятным языком эндпоинты и настройки, да ещё с примерами запросов, да ещё с образцами ответов! Читай ReDoc, документация в этом формате доступна по ссылке:

_http://127.0.0.1:8000/redoc/_

<h2>Как работать с API проекта YaMDb</h2>

**1. Вначале надо пользователю надо зарегистрироваться**

POST localhost:8000/api/v1/signup/
Content-Type: application/json

{
  "username": "name_of_user",
  "email": "name@yamdb.ru"
}


**2. На указанную почту придет письмо с кодом подтверждения**

**3. Пользователь отправляет POST-запрос с параметрами username и confirmation_code на эндпоинт /api/v1/auth/token/, в ответе на запрос ему приходит JWT-токен.**

*Пример такого запроса:*

POST localhost:8000/api/v1/auth/token/
Content-Type: application/json

{
  "username": "example_user",
  "password": "123456"
}

*Пример ответ от сервера:*

"token: eyJ0eXAiOiJKV1Q..."

**4. Если вы хотите добавить отзыв:**

POST http://localhost:8000/api/v1/titles/{title_id}/reviews/
Content-Type: application/json
Authorization: Bearer "eyJ0eXAiOi..."

{
    "text": "Мой отзыв",
    "score": 1
}

<h2>Используемые технологии</h2>

- Python 3.7.9
- requests 2.26.0
- Django 3.2
- djangorestframework 3.12.4
- PyJWT 2.1.0
- pytest 6.2.4
- pytest-django 4.4.0
- pytest-pythonpath 0.7.3
- django-filter 2.4.0
- python-dotenv 0.21.0
