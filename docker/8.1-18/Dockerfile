FROM php:8.1-cli-alpine3.18

LABEL maintainer "Smile EE DevOps <ee.devops.team+github@smile.fr>"

WORKDIR /app

        'bash': 'bash',
        'unzip': 'unzip',
        'git': 'git',
        'zip': 'zip',
        'sqlite': 'sqlite-dev',
        'mysql-client': 'mysql-client',
        'mariadb-connector-c': 'mariadb-connector-c',
        'png': 'libpng-dev',
        'zlib': 'zlib-dev',
        'webp/vpx': 'libvpx-dev',
        'jpeg': 'libjpeg-turbo-dev',
        'webp': 'libwebp-dev',
        'xpm': 'libxpm-dev',
        'freetype': 'freetype-dev',
        'msmtp': 'msmtp',


# Install dependencies.
RUN apk add --update --no-cache \
  bash \
  git \
  curl \
  rsync \
  openssh \
  openssl \
  ncurses \
  ca-certificates \
  # nodejs 18 dependencies
  npm \
  nodejs \
  # php dependencies
  zip \
  unzip \
  zlib-dev \
  php-posix \
  php-pcntl \
  libxpm-dev \
  libpng-dev \
  libwebp-dev \
  freetype-dev \
  libjpeg-turbo-dev \
  && rm -rf /var/cache/apk/* \
  && docker-php-ext-install pcntl posix  \
  && docker-php-ext-configure gd --with-jpeg --with-webp --with-freetype \
  && docker-php-ext-install gd \
  # Install composer latest
  && curl -sS https://getcomposer.org/installer |\
  php -- --install-dir=/usr/local/bin --filename=composer \
  # change default shell from ash to bash
  && sed -i -e "s/bin\/ash/bin\/bash/" /etc/passwd \
  && touch ~/.bashrc

ENV COMPOSER_ALLOW_SUPERUSER=1
