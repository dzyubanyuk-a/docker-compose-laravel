FROM php:8.2.12-fpm

WORKDIR /var/www

RUN groupadd -g 1000 www && \
    useradd -u 1000 -ms /bin/bash -g www www

RUN apt-get update && apt-get install -y \
    curl \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libzip-dev \
    libonig-dev \
    libxml2-dev \
    zlib1g-dev \
    libssl-dev && \
    docker-php-ext-configure gd --with-freetype --with-jpeg && \
    docker-php-ext-install -j$(nproc) gd mysqli pdo_mysql zip mbstring xml && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

COPY --chown=www:www . /var/www

USER www

CMD ["php-fpm"]