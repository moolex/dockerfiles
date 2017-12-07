FROM php:7.1-cli-alpine

LABEL MAINTAINER Shiyu Han <dock@moyo.im>

# Ext versions
ENV PROTOBUF_VER=3.4.0
ENV SWOOLE_VER=1.9.23

# Add depends for runtime
RUN apk add --update \
    hiredis

# Add depends for building
RUN apk add --update --virtual builds \
    linux-headers \
    hiredis-dev \
    openssl-dev \
    libc-dev \
    pcre-dev \
    autoconf \
    re2c \
    make \
    gcc \
    g++ \
    gc

# Ext protobuf
RUN curl -sS -o /tmp/protobuf.tar.gz http://pecl.php.net/get/protobuf-$PROTOBUF_VER.tgz \
    && cd /tmp/ && tar zxvf protobuf.tar.gz && cd protobuf-$PROTOBUF_VER \
    && phpize && ./configure && make && make install \
    && docker-php-ext-enable protobuf

# Ext swoole
RUN curl -sS -o /tmp/swoole.tar.gz http://pecl.php.net/get/swoole-$SWOOLE_VER.tgz \
    && cd /tmp/ && tar zxvf swoole.tar.gz && cd swoole-$SWOOLE_VER \
    && phpize \
    && ./configure --enable-async-redis --enable-mysqlnd --enable-openssl \
    && make && make install \
    && docker-php-ext-enable swoole

# Cleanup
RUN apk del builds && rm -rf /var/cache/apk/* /tmp/*

VOLUME ["/app"]

WORKDIR "/app"
