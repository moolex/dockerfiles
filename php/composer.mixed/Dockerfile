FROM composer

RUN composer global require hirak/prestissimo
RUN composer global require squizlabs/php_codesniffer
RUN composer global require phpstan/phpstan
RUN composer global require phpunit/phpunit

RUN composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/

ENV PATH="${PATH}:${COMPOSER_HOME}/vendor/bin"
