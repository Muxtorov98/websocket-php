FROM php:8.2-cli-alpine

# kerakli paketlar
RUN apk add --no-cache git unzip icu-dev oniguruma-dev

# composer yuklab olish
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

WORKDIR /app

# composer.json va composer install
COPY composer.json ./

RUN composer install --no-interaction --no-scripts --no-progress --prefer-dist

# server fayl
COPY server.php ./

EXPOSE 8080

CMD ["php", "server.php"]
