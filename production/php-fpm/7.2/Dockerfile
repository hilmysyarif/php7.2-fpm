FROM php:7.2-fpm

# this image adds additional extensions to default php image :
# mcrypt zip pdo_mysql opcache gd memcached


MAINTAINER Hilmy Syarif <hilmysyarif@gmail.com>

RUN apt-get update -yqq \
		&& buildDeps=" \
			libz-dev  \
			libpq-dev  \
			libjpeg-dev  \
			libpng-dev  \
			libfreetype6-dev  \
			libmcrypt-dev \
            libbz2-dev \
        " \
        && doNotUninstall=" \
				libfreetype6 \
				libhashkit2 \
				libjpeg62-turbo \
				libmcrypt4 \
				libpng12-0 \
				libpq5 \
        " \
		&& DEBIAN_FRONTEND=noninteractive apt-get install -y zip bzip2 wget tar less $buildDeps --no-install-recommends apt-utils \
        && rm -r /var/lib/apt/lists/* \
        \
		&& docker-php-ext-install bcmath bz2 calendar ctype curl dba dom enchant exif fileinfo filter ftp gd gettext gmp hash iconv imap interbase intl json ldap mbstring mysqli oci8 odbc opcache pcntl pdo pdo_dblib pdo_firebird pdo_mysql pdo_oci pdo_odbc pdo_pgsql pdo_sqlite pgsql phar posix pspell readline recode reflection session shmop simplexml snmp soap sockets sodium spl standard sysvmsg sysvsem sysvshm tidy tokenizer wddx xml xmlreader xmlrpc xmlwriter xsl zend_test zip \
		&& docker-php-ext-configure gd  \
				--enable-gd-native-ttf  \
				--with-jpeg-dir=/usr/lib  \
				--with-freetype-dir=/usr/include/freetype2 &&  \
				docker-php-ext-install gd \
		&& pecl install memcached \
		&& rm -rf /tmp/pear \
		\
        && apt-mark manual $doNotUninstall \
        && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false $buildDeps