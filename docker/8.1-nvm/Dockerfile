FROM php:8.1-cli-bookworm as php

LABEL maintainer "Smile EE DevOps <ee.devops.team+github@smile.fr>"

WORKDIR /app

# Install dependencies.
RUN apt update && apt install -y \
  bash \
  curl \
  git \
  unzip \
  wget \
  zip \
  openssl \
  libpng-dev \
  ca-certificates \
  libfreetype6-dev \
  libjpeg62-turbo-dev \
  libncurses5-dev libncursesw5-dev \
  && docker-php-ext-install pcntl posix \
  && docker-php-ext-configure gd --with-freetype --with-jpeg \
  && docker-php-ext-install -j$(nproc) gd \
  && touch ~/.bashrc && mkdir ~/.nvm

# ENV NVM_DIR /usr/local/nvm

# Install composer.
RUN curl -sS https://getcomposer.org/installer |\
  php -- --install-dir=/usr/local/bin --filename=composer

# Install nvm
RUN wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh \
  | bash \
  && nvm install ${NODE_VERSION} # install node \
  && ln -s "$(npm bin --global)" /usr/local/bin # add node bin to path \
  && echo 'export NVM_DIR="$HOME/.nvm"' >> ~/.bashrc  \
  && echo '[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"' >> ~/.bashrc \
  && source ~/.bashrc \
  && nvm install --lts=fermium \
  && nvm install --lts=gallium \
  && nvm install --lts=hydrogen

FROM scratch AS scratch
COPY --from=php / /

