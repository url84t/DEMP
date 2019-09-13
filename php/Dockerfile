FROM php:7.2-fpm
RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    gnupg2 \
    git \
    zip \
    unzip \
    curl \
    cron \
    procps \
    && docker-php-ext-install zip \
    && docker-php-ext-install pdo pdo_mysql \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd


# cron
COPY laravel-cron /etc/cron.d/laravel-cron
RUN chmod 0644 /etc/cron.d/laravel-cron
RUN crontab /etc/cron.d/laravel-cron
# RUN touch /var/log/cron.log # add cron.log to log dir

RUN apt-get update && apt-get install -y \
    curl \
    software-properties-common

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -

RUN apt-get update && apt-get install -y \
    build-essential \
    nodejs

RUN npm install -g npm

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    #&& php -r "if (hash_file('sha384', 'composer-setup.php') === '93b54496392c062774670ac18b134c3b3a95e5a5e5c8f1a9f115f203b75bf9a129d5daa8ba6a13e2cc8a1da0806388a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /bin/composer

RUN composer global require laravel/installer


RUN echo "export PATH=$HOME/.composer/vendor/bin:$PATH" >> ~/.bashrc

# remove hard links
RUN touch /etc/crontab /etc/cron.*/*
# start cron
# CMD cron && tail -f /var/log/cron.log
RUN cron
CMD php-fpm