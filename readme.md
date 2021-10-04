# Laravel + Apache + Docker

## Description
Start developing a fresh Laravel application with `docker` using `docker-compose`.

The images used in this repo is `php:7.2-apache` and `mysql:5.7`. The goal is to make setting up the development as simple as possible.

## Up and running
Clone the repo:
```
$ git clone https://github.com/sureshel/docker-apache-laravel8
$ cd docker-apache-laravel8
```

Copy `.env.example` to `.env`
```
$ cp .env.example .env 
```

Build the images and start the services:
```
docker-compose build
docker-compose up
```


### Laravel container - Install Composer and Key Generation
```
$ docker exec -it YOUR_LARAVEL_CONATINER_ID/NAME bash
user@11111:/var/www/html$ composer install
user@11111:/var/www/html$ php artisan key:generate
```
### Get or Update Database credentials
The Database credentials can be found for root user in docker-compose.yml file. If you want to create a new user in DB for Laravel website application you can do so by logging into the DB using root credentials. If not, you can use the root user for development purpose only.

You can also connect to mysql DB using any mysql client. Please run docker ps to check the hsot and port
DB host: localhost
Port: 3306
Get the credentails from .env file for docker-compose file.

### MYSQL DB container
```
$ docker exec -it YOUR_MYSQL_CONATINER_ID/NAME bash
user@11111:/var/www/html$ root@1558bf84bbf2:/# mysql -uroot -p
Enter password:
```
Once you enter the correct password you will get into the MySQL server. You can create new users with specific grants/priviledges.
```
mysql>
```


### Create Tables - Laravel Migrations 
```
$ docker exec -it YOUR_LARAVEL_CONATINER_ID/NAME bash
user@11111:/var/www/html$ php artisan migrate
```
Your Laravel Website should be up and running. Try the below urls, register as a new user and check your mysql database.
http://localhost:8000/login
http://localhost:8000/register


## Helper scripts
Running `composer`, `php artisan` or `phpunit` against the `php` container with helper scripts in the main directory:

### composer
Run `composer` command, example:
```
$ ./composer dump-autoload
Generating optimized autoload files> Illuminate\Foundation\ComposerScripts::postAutoloadDump
> @php artisan package:discover --ansi
Discovered Package: beyondcode/laravel-dump-server
Discovered Package: fideloper/proxy
Discovered Package: laravel/tinker
Discovered Package: nesbot/carbon
Discovered Package: nunomaduro/collision
Package manifest generated successfully.
Generated optimized autoload files containing 3527 classes
```

### php-artisan
Run `php artisan` commands, example:
```
$ ./php-artisan make:controller BlogPostController --resource
php artisan make:controller BlogPostController --resource
Controller created successfully.
```

### phpunit
Run `./vendor/bin/phpunit` to execute tests, example:
```
$ ./phpunit --group=failing
vendor/bin/phpunit --group=failing
PHPUnit 7.5.8 by Sebastian Bergmann and contributors.



Time: 34 ms, Memory: 6.00 MB

No tests executed!
```
