## 一 window 运行补充

1. MongoDB  容器启动问题
    - 【docker-compose.yml】 volume 映射关系使用 虚拟磁盘卷 - virtual_mongo:/data/db:rw （使用- ${DATA_DIR}/mongo:/data/db:rw  会报错）
    -  mysql 容器再 wsl 2 的环境下， 也会出现 容器不断重启问题

2. 访问网站提示 文件未找到
    - 【docker-compose.yml】 SOURCE_DIR 映射问题 - ${SOURCE_DIR}:/var/www/:rw （使用 - ${SOURCE_DIR}:/www/:rw  会出现 访问网站提示 文件未找到）

3. 在加了extra_hosts 容器中ping不通域名
    - 【docker-compose.yml】原因是加了多的空格  正确应该是这样"pro.mjngs.com:${HOST}"，可能和alpine有关更加严格 （"pro.mjngs.com : ${HOST}"  这种解析直接是 127.0.0.1）

4. 关于alpine linux（超轻量级的发行版） ，如果镜像选的是 PHP_VERSION: php:${PHP_VERSION}-fpm-alpine, 他linux就是alpine，即相关服务、扩展都需要是alpine版本
    - 比如【redis:5.0.3-alpine memcached:alpine  以及 wkhtmltopdf 等】
    
5. 请求超时问题
    - 建议不要使用 nginx.back.conf  配置存在些问题  

6. 初始化配置说明
    - .env                  参考env.dev                     [HOST  SOURCE_DIR]
    - docker-compose.yml    参考 docker-compose.dev.yml
    - conf.d

7. 容器 mysql8  使用Navicat连接报2059错误
    - 原因： mysql8 之前的版本中加密规则是mysql_native_password，而在mysql8之后加密规则是caching_sha2_password，navicat驱动目前不支持新加密规则
    - 解决方案：进入mysql容器  mysql -uroot -pmima      ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'root';

## 二 待处理事项

1. supervisor 容器了解

2. ffmpeg https 

## 三 常用命令
1. php容器相关
    netstat -taupln | grep 'php'
    netstat -lntup | grep 9000
        
    ps -ef | grep php-fpm   查看php-fpm所有的进程

    ps -ef | grep php-fpn.conf 查看配置所在路径

    pkill php-fpm
    php-fpm -R
2. bash: whereis: command not found
    #Debian
    apt-get install util-linux
    
    #Ubuntu
    apt-get install util-linux
    
    #Alpine
    apk add util-linux
    
    #Arch Linux
    pacman -S util-linux
    
    #Kali Linux
    apt-get install util-linux
    
    #CentOS
    yum install util-linux
    
    #Fedora
    dnf install util-linux
    
    #OS X
    brew install util-linux
    
    #Raspbian
    apt-get install util-linux
    
    #Docker
    docker run cmd.cat/whereis whereis
