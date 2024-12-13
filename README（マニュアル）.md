Docker環境構築

Dockerfileを作成して、4〜20をDockerfile内に記載
# ベースイメージ
FROM php:8.2-fpm

# 必要なパッケージのインストール
RUN apt-get update && apt-get install -y \
    libzip-dev zip unzip git curl && \
    docker-php-ext-install pdo pdo_mysql zip && \
    docker-php-ext-enable pdo_mysql

# Composerのインストール
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# 作業ディレクトリの設定
WORKDIR /var/www/html

# 権限変更
RUN chown -R www-data:www-data /var/www/html

docker-compose.ymlを作成して、23〜57をdocker-compose.yml内に記載
version: '3.8'

services:
  app:
    build:
      context: .
      dockerfile: Dockerfile
    container_name: laravel_app
    working_dir: /var/www/html
    volumes:
      - ./Laravel:/var/www/html
    ports:
      - "8000:8000"
    environment:
      - APP_ENV=local
      - APP_DEBUG=true
    depends_on:
      - db

  db:
    image: mysql:8.0
    container_name: laravel_db
    restart: always
    ports:
      - "3306:3306"
    environment:
      MYSQL_ROOT_PASSWORD=root
      MYSQL_DATABASE=laravel
      MYSQL_USER=laravel
      MYSQL_PASSWORD=secret
    volumes:
      - db_data:/var/lib/mysql

volumes:
  db_data:

