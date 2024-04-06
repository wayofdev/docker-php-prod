<br>

<div align="center">
<img width="456" src="https://raw.githubusercontent.com/wayofdev/docker-php-base/master/assets/logo.gh-light-mode-only.png#gh-light-mode-only">
<img width="456" src="https://raw.githubusercontent.com/wayofdev/docker-php-base/master/assets/logo.gh-dark-mode-only.png#gh-dark-mode-only">
</div>

<br>

<br>

<div align="center">
<a href="https://actions-badge.atrox.dev/wayofdev/docker-php-prod/goto"><img alt="Build Status" src="https://img.shields.io/endpoint.svg?url=https%3A%2F%2Factions-badge.atrox.dev%2Fwayofdev%2Fdocker-php-prod%2Fbadge&style=flat-square"/></a>
<a href="https://github.com/wayofdev/docker-php-prod/tags"><img src="https://img.shields.io/github/v/tag/wayofdev/docker-php-prod?sort=semver&style=flat-square" alt="Latest Version"></a>
<a href="https://hub.docker.com/repository/docker/wayofdev/php-prod"><img alt="Docker Pulls" src="https://img.shields.io/docker/pulls/wayofdev/php-prod?style=flat-square"></a>
<a href="LICENSE"><img src="https://img.shields.io/github/license/wayofdev/docker-php-prod.svg?style=flat-square&color=blue" alt="Software License"/></a>
<a href="#"><img alt="Commits since latest release" src="https://img.shields.io/github/commits-since/wayofdev/docker-php-prod/latest?style=flat-square"></a>
</div>

<br>

# Docker Image: PHP

> [!WARNING]  
> Package development **deprecated**
> Use:
>   - https://github.com/wayofdev/docker-php-base
>   - https://github.com/wayofdev/docker-php-dev

<br>

Repository contains dist folder with generated production ready PHP images and source code, written on Ansible, to generate them. Is used together with other WOD images, to create local development environment for our projects.

**Upstream image:** [wayofdev/docker-php-base](https://github.com/wayofdev/docker-php-base)

Additionaly to upstream image, enabled extensions by default:

| Extension                                           | Description                                         | Type   |
| --------------------------------------------------- | --------------------------------------------------- | ------ |
| [soap](https://www.php.net/manual/en/book.soap.php) | For SOAP servers and clients                        | native |
| [exif](https://www.php.net/manual/en/book.exif.php) | Functions for image meta data                       | native |
| [gd](https://www.php.net/manual/en/book.image.php)  | Creating and manipulating image files               | native |
| [imagick]()                                         | Creating and manipulating image files               | pecl   |
| [rdkafka]()                                         | Kafka client based on librdkafka                    | pecl   |
| [amqp]()                                            | Functions to communiate with amqp compliant servers | pecl   |
| [protobuf]()                                        | Mechanism for serializing structured data           | pecl   |
| [yaml]()                                            | YAML file type serialization functions              | pecl   |

<br>

If you **like/use** this repository, please consider **starring** it. Thanks!

<br>

## 🔧 Configuration

Ansible is used to generate distribution files, to add or remove PHP extensions, or configure project, see [group_vars/prod.yml](https://github.com/wayofdev/docker-php-prod/blob/master/src/group_vars/prod.yml)

**Default extension configuration:**

```yaml
ext_native_enabled:
  - soap
  - exif
  - gd

ext_pecl_enabled:
  - imagick
  - rdkafka
  - amqp
  - protobuf
  - yaml

ext_pecl_versions:
  imagick: "3.7.0"
  rdkafka: "6.0.3"
  amqp: "1.11.0"
  protobuf: "3.21.9"
  yaml: "2.2.2"
```

<br>

To generate dist files use ansible command:

```bash
$ make generate
```

<br>

## ⚙️ Development

To install dependencies and start development you can check contents of our `Makefile`

### →  Requirments

For testing purposes we use **goss** and **dgoss**, follow installation instructions on  [their official README](https://github.com/aelsabbahy/goss/blob/master/extras/dgoss/README.md)

<br>

### → Building locally

Generating distributable Dockerfiles from yaml source code:

```bash
$ make generate
```

<br>

Building default image:

```bash
$ git clone git@github.com:wayofdev/docker-php-prod.git
$ make build
```

To **build** image, **test** it and then **clean** temporary files run:

```bash
$ make
```

Building all images:

```bash
$ make build TEMPLATE="7.4-cli-alpine"
$ make build TEMPLATE="7.4-fpm-alpine"
$ make build TEMPLATE="7.4-supervisord-alpine"
$ make build TEMPLATE="8.0-cli-alpine"
$ make build TEMPLATE="8.0-fpm-alpine"
$ make build TEMPLATE="8.0-supervisord-alpine"
$ make build TEMPLATE="8.1-cli-alpine"
$ make build TEMPLATE="8.1-fpm-alpine"
$ make build TEMPLATE="8.1-supervisord-alpine"
```

<br>

## 🧪 Testing

You can check `Makefile` to get full list of commands for local testing. For testing you can use these comands to test whole role or separate tasks:

Testing default image:

```bash
$ make test
```

To test all images:

```bash
$ make test TEMPLATE="7.4-cli-alpine"
$ make test TEMPLATE="7.4-fpm-alpine"
$ make test TEMPLATE="7.4-supervisord-alpine"
$ make test TEMPLATE="8.0-cli-alpine"
$ make test TEMPLATE="8.0-fpm-alpine"
$ make test TEMPLATE="8.0-supervisord-alpine"
$ make test TEMPLATE="8.1-cli-alpine"
$ make test TEMPLATE="8.1-fpm-alpine"
$ make test TEMPLATE="8.1-supervisord-alpine"
```

<br>

### → Code quality tools

Run **yamllint** to validate all yaml files in project:

```bash
$ make lint
```

Run hadolint to validate created Dockerfiles:

```bash
$ make hadolint
```

<br>

## 🤝 License

[![Licence](https://img.shields.io/github/license/wayofdev/docker-php-prod?style=for-the-badge&color=blue)](./LICENSE)

<br>

## 🙆🏼‍♂️ Author Information

This repository was created in **2022** by [lotyp / wayofdev](https://github.com/wayofdev).

<br>

## 🫡 Contributors

<img align="left" src="https://img.shields.io/github/contributors-anon/wayofdev/docker-php-prod?style=for-the-badge" alt="Contributors"/>

<br>
