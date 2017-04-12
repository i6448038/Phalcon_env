# docker化的Phalcon框架本地开发环境
  Phalcon是个C扩展，意味着注定搭建起本地开发环境要比其他非扩展型的PHP框架麻烦很多。
  更糟心的是，好几个项目，都需要运行，却使用着不同的框架版本和PHP版本...你本地搭建一个环境试试~
  本项的目的是让大家迅速搭建一个Phalcon项目，三分钟内开发环境搞定。
## 使用前提
  使用此项目需要你首先下载docker。docker具体使用情况请见官网 [docker](https://www.docker.com)
  使用步骤：
  + 找到某个项目的根目录下，运行：
    
    ```git clone https://github.com/i6448038/Phalcon_env.git docker```
  
  + ``cd docker``进入到docker目录下
    
    ```docker-compose up -d```
  
  完毕！喝杯茶等五分钟。。。然后打开``localhost``试试
  
## docker目录说明
  ``logs``目录下都是nginx运行的日志。
  ``settings``目录下是nginx的配置信息

## 镜像说明
  本项目目前的镜像有：
  + php-nginx 安装有php、Phalcon扩展和nginx的镜像
  + 代码存放在php-nginx 容器中，一进入容器就可看到代码。此容器和redis、mysql、mongo、memcached建立了连接。连接地址分别是``redis``、
  ``mysql``、``mongo``和``memcached``。（PS：假如想要访问redis,那么配置文件中redis的host地址就得写redis）
  + mysql mysql的root用户password是homestead，用户名是：homestead，密码是：secret，端口是：3306
  + redis 端口是6379
  + memcached 端口是11211
  + mongoDB 端口是 27137

## 配置说明
  + 代码存放在php-nginx 容器中，一进入容器就可看到代码。此容器和redis、mysql、mongo、memcached建立了连接。连接地址分别是``redis``、
   ``mysql``、``mongo``和``memcached``。（PS：假如想要访问redis,那么配置文件中redis的host地址就得写redis）
  + 假如想要同时启动多个项目，需要自己修改docker-compose.yml文件中的每一个的``container_name``容器名字，和``ports``端口号的前半部分，例如我项目名字叫hello，我可以改成:
    ```###########################################################
       #      MAINTAINER: Ryu Gou <376832293@qq.com>         #
       ###########################################################
       
       # PHP + NGINX Container #----------------------------------
       php-nginx:
         image: ryugou/jiyu_phalcon:2.0
         container_name: hello_php-nginx
         ports:
           - "80:80"
           - "443:443"  
         volumes:
           - ./settings/nginx:/etc/nginx/sites-available
           - ../:/var/www
           - ./logs/nginx:/var/log/nginx
         links:
           - mysql
           - redis
           - memcached  
         environment:
           - REDIS_PORT=6379
       
       # MySQL Container #----------------------------------------
       mysql:
         image: mysql:5.6
         container_name: hello_mysql
         ports:
           - "3306:3306"
         environment:
           MYSQL_ROOT_PASSWORD: homestead
           MYSQL_DATABASE: homestead
           MYSQL_USER: homestead
           MYSQL_PASSWORD: secret
       
       # Redis Container #----------------------------------------
       redis:
         image: redis:3.0
         container_name: hello_redis
         ports:
           - "6379:6379"
       
       # Memcached Container #---------------------------------
       memcached:
         image: memcached:1.4
         container_name: hello_memcached
         ports:
           - "11211:11211"
         mem_limit: 1g ```
      
      这样我就把每个容器的名字改为了前缀"hello"，就避免了容器名字重复，同时，假如说有端口号占用，比方说redis，我只要把``ports``中的``- "6379:6379"``前半部分6379改为别的就可以了：
      ``- "63791:6379"``         

## 其他
  想要切换其他版本的Phalcon可以切一下git分之  
         
         
         
           
         
           
       
               
         
