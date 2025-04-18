[![Main Kittygram Workflow](https://github.com/LinarAl/kittygram_final/actions/workflows/main.yml/badge.svg)](https://github.com/LinarAl/kittygram_final/actions/workflows/main.yml)
# Проект Kittygram.
Kittygram - сервис для публикации данных о котиках. Чтобы посмотреть или выложить данные, необходимо: зарегестрироваться и нажать на кнопу добавить кота, загрузить фото, указать его имя и год рождения. Также можно добавить досижение котику.

Kittygram - это одностраничное приложение.
## Стек использованных технологий
#### Frontend - JavaScript, HTML, CSS, React.
#### Backend - python 3.9, Django, PostgreSQL, REST API, Gunicorn, Nginx, Docker, Docker-Compose, Git, GitHub Actions.

# Как развернуть проект
1. Установить Docker.
2. Создать папку для проекта c файлами.
3. Выполнить команды в терминале.

## 1. Установить Docker.
### Установка Docker на Windows 10-11
1. Для запуска проекта неоходимо установить Windows Subsystem for Linux [инструкция с официального сайта Microsoft](https://docs.microsoft.com/ru-ru/windows/wsl/install-win10).
2. Скачайте и установите [Docker](https://www.docker.com/products/docker-desktop/).
3. Запустите Docker Desctop.

Для работы с докером можно будет использовать любой доступный терминал рекомендуeтся работать в [Git Bash](https://git-scm.com/downloads/win).

### Установка Docker на Windows 8 и более старых версий:
1. Скачайте и установите программу для работы с виртуальными машинами, например [VirtualBox](https://www.virtualbox.org/wiki/Downloads).
2. Скачайте образ [Ubuntu](https://ubuntu.com/download/desktop).
3. Установите Ubuntu на виртуальную машину.
4. В виртуальную машину установите Docker по инструкции для Linux.

### Установка Docker на Linux
Первый способ установить Docker на Linux — скачать и выполнить [официальный скрипт](https://docs.docker.com/engine/install/ubuntu/#install-using-the-convenience-script) :
1. Скачайте и установите curl:
    ```
    sudo apt update
    sudo apt install curl
    ```
2. Скачайте скрипт для установки докера с официального сайта:
    ```
    curl -fSL https://get.docker.com -o get-docker.sh 
    ```
3. Запустите сохранённый скрипт с правами суперпользователя:
    ```
    sudo sh ./get-docker.sh
    ```
Второй способ установить Docker вручную: [официальная документации Docker](https://docs.docker.com/engine/install/ubuntu/).

4. Установите утилиту Docker Compose:
    ```
    sudo apt install docker-compose-plugin 
    ```

### Установка Docker на macOS
Зайдите [на официальный сайт проекта](https://www.docker.com/products/docker-desktop) и скачайте установочный файл Docker Desktop для вашей платформы — Apple Chip для процессоров M1/M2 и Intel Chip для процессоров Intel.

Откройте скачанный DMG-файл и перетащите Docker в Applications, а потом — запустите программу Docker.

## 2. Создать папку для проекта c файлами.
1. Создать директорию для проекта.
2. Скачать в папку проекта файл `docker-compose.production.yml` из репозитория.
3. Создать файл .env в папке с проектом. Пример файла .env:
    ```
    DEBUG=True
    ALLOWED_HOSTS='localhost 127.0.0.1'
    POSTGRES_USER=user
    POSTGRES_PASSWORD=password
    POSTGRES_DB=django_db
    DB_HOST=db
    DB_PORT=5432
    ```
3. Выполнить команды запуска Docker-Compose в терминале.
 
    Находясь в директории проекта с файлом `docker-compose.production.yml` запустите Docker Compose:
    
    В теминале из под **Windows**:
    ```
    docker compose -f docker-compose.production.yml pull
    docker compose -f docker-compose.production.yml up
    ```
    Откройте второе окно терминала и выполните миграции, собирите статику:   
    ```
    docker compose -f docker-compose.production.yml exec backend python manage.py migrate

    docker compose -f docker-compose.production.yml exec backend python manage.py collectstatic
    
    docker compose -f docker-compose.production.yml exec backend cp -r /app/static/. /static/static/
    ```
    В теминале из под **Linux**:
    
    ```
    sudo docker compose -f docker-compose.production.yml pull
    
    sudo docker compose -f docker-compose.production.yml up -d
    
    sudo docker compose -f docker-compose.production.yml exec backend python manage.py migrate

    sudo docker compose -f docker-compose.production.yml exec backend python manage.py collectstatic
    
    sudo docker compose -f docker-compose.production.yml exec backend cp -r /app/static/. /static/static/
    ```
    **Остановить контейнеры** в Docker Compose
    ```
    # Linux
    sudo docker compose -f docker-compose.production.yml stop
    # Windows
    docker compose -f docker-compose.production.yml stop
    ```

    ## Автор Проекта    
    [Линар А.](https://github.com/LinarAl)