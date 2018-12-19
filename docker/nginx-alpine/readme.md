```
编译
docker build -t mynginx .

运行
//进入命令行模式（mynginx是镜像名称）
docker run -it mynginx sh
//进入正在运行的容器（nginx是容器名称）
docker exec -it nginx sh
//直接运行（mynginx是镜像名称）
docker run -d -p 80:80 mynginx
//将当前目录下的www目录映射到容器的/www目录
docker run -d -p 80:80 -v $PWD/www:/www mynginx
//映射目录并指定容器名称
docker run -d -p 80:80 -v $PWD/www:/www --name nginx mynginx

```