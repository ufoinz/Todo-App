# Todo-App

Todo-App — это приложение с фронтендом на Angular и бэкендом на Go, с базой данных PostgreSQL. Все сервисы запускаются через Docker.

## Функционал

Приложение Todo-App позволяет управлять задачами и пользователями. Основные возможности:

- **Регистрация и вход пользователя** через email и пароль
- **Создание задач** с указанием заголовка, описания и даты выполнения
- **Просмотр всех задач** для текущего пользователя
- **Редактирование задач** (изменение заголовка, описания или даты)
- **Удаление задач**
- **REST API** для всех операций (доступно через `/api/v1/...`)
- **SPA фронтенд** с Angular и Nginx, который автоматически отображает актуальные данные

## Интерфейс
- Страница входа
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/9deac3e9-01b7-45b3-b36b-e820d6365bb9" />

- Страница событий
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/72c94df4-cf06-4235-9381-402d0bf3959a" />


## Структура проекта
```
todo-app/
├─ todo-backend/ # backend на Go
├─ todo-frontend/ # frontend на Angular
├─ docker-compose.yml
├─ .gitignore
└─ README.md
```

## Стек и библиотеки

- **Go (Gin)** — веб-фреймворк для бэкенда  
  - **GORM** — ORM для работы с PostgreSQL (`gorm.io/gorm`, `gorm.io/driver/postgres`)  
  - **godotenv** — загрузка переменных окружения из `.env` (если используется)  
  - **gin-contrib/cors** — настройка CORS  
  - **golang-jwt/jwt** — работа с JWT  
- **Angular** — фронтенд  
  - **@angular/router** — маршрутизация  
  - **@angular/forms** — формы  
- **PostgreSQL** — база данных  
- **Docker & Docker Compose** — контейнеризация  
- **Nginx** — веб-сервер для фронтенда


## Настройка

**1.** Клонируйте репозиторий:

```bash
git clone https://github.com/ufoinz/Todo-App.git
cd Todo-App
```

**2.** Проверьте .env файлы для backend и frontend:

- todo-backend/.env:
```
DB_HOST=db
DB_PORT=5432
DB_USER=postgres
DB_PASSWORD=example
DB_NAME=tododatabase
```

- todo-frontend/.env (если используется):
```
API_URL=http://localhost:8080/api
```
> **Важно:** эти файлы не включены в репозиторий.

**3.** Постройте и запустите все сервисы через Docker Compose:
```
docker-compose up --build
```

**4.** После запуска:

- Фронтенд доступен по адресу: http://localhost:4200
- Бэкенд API доступен по адресу: http://localhost:8080/api
- PostgreSQL: порт 5432

**5.** Для остановки сервисов:
```
docker-compose down
```

## Команды для работы с Docker

- **Пересобрать проект с нуля:**
```
docker-compose down -v
docker-compose up --build
```

- **Подключение к базе PostgreSQL внутри Docker:**
```
docker exec -it todo-app-db-1 psql -U postgres -d todo_db
```

- **Проверка логов фронтенда и бэкенда:**
```
docker logs todo-app-frontend-1
docker logs todo-app-backend-1
```

## Структура базы данных

- **users** — хранит пользователей (id, email, пароль)
- **events** — хранит задачи (id, user_id, title, description, due_date)


