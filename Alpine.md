### alpine安装
下载地址：http://dl-cdn.alpinelinux.org/alpine/v3.6/releases/x86_64/alpine-standard-3.6.2-x86_64.iso
安装时能默认配置就默认配置，完成后重启

安装成功后登陆系统需要密码

修改国内镜像
vi /etc/apk/repositories
加入：https://mirrors.aliyun.com/alpine/v3.6/main/
https://mirrors.aliyun.com/alpine/v3.6/community/

更新一下软件包索引文件
apk update

安装curl库
apk add curl

搜索软件包
apk search xx

删除已安装软件包
apk del xxx

帮助
apk --help

配置root用户ssh
vi /etc/ssh/sshd_config
加入 PermitRootLogin yes
重启系统即可用xshell连接
reboot

### nginx安装
apk add nginx

启动nginx
/usr/sbin/nginx 或者
/etc/init.d/nginx start

修改配置
vi /etc/nginx/conf.d/default.conf 
server {
        listen 80 default_server;
        listen [::]:80 default_server;

        # Everything is a 404
        location / {
            index index.html;
            root /www/html;
        }

        # You may need this to prevent return 404 recursion.
        location = /404.html {
                internal;
        }
}

重启nginx
nginx -s reload
（有可能报nginx: [error] open() "/run/nginx/nginx.pid" failed (2: No such file or directory)的错，使用/etc/init.d/nginx restart重启）

创建文件夹并写入index.html
mkdir /www/html
vi index.html

访问
curl http://127.0.0.1

### php7安装
apk add php7
（安装成功后使用php -v查看php版本实际是7.1.17）

安装扩展
apk add php7-fpm php7-mysqli php7-pdo_mysql php7-mbstring php7-json php7-zlib php7-gd php7-intl php7-session php7-openssl php7-tokenizer php7-xml php7-ctype php7-soap php7-phar php7-dom

配置文件路径
/etc/php7/php.ini
/etc/php7/conf.d/*.ini

### composer安装
curl -s http://getcomposer.org/installer | php
会下载一个composer.phar的文件，将它移动到/usr/local/bin/就可以全局调用
mv composer.phar /usr/local/bin/composer

配置国内镜像
composer config -g repo.packagist composer https://packagist.phpcomposer.com

composer创建laravel项目
/www# composer create-project laravel/laravel laravel51 --prefer-dist "5.1.*"

创建laravel项目的nginx配置文件
cp /etc/nginx/conf.d/default.conf /etc/nginx/conf.d/laravel51.conf
修改配置
server {
        listen 8080 default_server;

        root /www/laravel51/public;
        index index.php index.html;

        # Everything is a 404
        location / {
            try_files $uri $uri/ /index.php?$query_string;
        }

        location ~ \.php {
            fastcgi_pass                  127.0.0.1:9000;
            fastcgi_index                 /index.php;
            fastcgi_split_path_info       ^(.+\.php)(/.+)$;
            fastcgi_param PATH_INFO       $fastcgi_path_info;
            fastcgi_param PATH_TRANSLATED $document_root$fastcgi_path_info;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
            include                       fastcgi_params;
        }

        location ~* ^/(css|img|js|flv|swf|download)/(.+)$ {

        }

        location ~ /\.ht {
            deny all;
        }
}

配置完成后启动php-fpm和重启nginx
nginx -s stop （如果nginx已启动，先停掉）
/usr/sbin/php-fpm7 （php先启动）
/usr/sbin/nginx （nginx后启动）

访问
curl http://127.0.0.1:8080

### mysql安装
apk add mysql
/etc/init.dmariadb setup

参考
http://www.zzfly.net/alpine-linux-php-mysql/
https://segmentfault.com/a/1190000014350195
https://www.jb51.net/article/150666.htm
