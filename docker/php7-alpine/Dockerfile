FROM alpine:latest
MAINTAINER wuyun

WORKDIR /www

RUN echo 'https://mirrors.aliyun.com/alpine/v3.6/main/' > /etc/apk/repositories
RUN echo 'https://mirrors.aliyun.com/alpine/v3.6/community/' >> /etc/apk/repositories

RUN apk update
# 安装php7-fpm和扩展
RUN apk add php7 php7-fpm \
         php7-mysqli php7-pdo_mysql \
         php7-mbstring php7-json \
         php7-zlib php7-gd php7-intl \
         php7-session php7-openssl \
         php7-tokenizer php7-xml \
         php7-ctype php7-soap \
         php7-phar php7-dom

# 安装composer
RUN apk add curl
RUN curl -s http://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer
# 配置国内composer镜像
RUN composer config -g repo.packagist composer https://packagist.phpcomposer.com

#安装supervisor
RUN apk add supervisor
RUN mkdir /etc/supervisor.d

COPY php.ini /etc/php7/php.ini

EXPOSE 9000

CMD ["php-fpm7"]

