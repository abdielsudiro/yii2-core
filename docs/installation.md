# Installation

## Table of contents

- [Before you begin](#before-you-begin)
- [Manual installation](#manual-installation)
    - [Requirements](#requirements)
    - [Setup application](#setup-application)
    - [Authentication](#authentication)
    - [Configure your web server](#configure-your-web-server)
    - [Single domain installtion](#single-domain-installation)
    - [Video instruction](#video-instruction)
- [Vagrant installation](#vagrant-installation)

## Before you begin

If you do not have [Composer](http://getcomposer.org), you may install it by following the instructions at [getcomposer.org](http://getcomposer.org/doc/00-intro.md#installation-nix).

It uses [asset-packagist](https://asset-packagist.org) for managing bower and npm package dependencies through Composer. Also you can use [asset-plugin](https://packagist.org/packages/fxp/composer-asset-plugin), as in earlier versions, but it works slowly.

### Get source code via Composer

You can install this application template with `composer` using the following command:

```bash
composer create-project --prefer-dist --stability=dev beaten-sect0r/yii2-core
```

### Get source code

#### Download sources

https://github.com/Beaten-Sect0r/yii2-core/archive/master.zip

#### Or clone repository manually

```bash
git clone https://github.com/Beaten-Sect0r/yii2-core.git
```

#### Install composer dependencies

```bash
composer install --prefer-dist
```

## Manual installation

### Requirements

The minimum requirement by this project template is that your Web server supports PHP 5.4.0.

### Setup application

1. Copy `.env.dist` to `.env` in the project root.

2. Adjust settings in `.env` file
	- Set debug mode and your current environment

	```
	YII_DEBUG = true
	YII_ENV = dev
	```

	- Set DB configuration

	```
	DB_DSN = mysql:host=localhost;port=3306;dbname=yii2-core
	DB_USERNAME = user
	DB_PASSWORD = password
	```

	- Set application canonical urls

	```
	FRONTEND_URL = http://alyatama.loc
	BACKEND_URL = http://backend.alyatama.loc
	STORAGE_URL = http://storage.alyatama.loc
	```

3. Run in command line

```bash
php yii app/setup
```

### Authentication

`administrator` role account

```
Login: Administrator
Password: passwd
```

### Configure your web server

Or configure your web server with three different web roots:
- alyatama.loc => /path/to/yii2-core/frontend/web
- backend.alyatama.loc => /path/to/yii2-core/backend/web
- storage.alyatama.loc => /path/to/yii2-core/storage

### Single domain installation

#### Setup application

Adjust settings in `.env` file

```
FRONTEND_URL = http://alyatama.loc
BACKEND_URL = http://alyatama.loc/backend
STORAGE_URL = http://alyatama.loc/storage
```

Adjust settings in `backend/config/main.php` file

```php
    ...
    'components'=>[
        ...
        'request' => [
            'baseUrl' => '/backend',
        ...
```

Adjust settings in `frontend/config/main.php` file

```php
    ...
    'components'=>[
        ...
        'request' => [
            'baseUrl' => '',
        ...
```

#### Configure your web server

##### Apache

Single domain .htaccess for apache

```apache
# Set the default charset.
AddDefaultCharset UTF-8

# Don't show directory listings for URLs which map to a directory.
Options -Indexes

# Enable symlinks
Options +FollowSymlinks

# Enable mod_rewrite
RewriteEngine On

# Backend redirect
RewriteCond %{REQUEST_URI} ^/backend
RewriteRule ^backend/(.*)$ backend/web/$1 [L]

# Storage redirect
RewriteCond %{REQUEST_URI} ^/storage
RewriteRule ^storage/(.*)$ storage/$1 [L]

# Frontend redirect
RewriteCond %{REQUEST_URI} ^(.*)$
RewriteRule ^(.*)$ frontend/web/$1
```

### Video instruction

[https://www.youtube.com/watch?v=XAC5joagA70](https://www.youtube.com/watch?v=XAC5joagA70)

## Vagrant installation

This way is the easiest but long (~20 min).

**This installation way doesn't require pre-installed software (such as web-server, PHP, MySQL etc.)** - just do next steps!

1. Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
2. Install [Vagrant](https://www.vagrantup.com/downloads.html)
3. Create GitHub [personal API token](https://github.com/blog/1509-personal-api-tokens)
4. Copy `vagrant-local.example.yml` to `vagrant-local.yml`
5. Place your GitHub personal API token to `vagrant-local.yml`
6. Run commands:

    ```bash
    cd yii2-core
    vagrant plugin install vagrant-hostmanager
    vagrant up
    ```

That's all. You just need to wait for completion! After that you can access project locally by URLs:
* frontend: http://alyatama.loc
* backend: http://backend.alyatama.loc
* storage: http://storage.alyatama.loc
* phpmyadmin: http://pma.alyatama.loc
