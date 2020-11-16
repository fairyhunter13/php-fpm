بِسْمِ اللّٰهِ الرَّحْمٰنِ الرَّحِيْمِ

<br/>

السَّلاَمُ عَلَيْكُمْ وَرَحْمَةُ اللهِ وَبَرَكَاتُهُ

<br/>

ٱلْحَمْدُ لِلَّهِ رَبِّ ٱلْعَٰلَمِينَ

ٱلْحَمْدُ لِلَّهِ رَبِّ ٱلْعَٰلَمِينَ

ٱلْحَمْدُ لِلَّهِ رَبِّ ٱلْعَٰلَمِينَ

<br/>

اللَّهُمَّ صَلِّ عَلَى مُحَمَّدٍ ، وَعَلَى آلِ مُحَمَّدٍ ، كَمَا صَلَّيْتَ عَلَى إِبْرَاهِيمَ وَعَلَى آلِ إِبْرَاهِيمَ ، إِنَّكَ حَمِيدٌ مَجِيدٌ ، اللَّهُمَّ بَارِكْ عَلَى مُحَمَّدٍ ، وَعَلَى آلِ مُحَمَّدٍ ، كَمَا بَارَكْتَ عَلَى إِبْرَاهِيمَ ، وَعَلَى آلِ إِبْرَاهِيمَ ، إِنَّكَ حَمِيدٌ مَجِيدٌ

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
# Unincluded Plugins
The image doesn't contain these following plugins:
- ffi is not supported for php version 7.2
- gmagick, because there is already imagick installed
- mongo is not supported for php version 7.2
- mssql is not supported for php version 7.2
- mysql is not supported for php version 7.2
- parallel, because the image doesn't have php which the thread-safety feature is enabled
- pthreads, because the image doesn't have php which the thread-safety feature is enabled
- snuffleupagus, because it keeps messing with the installation of the plugins and maybe the php execution's script
- sybase_ct is not supported for php version 7.2
- xdebug, because it makes the composer's command stuck inside Docker container

