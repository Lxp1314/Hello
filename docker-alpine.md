### Dockerfile的编写

FROM alpine:latest
MAINTAINER wuyun
CMD echo "Hello Alpine"

### Dockerfile编译
docker build -t php-alpine .

### Dockerfile
docker run  -it php-alpine sh
