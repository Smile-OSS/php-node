FROM php:8.1-cli-alpine

LABEL maintainer "Smile EE DevOps <ee.devops.team+github@smile.fr>"

ARG COMPOSER_VERSION
ARG NODE_VERSION

USER root

# Install dependencies.
RUN apk add --update --no-cache \
  bash \
  binutils \
  ca-certificates \
  coreutils \
  curl \
  findutils \
  git \
  libuser \
  linux-headers \
  ncurses \
  openssl \
  openssh \
  php-pcntl \
  php-posix \
  util-linux \
  zlib-dev \
  && rm -rf /var/cache/apk/*

RUN docker-php-ext-install pcntl posix

# change default shell from ash to bash
RUN sed -i -e "s/bin\/ash/bin\/bash/" /etc/passwd

# ENV NVM_DIR /usr/local/nvm

# Install composer.
RUN curl -sS https://getcomposer.org/installer |\
    php -- --install-dir=/usr/local/bin --filename=composer --version=${COMPOSER_VERSION}

RUN wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash #install nvm \
    && export NVM_DIR="$HOME/.nvm" && . "$NVM_DIR/nvm.sh" --no-use #load nvm \
    && eval "[ -f .nvmrc ] && nvm install ${NODE_VERSION}" #install node \
    && npm install --global yarn \
    && echo "`node --version` && `npm --version`"

# Add NVM to .bashrc for initialization by bash.
RUN echo 'export NVM_DIR="$HOME/.nvm"' >> ~/.bashrc  \
    && echo '[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"' >> ~/.bashrc

WORKDIR /app
