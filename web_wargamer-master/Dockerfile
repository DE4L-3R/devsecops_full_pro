FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Seoul

WORKDIR /var/www/html

# Apache와 PHP 패키지만 설치
RUN apt-get update && apt-get install -y \
    apache2 \
    php \
    php-cli \
    php-fpm \
    php-mysql \
    php-json \
    php-opcache \
    php-xml \
    && apt-get clean

# Apache 모듈 설정
RUN a2enmod proxy && \
    a2enmod proxy_fcgi && \
    a2enmod proxy_http

# Apache 설정
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf && \
    echo "ProxyPassMatch ^/(.*\.php(/.*)?)$ fcgi://127.0.0.1:9000/var/www/html/$1" >> /etc/apache2/apache2.conf

# PHP 설정
RUN sed -i 's/;date.timezone =/date.timezone = Asia\/Seoul/g' /etc/php/7.4/cli/php.ini && \
    mkdir -p /run/php && \
    sed -i 's/listen = \/run\/php\/php7.4-fpm.sock/listen = 127.0.0.1:9000/g' /etc/php/7.4/fpm/pool.d/www.conf

# 웹 소스 파일 복사 및 권한 설정
COPY web/ /var/www/html/
RUN chown -R www-data:www-data /var/www/html && \
    chmod -R 755 /var/www/html

# 시작 스크립트 생성
RUN printf '#!/bin/bash\n\
/usr/sbin/php-fpm7.4 &\n\
/usr/sbin/apache2ctl -D FOREGROUND' > /start.sh && \
chmod +x /start.sh

CMD ["/start.sh"]
