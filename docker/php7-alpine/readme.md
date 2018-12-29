### 编译
docker build -t myphp7 .

### 运行
//进入命令行模式（myphp7是镜像名称）
docker run -it --rm myphp7 sh
//进入正在运行的容器（php7-fpm是容器名称）
docker exec -it php7-fpm sh
//作为服务运行
docker run -d -p 9000:9000 -v $PWD/www:/www --name php7-fpm myphp7