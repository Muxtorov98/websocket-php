FROM php:8.2-cli

RUN apt-get update && apt-get install -y git unzip libicu-dev

COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

WORKDIR /app

COPY composer.json ./

RUN composer install --no-interaction --no-scripts --no-progress

COPY server.php ./

CMD ["php", "server.php"]
