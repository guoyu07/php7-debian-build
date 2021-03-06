# php7-debian-build install php7 on debian wheezy
## Build php 7


###### Mostly for my own reference.  Should work on a fresh Debian installation.
####### TODO: Install phpmyadmin

add to /etc/apt/sources.list:
```
# Testing repository - main, contrib and non-free branches
deb http://http.us.debian.org/debian testing main non-free contrib
deb-src http://http.us.debian.org/debian testing main non-free contrib


# Testing security updates repository
deb http://security.debian.org/ testing/updates main contrib non-free
deb-src http://security.debian.org/ testing/updates main contrib non-free


# Unstable repo main, contrib and non-free branches, no security updates here
deb http://http.us.debian.org/debian unstable main non-free contrib
deb-src http://http.us.debian.org/debian unstable main non-free contrib
```

`apt-get update`

`apt-get upgrade`

`apt-get install apache2 apache2-mpm-event libapache2-mod-fcgid`

`apt-get install apache2-dev libpcre3 libpcre3-dev autoconf`

`apt-get install build-essential bison libbz2-dev  libpng12-dev libfreetype6-dev libgmp3-dev libmcrypt-dev libmysqlclient-dev libpspell-dev librecode-dev libxml2-dev libt1-dev libcurl4-openssl-dev libjpeg-dev libpng-dev libxpm-dev libmysqlclient-dev libpq-dev libicu-dev libfreetype6-dev libldap2-dev libxslt-dev openssl libcurl4-openssl-dev pkg-config git libtool`

`apt-get install mysql-client mysql-server`




`git clone https://github.com/php/php-src.git`

add:

`LC_ALL="en_GB.utf8"`

to /etc/environment

`cd php-src`

`./buildconf`


`./configure   --prefix=/usr/local/php   --with-apxs2=/usr/local/apache/bin/apxs   --enable-mbstring   --with-curl   --with-openssl   --with-xmlrpc   --enable-soap   --enable-zip   --with-gd   --with-jpeg-dir   --with-png-dir     --with-pgsql   --enable-embedded-mysqli   --with-freetype-dir   --enable-intl   --with-xsl  --with-apxs2=/usr/bin/apxs2 --with-mysqli --with-pdo-mysql --enable-pdo=shared --with-pdo-mysql=shared  --with-pdo-sqlite=shared `


`make`

`make install`

`ln -sf /usr/local/php/bin/php /usr/bin/php`

add to /etc/apache2/sites-enabled/000-default.conf or other vhost conf file:

`AddType application/x-httpd-php .php .phtml`

`php -v`

```
PHP 7.0.0-dev (cli) (built: Mar 30 2015 11:23:52)
Copyright (c) 1997-2015 The PHP Group
Zend Engine v3.0.0-dev, Copyright (c) 1998-2015 Zend Technologies
```

add to /usr/local/php/lib
``` 
extension=pdo.so
extension=pdo_mysql.so
```

mysql will now work, but I was not able to get it to work with 'localhost'.  I had to bind mysql to * and use the direct server IP.
