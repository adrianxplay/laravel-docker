FROM php:7.2.10-cli

RUN apt-get update && apt-get install -y libpq-dev

RUN docker-php-source extract \
    && docker-php-ext-install pdo_pgsql \
    && docker-php-ext-configure pdo_pgsql \
    && docker-php-source delete

ADD wait-for-it.sh /usr/local/bin/wait-for-it

RUN chmod +x /usr/local/bin/wait-for-it

WORKDIR /code

CMD wait-for-it postgres:5432 -- php artisan migrate:fresh --seed \
    && tail -f /dev/null

CMD tail -f /dev/null