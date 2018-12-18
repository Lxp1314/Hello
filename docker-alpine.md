FROM alpine:latest
MAINTAINER wuyun
CMD echo "Hello Alpine"

docker build -t php-alpine .

 docker run  -it php-alpine sh
