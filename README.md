# Проект YaMDb
Проект YaMDb собирает отзывы (Review) пользователей на произведения (Title). Произведения делятся на категории: "Книги", "Фильмы", "Музыка". Список категорий (Category) может быть расширен.
Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.
В каждой категории есть произведения: книги, фильмы или музыка. Например, в категории "Книги" могут быть произведения "Винни Пух и все-все-все" и "Марсианские хроники", а в категории "Музыка" — песня "Давеча" группы "Насекомые" и вторая сюита Баха. Произведению может быть присвоен жанр из списка предустановленных (например, "Сказка", "Рок" или "Артхаус"). Новые жанры может создавать только администратор.
Благодарные или возмущённые читатели оставляют к произведениям текстовые отзывы (Review) и выставляют произведению рейтинг.

## Примеры запросов
Регистрация нового пользователя:
POST api/v1/auth/signup/

Получение JWT-токена:
POST api/v1/auth/token/

Получение списка всех категорий:
GET api/v1/categories/

Удаление жанра:
DELETE api/v1/genres/{slug}/

Частичное обновление информации о произведении:
PATCH /api/v1/titles/{titles_id}

Получение списка всех отзывов:
GET /api/v1/titles/{title_id}/reviews/

Добавление комментария к отзыву:
POST /api/v1/titles/{title_id}/reviews/{review_id}/comments/

## Установка

Склонируйте репозитрий на свой компьютер.

Заполните шаблон infra/.env.template

Выполните копирование файла командой:
cp infra/.env.template infra/.env 

Из папки infra/ соберите образ при помощи docker compose
docker compose up -d --build

Примените миграции
docker compose exec web python manage.py migrate

Соберите статику
docker compose exec web python manage.py collectstatic --no-input

Для доступа к админке не забудьте создать суперюзера
docker compose exec web python manage.py createsuperuser

Заполнение базы данными
docker compose exec web python manage.py loaddata fixtures.json 

## Деплой на удаленный сервер
Для запуска проекта на удаленном сервере необходимо:

скопировать на сервер файлы docker-compose.yaml, .env и папку nginx командами:

scp docker-compose.yaml  <user>@<server-ip>:
scp .env <user>@<server-ip>:
scp -r nginx/ <user>@<server-ip>:

создать переменные окружения в разделе secrets настроек текущего репозитория:

DOCKER_PASSWORD # Пароль от Docker Hub
DOCKER_USERNAME # Логин от Docker Hub
HOST # Публичный ip адрес сервера
USER # Пользователь зарегистрированный на сервере
PASSPHRASE # Если ssh-ключ защищен фразой-паролем
SSH_KEY # Приватный ssh-ключ
TELEGRAM_TO # ID телеграм-аккаунта
TELEGRAM_TOKEN # Токен бота

### После каждого обновления репозитория (git push) будет происходить:

Проверка кода на соответствие стандарту PEP8 (с помощью пакета flake8) и запуск pytest из репозитория yamdb_final
Сборка и доставка докер-образов на Docker Hub.
Автоматический деплой.
Отправка уведомления в Telegram.

![example workflow](https://github.com/ValentinGorovenko/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

## Авторы
Данилова Марина - https://github.com/maridana

Личинин Виталий - https://github.com/Lichinin

Горовенко Валентин - https://github.com/ValentinGorovenko
