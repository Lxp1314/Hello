### Dockerfile的编写

```
FROM alpine:latest
MAINTAINER wuyun
WORKDIR /app
CMD echo "Hello Alpine"

说明：
WORKDIR /app 使用docker run -it imageName sh进入容器后默认的位置，WORKDIR指定的目录不存在时会自动创建
```


### Dockerfile编译
docker build -t php-alpine .

### Dockerfile
docker run  -it php-alpine sh
