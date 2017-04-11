# docker化的Phalcon框架本地开发环境
  Phalcon是个C扩展，意味着注定搭建起本地开发环境要比其他非扩展型的PHP框架麻烦很多。
  更糟心的是，好几个项目，都需要运行，却使用着不同的框架版本和PHP版本...你本地搭建一个环境试试~
  本项的目的是让大家迅速搭建一个Phalcon项目，三分钟内开发环境搞定。
## 使用前提
  使用此项目需要你首先下载docker。docker具体使用情况请见官网 [docker] (https://www.docker.com)
  使用步骤：
  + 找到某个项目的根目录下，运行：
    
    git clone https://github.com/i6448038/Phalcon_env.git docker
  
  + ``cd docker``进入到docker目录下
    
    docker-compose up -d
  
  完毕！喝杯茶等五分钟。。。然后打开``localhost``试试
  
## docker目录说明
  ``logs``目录下都是nginx运行的日志。
  ``settings``目录下是nginx的配置信息

## 镜像说明
  本项目目前的镜像有：
  + php-nginx 安装有php、Phalcon扩展和nginx的镜像
  + mysql mysql的root用户password是homestead，用户名是：homestead，密码是：secret，端口是：3306
  + redis 端口是6379

  
    

        
  
