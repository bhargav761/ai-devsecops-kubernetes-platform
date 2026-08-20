FROM openresty/openresty:alpine-fat

RUN apk update && apk upgrade curl libcurl

COPY default.conf /etc/nginx/conf.d/default.conf

RUN mkdir -p /etc/nginx/conf.d/lua

COPY lua/agg.lua /etc/nginx/conf.d/lua
