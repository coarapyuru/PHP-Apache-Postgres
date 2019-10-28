# PHP7.2 & Apache2.4 イメージをダウンロード
FROM php:7.2-apache

# 不要なパッケージを削除
RUN apt-get clean
RUN apt-get -y autoremove

# パッケージ最新化
RUN apt-get update

# Zipをインストール
RUN apt-get install -y libzip-dev zip && docker-php-ext-configure zip --with-libzip && docker-php-ext-install zip

# Curlをインストール
RUN apt-get install -y libcurl3-dev curl && docker-php-ext-install curl

# vim less インストール
RUN apt-get install -y vim less

# Postgres関連パッケージインストール
RUN set -ex apk --no-cache add postgresql-dev libpq-dev
RUN apt-get install -y libpq-dev \
    && docker-php-ext-install pdo pdo_pgsql pgsql mbstring

# Xdebugをインストール
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug

# Composerをインストール
ENV COMPOSER_ALLOW_SUPERUSER 1
RUN php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer
RUN chmod 0755 /usr/bin/composer

# php.iniをコピー
COPY ./php.ini /usr/local/etc/php/php.ini

# httpd.confをコピー
COPY ./httpd.conf /usr/local/apache2/conf/httpd.conf

# パッケージをクリーンアップ
RUN apt-get clean
RUN apt-get -y autoremove
