# Symfony REST API Example

Этот проект демонстрирует простое REST API на Symfony 7.2 с использованием PHP 8.4, Docker, PostgreSQL и Redis. Реализованы 3 эндпоинта для работы с пользователями:
- **GET /api/users** – получение списка всех пользователей
- **POST /api/users** – создание пользователя (DTO + валидация)
- **DELETE /api/users/{id}** – удаление пользователя по ID

## Функциональность
- **DTO и валидация:** Входящие данные для создания пользователя сериализуются в DTO с использованием Symfony Validator (атрибуты валидации).
- **Сервисный слой:** Бизнес-логика вынесена в отдельный сервис, что соответствует принципам SOLID.
- **Тестирование:** Функциональные тесты написаны с использованием Symfony PHPUnit Bridge.

## Требования
- PHP 8.4
- Docker и Docker Compose
- Composer

## Установка

1. **Клонируйте репозиторий:**

   ```bash
   git clone https://github.com/your-username/your-repo.git
   cd your-repo
   ```
   
2. **Установите зависимости через Composer:**

   ```bash 
   composer install
   ```
3. **Настройте переменные окружения:**

Скопируйте файл .env в .env.local и настройте параметры подключения к базе данных и другим сервисам (например, PostgreSQL, Redis).
4. **Создайте базу данных и выполните миграции:**
    
  ```bash 
      php bin/console doctrine:database:create
      php bin/console doctrine:schema:update --force
   ```

## Запуск проекта в Docker
В корне проекта находится файл compose.yaml, который включает следующие контейнеры:
- **php:** Образ PHP 8.4 с FPM и необходимыми расширениями.
- **nginx:** Веб-сервер для обслуживания приложения.
- **postgres:** База данных PostgreSQL.

## Запуск контейнеров

   ```bash 
    docker-compose up -d
   ```

После запуска приложение будет доступно по адресу http://localhost:8080.

## Сброс кэша
При разработке нужно отключить Jit. 

При добавлении файлов в контейнере php необходимо выполнить скрипт:

 ```bash
    ./cache.sh
 ```

   Он сбрасывает и прогревает кэш.  

## API Эндпоинты
Api документация http://localhost:8080/api/doc.

## Тестирование

   Перед запуском тестов необходимо подготовить тестовую базу данных.
   
### Подготовка тестовой базы данных

  Выполните следующие команды, чтобы создать тестовую базу данных, сформировать схему и загрузить тестовые фикстуры:
  
1. **Создать базу данных:**

    ```bash 
      php bin/console --env=test doctrine:database:create
    ```
2. **Создать схему базы данных:**
    ```bash
   php bin/console --env=test doctrine:schema:create
    ```
    
3. **Загрузить фикстуры:**
   ```bash
    php bin/console --env=test doctrine:fixtures:load
    ``` 

## Запуск тестов
Запустите тесты с помощью команды:
    
```bash
   ./bin/simple-phpunit
  ```