# JailStack Back-End

> A Laravel App

https://laravel.com/

## Develop

local
```sh
# install dependency package
composer install

# copy .env.example to .env and edit some info on it, such as db name, db user, etc.
cp .env.example .env

# generate APP_KEY and JWT_SECRET in .env
php artisan key:generate
php artisan vendor:publish --provider="Tymon\JWTAuth\Providers\LaravelServiceProvider"
php artisan jwt:secret

# db migration
php artisan migrate

# start a PHP's built-in development server for laravel
php artisan serve
```

docker compose
```sh
docker-compose up -d php7.2-cli mysql

# enter php7.2-cli and execute following commands
docker-compose exec php7.2-cli bash

# install dependency package
composer install

# copy .env.example to .env and edit some info on it, such as db name, db user, etc.
cp .env.example .env

# generate APP_KEY and JWT_SECRET in .env
php artisan key:generate
php artisan vendor:publish --provider="Tymon\JWTAuth\Providers\LaravelServiceProvider"
php artisan jwt:secret

# db migration
php artisan migrate

# start a PHP's built-in development server for laravel
php artisan serve --host 0.0.0.0
```

## Deploy

build docker image
```sh
docker build -t jailstack .
```

build docker image with custom db config
```sh
docker build -t jailstack \
  --build-arg DB_HOST=127.0.0.1 \
  --build-arg DB_PORT=3307 \
  --build-arg DB_DATABASE=jailstack \
  --build-arg DB_USER=user \
  --build-arg DB_PASSWORD=pwd .
```

run with docker-compose
```sh
docker-compose up -d php7.2-apache mysql

# enter php7.2-apache and run db migration
docker-compose exec php7.2-apache bash
php artisan migrate
```