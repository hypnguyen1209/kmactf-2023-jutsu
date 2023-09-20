FROM webdevops/php:8.2-alpine

LABEL description="Keep configuration secure"

LABEL version="1.0"

LABEL author="meulody"

ENV TZ=Asia/Ho_Chi_Minh

ENV WEB_DOCUMENT_ROOT=/app

RUN echo "max_execution_time = 250" >> /opt/docker/etc/php/php.webdevops.ini 

WORKDIR /app

COPY --chown=www-data:www-data ./craftcms /app

RUN composer2 require -d /app nystudio107/craft-twigprofiler:4.0.0-beta.1 -w 

RUN composer2 install -d /app \
    &&  chown -R www-data:www-data /app/vendor \
    && chown -R www-data:www-data /app/composer.lock \
    && chmod 777 /app/storage

RUN composer require -d /app nystudio107/craft-twigprofiler:4.0.0-beta.1 -w 

EXPOSE 8080

CMD (php craft serve "0.0.0.0:8080" >/tmp/nothing_payload_in_here.log 2>&1 &) && /opt/docker/bin/service.d/supervisor.sh