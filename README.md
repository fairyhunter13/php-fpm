# php-fpm
This php-fpm image is a docker image with almost all of the prebuilt extensions, Composer, and PHP-FPM.
The Composer and PHP-FPM image are used from the official library.

# How to Use
There are two of all alternatives to use this Dockerfile.

## Using Dockerfile
Make a Dockerfile.
```Dockerfile
FROM fairyhunter13/php-fpm:7.2

RUN install-php-extensions gd xdebug
```

After that, run these commands.
```bash
$ docker build -t yourapp .
$ docker run -it --rm --name your-fpm-app yourapp
```

## Using Docker Compose

```yml
version: "3"
services:
  php-fpm:
    tty: true
    stdin_open: true
    restart: on-failure
    image: fairyhunter13/php-fpm:7.2
```


