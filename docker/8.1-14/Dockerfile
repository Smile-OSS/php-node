FROM php:8.1-cli-alpine3.14

LABEL maintainer "Smile EE DevOps <ee.devops.team+github@smile.fr>"

WORKDIR /app

# Install dependencies.
RUN apk add --update --no-cache \
  bash \
  git \
  curl \
  openssh \
  openssl \
  ncurses \
  ca-certificates \
  # nodejs 14 dependencies
  npm \
  nodejs \
  # php dependencies
  zlib-dev \
  php-posix \
  php-pcntl \
  libpng-dev \
  libwebp-dev \
  freetype-dev \
  libjpeg-turbo-dev \
  && rm -rf /var/cache/apk/* \
  && docker-php-ext-install pcntl posix \
  && docker-php-ext-configure gd --with-jpeg --with-webp --with-freetype \
  && docker-php-ext-install gd \
  # Install composer.
  && curl -sS https://getcomposer.org/installer |\
  php -- --install-dir=/usr/local/bin --filename=composer --version=2.2.22 \
  # change default shell from ash to bash
  && sed -i -e "s/bin\/ash/bin\/bash/" /etc/passwd \
  && touch ~/.bashrc
