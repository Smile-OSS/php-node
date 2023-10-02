# PHP with Node and Composer for Ci/Cd

[![GitHub release (with filter)](https://img.shields.io/github/v/release/Smile-OSS/php-node?style=for-the-badge)](https://github.com/Smile-OSS/php-node/pkgs/container/php-node)
[![GitHub](https://img.shields.io/github/license/Smile-OSS/php-node?style=for-the-badge)](LICENSE)
[![GitHub Workflow Status (with event)](https://img.shields.io/github/actions/workflow/status/Smile-OSS/php-node/build.yml?style=for-the-badge)](https://github.com/Smile-OSS/php-node/actions)
[![Sonar Violations (long format)](https://img.shields.io/sonar/violations/Smile-OSS_php-node/main?server=https%3A%2F%2Fsonarcloud.io&style=for-the-badge)](https://github.com/Smile-OSS/php-node/actions)

- [PHP with Node and Composer for Ci/Cd](#php-with-node-and-composer-for-cicd)
  - [Contents](#contents)
    - [`$PHP_VERSION-nvm-$TAG`](#php_version-nvm-tag)
    - [`$PHP_VERSION-14-$TAG`](#php_version-14-tag)
    - [`$PHP_VERSION-16-$TAG`](#php_version-16-tag)
    - [`$PHP_VERSION-18-$TAG`](#php_version-18-tag)
  - [Size of images](#size-of-images)
  - [Usage](#usage)

## Contents

There are four tags for each PHP version:

### `$PHP_VERSION-nvm-$TAG`

This PHP image is based on the official PHP Debian with next additions:

- NVM with next LTS Node versions: `14`, `16`, `18`
- Composer `latest` version

### `$PHP_VERSION-14-$TAG`

This PHP image is based on the official PHP Alpine 3.14 with next additions:

- Node 14
- Composer `2.2.22`

### `$PHP_VERSION-16-$TAG`

This PHP image is based on the official PHP Alpine 3.16 with next additions:

- Node 16
- Composer `2.5.8`

### `$PHP_VERSION-18-$TAG`

This PHP image is based on the official PHP Alpine 3.18 with next additions:

- Node 18
- Composer `latest`

## Size of images

```bash
REPOSITORY                   TAG              IMAGE ID       CREATED             SIZE
ghcr.io/smile-oss/php-node   8.1-14-v1.0.3    ff917b60f6fa   About an hour ago   170MB
ghcr.io/smile-oss/php-node   8.1-18-v1.0.3    3376ab312e36   About an hour ago   176MB
ghcr.io/smile-oss/php-node   8.1-16-v1.0.3    8f87df78ac6d   About an hour ago   175MB
ghcr.io/smile-oss/php-node   8.1-nvm-v1.0.3   5ac0f9e25761   About an hour ago   1.03GB

```

## Usage

Please use `task --list-all` to see all available tasks with their description.

```bash
❯ task --list-all
task: Available tasks for this project:
* build:           Build docker image      (aliases: default)
* build-all:       Build all docker images
* push:            Push docker image
* push-all:        Push all docker images

```

And `task --summary <task>` to see full description of the task.

```bash
❯ task --summary build-all
task: build-all

Build all docker images

It will iterate over all directories in `docker` directory and build docker images
based on the directory name as the PHP version.

Example:
❯ task build-all Tag=v1.0.0

commands:
 - for dir in $(find ./docker -maxdepth 1 -type d -not -path '*/\.*' -not -path './docker'); do
  task build Version=$(basename $dir) Tag=
done

```

Current status:

![Curremt status](docs/assets/current.png)
