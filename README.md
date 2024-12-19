# Проект Kittygram

![Collaboration Badge](https://img.shields.io/badge/Collaborator-https://github.com/EugeneSal-blue) 

### Описание проекта
Kittygram — это веб-приложение, которое позволяет пользователям коратко рассказать о своих усатых питомцах с помощью фото и кошачих достижений. Проект предоставляет удобный интерфейс для отражения самых запоминающихся моментах, проведённых со своим хвостатым другом.

### Функциональность
- Создание и редактирование профелей своих пушыстых друзей.
- Загрузка изображенй и достижений.

### Автор https://github.com/evi1ghost

### Стек технологий 
- **Django** — основной фреймворк для backend.
- **PostgreSQL** — база данных для хранения данных.
- **Node.js** — основной фреймворк для frontend.
- **Nginx** — для обслуживания статических файлов.
- **Docker** — для контейнеризации приложения.

## Как развернуть проект
### Для локального развёртывания:
Пример всех команд приведён в ***bash sell***
1. Форкните репозиторий
2. Клонируйте репозиторий любым удобным способом, например
```bash
git clone https://github.com/yourusername/kittygram_final.git
# yourusername - имя вашего аккаунта на GitHub
```
3. Перейдите в директорию с клонированым репозиторием
```bash
cd kittygram_final
```
4. Создайте любым удобным для вас способом, а затем заполните ```.env``` :
```nano
SECRET_KEY='your-secret-key'
DEBUG=True
ALLOWED_HOSTS=localhost 127.0.0.1 domain.name
POSTGRES_DB=kittygram
POSTGRES_USER=user
POSTGRES_PASSWORD=assword
DB_NAME=kittygram
DB_HOST=db
DB_PORT=5432
```
- `SECRET_KEY` — секретный ключ для Django.
- `DEBUG` — указывает, включен ли режим отладки.
- `ALLOWED_HOSTS` — список разрешенных хостов.
- `POSTGRES_DB`, `POSTGRES_USER`, `POSTGRES_PASSWORD` — параметры для подключения к PostgreSQL.
- `DB_HOST`, `DB_PORT` — хост и порт базы данных.

Создать и открыть для заполнения .env можно командой:
```bash
nano .env
```

**Windows 10/11**
1. Установите WSL любым удобным способом.
2. Установите Docker Desktop и запустите его.
3. Из директории с клонированным репозиторием в терминале перейдите в оболочку WSL командой
```bash
wsl
```
4. Запустите проект выполнив команду:
```bash
sudo docker-compose -f docker-compose.production.yml up -d
```
- ```-f docker-compose.production.yml``` указывает использовать файл docker-compose.production.yml.
- ```-d``` запускает контейнеры в фоновом режиме(может отсутствовать).

5. Собирерите статику и примените миграции БД:
```bash
sudo docker compose -f docker-compose.production.yml exec backend python manage.py migrate
sudo docker compose -f docker-compose.production.yml exec backend python manage.py collectstatic
sudo docker compose -f docker-compose.production.yml exec backend cp -r /app/collected_static/. /static/static/
```
Поздравляем, проект развёрнут!!!

Для остановки контейнеров используйте:
```bash
docker-compose -f docker-compose.production.yml down
```
Для запуска:
```bash
docker-compose -f docker-compose.production.yml up -d
```

****
**Linux Ubuntu/Debian**
1. Установите Docker
```bash
sudo apt update
sudo apt install docker.io docker-compose
```
2. Запустите и настройте Docker
```bash
sudo systemctl start docker
sudo systemctl enable docker
```
3. (Опционально) Если хотите использовать Docker без ```sudo```:
```bash
sudo usermod -aG docker $USER
newgrp docker
```
4. Запустите проект выполнив команду:
```bash
sudo docker-compose -f docker-compose.production.yml up -d
```
- ```-f docker-compose.production.yml``` указывает использовать файл docker-compose.production.yml.
- ```-d``` запускает контейнеры в фоновом режиме(может отсутствовать).

5. Собирерите статику и примените миграции БД:
```bash
sudo docker compose -f docker-compose.production.yml exec backend python manage.py migrate
sudo docker compose -f docker-compose.production.yml exec backend python manage.py collectstatic
sudo docker compose -f docker-compose.production.yml exec backend cp -r /app/collected_static/. /static/static/
```
Поздравляем, проект развёрнут!!!

Для остановки контейнеров используйте:
```bash
docker-compose -f docker-compose.production.yml down
```
Для запуска:
```bash
docker-compose -f docker-compose.production.yml up -d
```

### Для развёртывания на удалённом сервере с помощью GitHab Action

1. В клонированном репозитории создайте директорию .github, переместите в неё файл ```kittygram_workflow.yml``` из коневой директории проекта и переименуйти его в ```main.yml```:

```bush
mkdir .github | cp kittygram_workflow.yml .github/main.yml
```

2. В репозитории на GitHub в настройках репозитория добавьте следующие секреты settings->Secrets and varibles->Actions->New repository sectet:

```DOCKER_PASSWORD``` — секрет, содержащий пароль для аутентификации в Docker Registry (например, на Docker Hub).

```DOCKER_USERNAME``` — секрет, содержащий имя пользователя для аутентификации в Docker Registry. 

```HOST``` — переменная, содержащая адрес хоста или сервер, к которому необходимо подключиться. Это может быть IP-адрес или доменное имя, которое используется для SSH-подключений или в других целях (например, для деплоя).

```SSH_KEY``` — приватный SSH-ключ, используемый для аутентификации при подключении к серверу или хосту по SSH. Этот ключ используется в качестве альтернативы паролю для безопасного доступа к удалённым серверам.

```SSH_PASSPHRASE``` — фраза для защиты приватного SSH-ключа.

```TELEGRAM_TO``` — ID получателя для отправки уведомлений через Telegram (например, ID чата или канала). Это значение используется для указания, куда отправить сообщения через Telegram Bot API.

```TELEGRAM_TOKEN``` — токен для доступа к Telegram Bot API. Этот токен используется для аутентификации в Telegram API, чтобы бот мог отправлять сообщения в указанный канал или чат.

```USER``` — имя пользователя, которое может использоваться для аутентификации или для указания, какой пользователь выполняет определённые операции. Это может быть имя пользователя в системе или сервисе для доступа или деплоя.

3. На удалённом сервере создайте директорию ```kittigram``` а внутри файл ```.env```, такой же, как и в примере с локальным развёртыванием, см.выше.
4. В директории корня проекта добавляем изменения в индекс, делаем коммит и пушим на GitHub:
```bash
git add.
git commit -m 'message'
git push
```
Если вы всё зделали правильно, проект развёрнут на вашем удалённом сервере и готов к работе. Он так же будет поддерживать все новые изменения отправленные на удалённый репозиторий, если они не нарушают правильную работу workflow ```main.yml```.
