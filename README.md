# praktikum_new_diplom
# ЯП - Спринт 14 - Приложение «Продуктовый помощник». Python-разработчик (бекенд) (Яндекс.Практикум)

### Описание

Приложение «Продуктовый помощник»: сайт, на котором пользователи будут публиковать рецепты, добавлять чужие рецепты в избранное и подписываться на публикации других авторов. Сервис «Список покупок» позволит пользователям создавать список продуктов, которые нужно купить для приготовления выбранных блюд. 

Полная документация к API находится по эндпоинту api/docs/redoc

![example workflow](https://github.com/alexandra2706/foodgram-project-react/actions/workflows/yamdb_workflow.yml/badge.svg)

### Установка, Как запустить проект на сервере:

Клонировать репозиторий:

```
git clone git@github.com:Alexandra2706/foodgram-project-react.git
```

В клонированном репозитории создать secrets:

```
 - DB_ENGINE - django.db.backends.postgresql
 - DB_HOST - db
 - DB_NAME - postgres
 - DB_PORT - 5432
 - DOCKER_PASSWORD - <ваш_пароль_dockerhub>
 - DOCKER_USERNAME -<ваш_username_dockerhub> 
 - HOST - IP-адрес вашего сервера
 - PASSPHRASE - пароль к ssh-ключу
 - POSTGRES_PASSWORD - postgres
 - POSTGRES_USER -postgres
 - SSH_KEY - ваш ssh-ключ
 - TELEGRAM_TO - ID вашего телеграм-аккаунта
 - TELEGRAM_TOKEN - токен вашего бота
 - USER - имя пользователя для подключения к серверу
```

На сервере усиановить докер:

```
sudo apt install docker.io
```

Изменить ip-адрес сервера в файле:

```
/infra/nginx/default.conf
```

Подключиться к серверу по ssh-ключу:

```
ssh your_login@pu.bl.ic.ip
```

Скопировать файлы docker-compose.yml и nginx.conf на сервер в home/<ваш_username>/docker-compose.yaml и home/<ваш_username>/nginx/default.conf соответственно

```
 - docker-compose.yaml в home/<ваш_username>/docker-compose.yml
 - nginx.conf в home/<ваш_username>/nginx.conf
```

Запушить проект на сервер:

```
 - git add .
 - git commit -m "comment"
 - git push
```

Запустить docker-compose:

```
docker-composer up
```

Выполнить миграцииб импортировать данные, создать суперюзера, собрать статику:

```
docker-compose exec backend python manage.py migrate
sudo docker-compose exec backend python manage.py load_all_data
sudo docker-compose exec backend python manage.py load_tags
docker-compose exec backend python manage.py createsuperuser
docker-compose exec backend python manage.py collectstatic --no-input
```

Проект можно посмотреть по адресу:

```
http://84.201.141.88/admin/login/?next=/admin/
```

или

```
http://myproject.hopto.org/admin/login/?next=/admin/
```

Логин и пароль:

```
login: addmin
password: addmin
```

### Установка, Как запустить проект локально:

Клонировать репозиторий и перейти в него в командной строке:

```
git clone git@github.com:Alexandra2706/foodgram-project-react.git
cd foodgram-project-react
```

Cоздать и активировать виртуальное окружение:

```
python -m venv env
```

* Если у вас Linux/macOS

    ```
    source env/bin/activate
    ```

* Если у вас windows

    ```
    source env/scripts/activate
    ```

```
python -m pip install --upgrade pip
```

Установить зависимости из файла requirements.txt:

```
pip install -r requirements.txt
```

```
cd backend
```

Выполнить миграции:

```
python manage.py migrate
```

Создать суперюзера:

```
python3 manage.py createsuperuser
```

Запустить проект:

```
python3 manage.py runserver
```

### Примеры работы с API для всех пользователей

Для неавторизованных пользователей работа с API доступна в режиме чтения, что-либо изменить или создать не получится.

```
GET /api/recipes/ - Получение списка всех рецептов
GET /api/recipes/{id}/ - Получение рецепта
GET /api/users/ - Получение списка всех пользователей
GET /api/users/{id}/ - Профиль пользователя
GET /api/users/ - Получение списка всех пользователей
GET /api/tags/ - Получение списка всех тегов
GET /api/ingredients/ - Получение списка всех ингредиентов
```

### Уровни доступа пользователей

- **Гость (неавторизованный пользователь)** — Создать аккаунт, просматривать рецепты на главной, просматривать отдельные страницы рецептов, просматривать страницы пользователей, фильтровать рецепты по тегам.
- **Авторизованный пользователь** — может, входить в систему под своим логином и паролем, выходить из системы (разлогиниваться), менять свой пароль, создавать/редактировать/удалять собственные рецепты, просматривать рецепты на главной, просматривать страницы пользователей, просматривать отдельные страницы рецептов, фильтровать рецепты по тегам, работать с персональным списком избранного: добавлять в него рецепты или удалять их, просматривать свою страницу избранных рецептов, работать с персональным списком покупок: добавлять/удалять любые рецепты, выгружать файл с количеством необходимых ингридиентов для рецептов из списка покупок, подписываться на публикации авторов рецептов и отменять подписку, просматривать свою страницу подписок.
- **Что может делать администратор** — те же права, что и у Аутентифицированного пользователя плюс изменять пароль любого пользователя, создавать/блокировать/удалять аккаунты пользователей, редактировать/удалять любые рецепты, добавлять/удалять/редактировать ингредиенты, добавлять/удалять/редактировать теги.

### Регистрация нового пользователя

В проекте должна быть доступна система регистрации и авторизации пользователей.

Регистрация нового пользователя:

```
POST /api/users/post/
```


```
{
"email": "vpupkin@yandex.ru",
"username": "vasya.pupkin",
"first_name": "Вася",
"last_name": "Пупкин",
"password": "Qwerty123"
}
```
Получение токена-авторизации:

```
POST /api/auth/token/login/
```

```
{
  "password": "string",
  "email": "string"
}
```
### Примеры работы с API для авторизованных пользователей
**Добавление рецепта:**

```
POST /api/recipes/
```
```
{
  "ingredients": [],
  "tags": [],
  "image": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABAgMAAABieywaAAAACVBMVEUAAAD///9fX1/S0ecCAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAACklEQVQImWNoAAAAggCByxOyYQAAAABJRU5ErkJggg==",
  "name": "string",
  "text": "string",
  "cooking_time": 1
}
```
Удаление рецепта:

```
DELETE /api/recipes/{id}/
```
Обновление рецепта:

```
PATCH /api/recipes/{id}/
```
```
{
  "ingredients": [],
  "tags": [],
  "image": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABAgMAAABieywaAAAACVBMVEUAAAD///9fX1/S0ecCAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAACklEQVQImWNoAAAAggCByxOyYQAAAABJRU5ErkJggg==",
  "name": "string",
  "text": "string",
  "cooking_time": 1
}
```
Добавление рецепта в избранное:
```

POST /api/recipes/{id}/favorite/
```
```
Удаление рецепта из избранного:

```
DELETE /api/recipes/{id}/favorite/
```

```
**Подписки:**
```
Возвращает пользователей, на которых подписан текущий пользователь.
GET /api/users/subscriptions/
```

```
Подписаться на пользователя
POST /api/users/{id}/subscribe/
```

```
Отписаться от пользователя
DELETE /api/users/{id}/subscribe/
```

**Список покупок**

```
Скачать список покупок
GET /api/recipes/download_shopping_cart/
```

```
Добавить рецепт в список покупок
POST /api/recipes/{id}/shopping_cart/
```

```
Удалить рецепт из списка покупок
DELETE /api/recipes/{id}/shopping_cart/
```

Проект сделан в рамках учебного процесса по специализации Python-разработчик (back-end) Яндекс.Практикум.

Автор в рамках учебного курса ЯП Python - разработчик бекенда:

- [Александра Гаврилова](https://github.com/Alexandra2706)
