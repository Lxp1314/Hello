FROM alpine:latest
MAINTAINER wuyun

WORKDIR /www

RUN echo 'https://mirrors.aliyun.com/alpine/v3.6/main/' > /etc/apk/repositories
RUN echo 'https://mirrors.aliyun.com/alpine/v3.6/community/' >> /etc/apk/repositories
RUN apk update && apk add curl
RUN apk add nginx
RUN mkdir -p /run/nginx && touch /run/nginx/nginx.pid

RUN mkdir html && touch html/index.html && echo 'Hello Nginx~' > html/index.html

COPY nginx.conf /etc/nginx/nginx.conf
COPY conf.d/default.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]