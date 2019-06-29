# docker_php7.0.7

- 本项目包含构建 php7.0.7 镜像的源文文件； 
- docker image 地址：[wenzhi/php7.0.7](https://cloud.docker.com/repository/docker/wenzhi/php7.0.7)

## 拓展
[PHP Modules]     
amqp
apcu
bcmath
calendar
Core
ctype
curl
date
dom
filter
ftp
gd
gettext
hash
iconv
imagick
json
libxml
mbstring
mcrypt
mongodb
mysqli
mysqlnd
openssl
pcntl
pcre
PDO
pdo_mysql
pdo_sqlite
pdo_sqlsrv
Phar
posix
rdkafka
redis
Reflection
session
shmop
SimpleXML
soap
sockets
SPL
sqlite3
sqlsrv
standard
swoole
sysvmsg
sysvsem
sysvshm
tokenizer
xhprof
xml
xmlreader
xmlrpc
xmlwriter
Zend OPcache
zip
zlib
zookeeper

[Zend Modules]     
Zend OPcache

## 使用方式
### php-fpm :  
nginx conf :    
```
    location ~ \.php$ {
        fastcgi_pass     0.0.0.0:9009;
        fastcgi_param   SCRIPT_FILENAME /var/www_data$fastcgi_script_name;
        include         fastcgi_params;
        try_files $uri =404;
    }
```  
docker run -p9009:9000 -v /your-php-file-path:/var/www_data -d phpdockerio/php7-fpm
### php-cli :
alias docker_php='docker run -it --rm --name php -v $PWD:/usr/src/myapp -w /usr/src/myapp wenzhi/php7.0.7 php'      
docker_php test.php
