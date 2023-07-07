<div align=center>

# [Kittygram](https://kittyyandexhomepc.ddns.net)


![Python](https://img.shields.io/badge/Python-3.9.10-blue)
![Django](https://img.shields.io/badge/Django-3.2.16-blue)
![Django_REST_framework](https://img.shields.io/badge/Django_REST_framework-3.12.4-blue)
![Nginx](https://img.shields.io/badge/Nginx-1.18.0-blue)
![Gunicorn](https://img.shields.io/badge/Gunicorn-20.1.0-blue)
## Учебный проект Замечательные коты

Проект для публикаций фотографий своих любимцев.
В Kittygram предоставлены интерфейсы для регистрации новых и для аутентификации зарегистрированных пользователей.

Аутентифицированным пользователям проект позволяет добавлять новых питомцев на сайт.

Для каждого нового котика нужно указать его имя, год рождения и достижения(выбрать из уже существующих или создать новое), выбрать цвет . Опционально можно загрузить фотографию своего питомца; для котиков без фотографии будет выводиться изображение по умолчанию.
Информацию о собственных котах можно изменить или вовсе удалить с сайта.

На одной странице отображается не более десяти котиков.

## **Описание проекта**

Проект Kittygram находится по адресу: https://kittyyandexhomepc.ddns.net

## **Стэк технологий**

* [Python 3.9](https://www.python.org/downloads/)
* [Django 3.2.3](https://www.djangoproject.com/download/)
* [djangorestframework 3.12.4](https://pypi.org/project/djangorestframework/#files)
* [djoser 2.1.0](https://pypi.org/project/djoser/#files)
* [webcolors 1.11.1](https://pypi.org/project/webcolors/1.11.1/)
* [gunicorn 20.1.0](https://pypi.org/project/gunicorn/20.1.0/)
* [psycopg2-binary 2.9.6](https://pypi.org/project/psycopg2-binary/#files)
* [pytest-django 4.4.0](https://pypi.org/project/pytest-django/)
* [pytest-pythonpath 0.7.3](https://pypi.org/project/pytest-pythonpath/)
* [pytest 6.2.4](https://pypi.org/project/pytest/)
* [PyYAML 6.0](https://pypi.org/project/PyYAML/)
* [python-dotenv 1.0.0](https://pypi.org/project/python-dotenv/)

## Локальный запуск проекта

Клонировать репозиторий и перейти в него в командной строке:

```bash
git clone https://github.com/occamablade/kittygram_final.git
cd kittygram_final
```

Cоздать и активировать виртуальное окружение, установить зависимости:

```bash
python3 -m venv venv && \ 
    source venv/scripts/activate && \
    python -m pip install --upgrade pip && \
    pip install -r backend/requirements.txt
```

Установите [docker compose](https://www.docker.com/) на свой компьютер.

Запустите проект через docker-compose:

```bash
docker compose -f docker-compose.yml up --build -d
```

Выполнить миграции:

```bash
docker compose -f docker-compose.yml exec backend python manage.py migrate
```

Соберите статику и скопируйте ее:

```bash
docker compose -f docker-compose.yml exec backend python manage.py collectstatic  && \
docker compose -f docker-compose.yml exec backend cp -r /app/static_backend/. /backend_static/static/
```

## .env

В корне проекта создайте файл .env и пропишите в него свои данные.

Пример:

```apache
POSTGRES_DB=kittygram
POSTGRES_USER=kittygram_user
POSTGRES_PASSWORD=kittygram_password
DB_NAME=kittygram
```

## Workflow

Для использования Continuous Integration (CI) и Continuous Deployment (CD): в репозитории GitHub Actions `Settings/Secrets/Actions` прописать Secrets - переменные окружения для доступа к сервисам:

```
SECRET_KEY                     # стандартный ключ, который создается при старте проекта

DOCKER_USERNAME                # имя пользователя в DockerHub
DOCKER_PASSWORD                # пароль пользователя в DockerHub
HOST                           # ip_address сервера
USER                           # имя пользователя
SSH_KEY                        # приватный ssh-ключ (cat ~/.ssh/id_rsa)
PASSPHRASE                     # кодовая фраза (пароль) для ssh-ключа

TELEGRAM_TO                    # id телеграм-аккаунта (можно узнать у @userinfobot, команда /start)
TELEGRAM_TOKEN                 # токен бота (получить токен можно у @BotFather, /token, имя бота)
```

При push в ветку main автоматически отрабатывают сценарии:

* *tests* - проверка кода на соответствие стандарту PEP8 и запуск pytest. Дальнейшие шаги выполняются только если push был в ветку main;
* *build\_and\_push\_to\_docker\_hub* - сборка и доставка докер-образов на DockerHub
* *deploy* - автоматический деплой проекта на боевой сервер. Выполняется копирование файлов из DockerHub на сервер;
* *send\_message* - отправка уведомления в Telegram.

<div align=center>

## Контакты

[![Telegram Badge](https://img.shields.io/badge/-vanyshqa-blue?style=social&logo=telegram&link=https://t.me/vanyshqa)](https://t.me/vanyshqa) [![Gmail Badge](https://img.shields.io/badge/-bezborodnikov18@gmail.com-c14438?style=flat&logo=Gmail&logoColor=white&link=mailto:bezborodnikov18@gmail.com)](mailto:bezborodnikov18@gmail.com)

</div>
