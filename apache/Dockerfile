# https://github.com/docker-library/docs/blob/master/php/README.md#with-apache
FROM php:7.2-apache
COPY 000-default.conf /etc/apache2/sites-enabled/
COPY spotloader-node.ini /home/spotloader/.spotloader-globosat-node.ini
ADD simplesamlphp.tar.gz /home/spotloader/

# Enable mod rewrite apache
RUN a2enmod rewrite

### Additional apt packages ###
RUN apt-get update \
        && apt-get install -y libicu-dev \
        libxml2-dev \
        libxslt-dev \
	libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libgd-dev \
	libgmp-dev \
	libbz2-dev \
        zlib1g-dev \
	libssl-dev \
	locales \
	vim

# gmp lib fix
RUN ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/include/gmp.h

# Locales
RUN sed -i 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen \
	&& sed -i 's/# pt_BR.UTF-8 UTF-8/pt_BR.UTF-8 UTF-8/' /etc/locale.gen \
	&& sed -i 's/# pt_BR ISO-8859-1/pt_BR ISO-8859-1/' /etc/locale.gen \
	&& locale-gen

# PHP extensions
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install -j$(nproc) \
	mysqli \
	pdo \
	pdo_mysql \
	gettext \
	mbstring \
	dom \
	xmlrpc \
	xsl \
	gd \
	exif \
	gmp \
	bcmath \
	zip \
	bz2 \
	ftp


## ssh2
#RUN apt-get update \
#	&& apt-get install -y \
#	libssh2-1-dev
#
## memcached
#RUN apt-get update \
#	&& apt-get install -y \
#	libmemcached-dev \
#	libmemcached11
#
#
## others
#RUN docker-php-ext-install -j$(nproc) \
#	soap \
#	sockets \
#	calendar \
#	sysvmsg \
#	sysvsem \
#	sysvshm
#
## PECL
#RUN docker-php-pecl-install \
#	ssh2-1.1.2 \
#	redis-4.0.2 \
#	apcu-5.1.11 \
#	memcached-3.0.4
