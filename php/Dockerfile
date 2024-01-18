FROM php:8.1-fpm-alpine

WORKDIR "/var/www/html"

ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

RUN echo "Updating dependencies:"
RUN apk update && apk add \
	mc \
	nano \
  build-base \
  freetype-dev \
  libjpeg-turbo-dev \
  libpng-dev \
  libwebp-dev \
  libzip-dev \
  zip \
  unzip \
  git \
  oniguruma-dev \
  curl \
  libmcrypt-dev \
  neovim \
  bash \
  openssh-client \
  postgresql-dev

RUN apk add --update linux-headers

# Installing PDO-MySQL Extension
RUN echo "Installing PDO-MySQL Extension:"
RUN docker-php-ext-install pdo_mysql mbstring zip exif pcntl

# # Installing PDO-PostgreSQL Extension
# RUN echo "Installing PDO-PostgreSQL Extension:"
# RUN docker-php-ext-install pdo_pgsql mbstring zip exif pcntl

# Installing Redis Extension
RUN echo "Installing Redis Extension:"
RUN apk add autoconf && pecl install -o -f redis \
    &&  rm -rf /tmp/pear \
    &&  docker-php-ext-enable redis && apk del autoconf

# Installing composer
RUN echo "Installing composer"
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Configure images formats
RUN echo "Configure images formats:"
RUN docker-php-ext-configure gd --with-freetype --with-webp --with-jpeg && \
  docker-php-ext-install gd

# Installing NodeJS
RUN echo "Installing NodeJS:"
RUN apk add nodejs npm
