FROM webdevops/php-nginx:8.2-alpine

LABEL description="Keep configuration secure"

LABEL version="1.0"

LABEL author="meulody"

RUN echo "Asia/Ho_Chi_Minh" > /etc/timezone

ENV WEB_DOCUMENT_ROOT=/app

RUN echo "memory_limit = 512 M" >> /opt/docker/etc/php/php.ini

COPY ./nginx/nginx.conf /opt/docker/etc/nginx/main.conf

WORKDIR /app

COPY --chown=www-data:www-data ./craftcms /app

RUN composer2 install -d /app \
    &&  chown -R www-data:www-data /app/vendor \
    && chown -R www-data:www-data /app/composer.lock \
    && chmod 777 /app/storage

CMD php craft up