From wenzhi/centos7-systemd
MAINTAINER wenzhi

ADD ./package /usr/local
RUN cd /usr/local && tar -zxvf pdo_sqlsrv-5.2.0.tgz && \
    tar -zxvf php-7.0.7.tar.gz && \
    tar -zxvf sqlsrv-5.2.0.tgz && \
    tar -zxvf zookeeper-lib.tar.gz && \
    rm -f pdo_sqlsrv-5.2.0.tgz php-7.0.7.tar.gz sqlsrv-5.2.0.tgz zookeeper-lib.tar.gz && \
    cd /usr/local/exts && \
    tar -zxvf apcu-5.1.8.tgz && \
    tar -zxvf mongodb-1.1.6.tgz && \
    tar -zxvf pdo_sqlsrv-5.2.0.tgz && \
    tar -zxvf sqlsrv-5.2.0.tgz && \
    tar -zxvf zookeeper-0.4.0.tgz && \
    tar -zxvf rdkafka-3.0.5.tgz && \
    tar -zxvf swoole-1.7.21.tgz && \
    tar -zxvf imagick-3.4.3.tgz && \
    tar -zxvf redis-3.1.2.tgz && \
    tar -zxvf rabbitmq-c-0.8.0.tar.gz && \
    tar -zxvf librdkafka-master.tgz && \
    tar -zxvf amqp-1.9.4.tgz && \
    rm -f apcu-5.1.8.tgz mongodb-1.1.6.tgz pdo_sqlsrv-5.2.0.tgz sqlsrv-5.2.0.tgz zookeeper-0.4.0.tgz rdkafka-3.0.5.tgz swoole-1.7.21.tgz imagick-3.4.3.tgz  redis-3.1.2.tgz librdkafka-master.tgz && \
    rm -f rabbitmq-c-0.8.0.tar.gz amqp-1.9.4.tgz

RUN yum install -y perl pcre-devel openssl-devel gcc curl gcc-c++ autoconf automake libtool make wget deltarpm libxml2 libxml2-devel curl-devel libjpeg-devel libpng-devel && \
    yum install freetype-devel -y && \
    yum install -y epel-release && \
    yum install -y libmcrypt-devel ImageMagick-devel && \
    cd /usr/local/php-7.0.7 && \
    ./configure  --prefix=/usr/local/php7.0.7 --with-config-file-path=/usr/local/php7.0.7/etc --enable-fpm --with-mcrypt=/usr/include --enable-mysqlnd --with-gd --with-iconv --with-zlib --enable-bcmath --enable-sysvshm --enable-shmop --enable-opcache --enable-sysvmsg --enable-sysvsem --enable-inline-optimization --enable-mbregex --enable-xml --enable-mbstring --enable-gd-native-ttf --enable-pcntl --enable-sockets --with-xmlrpc --enable-zip --enable-ftp --enable-soap --with-gettext --with-curl --with-jpeg-dir --with-freetype-dir --enable-embedded-mysqli --with-pdo-mysql --disable-debug --disable-fileinfo --with-mysqli --with-pcre-regex --with-openssl --with-mhash --with-imap-ssl

RUN cd /usr/local/php-7.0.7 && \
    make -j3 && make install 

RUN cp /usr/local/php-7.0.7/php.ini-development /usr/local/php7.0.7/etc/php.ini && \
    cp /usr/local/php-7.0.7/sapi/fpm/init.d.php-fpm.in /etc/init.d/php-fpm && \
    cp /usr/local/php-7.0.7/sapi/fpm/www.conf /usr/local/php7.0.7/etc/php-fpm.d/ && \
    cp /usr/local/php7.0.7/etc/php-fpm.conf.default /usr/local/php7.0.7/etc/php-fpm.conf && \
    sed -i "s/user = nobody/user = nginx/g" /usr/local/php7.0.7/etc/php-fpm.d/www.conf && \
    sed -i "s/group = nobody/group = nginx/g" /usr/local/php7.0.7/etc/php-fpm.d/www.conf && \
    sed -i "s/expose_php = On/expose_php = Off/g" /usr/local/php7.0.7/etc/php.ini && \
    sed -i "s/variables_order = \"GPCS\"/variables_order = \"EGPCS\"/g" /usr/local/php7.0.7/etc/php.ini && \
    sed -i "s/; max_input_vars = 1000/max_input_vars = 5000/g" /usr/local/php7.0.7/etc/php.ini && \
    sed -i "s/error_reporting = E_ALL/error_reporting = E_ALL \& ~E_DEPRECATED \& ~E_STRICT/g" /usr/local/php7.0.7/etc/php.ini && \
    sed -i "s/upload_max_filesize = 2M/upload_max_filesize = 8M/g" /usr/local/php7.0.7/etc/php.ini && \
    sed -i "/;extension=php_xsl.dll/a\extension=amqp.so" /usr/local/php7.0.7/etc/php.ini && \
    sed -i "/;extension=php_xsl.dll/a\extension=apcu.so" /usr/local/php7.0.7/etc/php.ini && \
    sed -i "/;extension=php_xsl.dll/a\extension=zookeeper.so" /usr/local/php7.0.7/etc/php.ini && \
    sed -i "/;extension=php_xsl.dll/a\extension=swoole.so" /usr/local/php7.0.7/etc/php.ini && \
    sed -i "/;extension=php_xsl.dll/a\extension=redis.so" /usr/local/php7.0.7/etc/php.ini && \
    sed -i "/;extension=php_xsl.dll/a\extension=mongodb.so" /usr/local/php7.0.7/etc/php.ini && \
    sed -i "/;extension=php_xsl.dll/a\extension=imagick.so" /usr/local/php7.0.7/etc/php.ini && \
    sed -i "/;extension=php_xsl.dll/a\extension=rdkafka.so" /usr/local/php7.0.7/etc/php.ini && \
    sed -i "/;extension=php_xsl.dll/a\extension=calendar.so" /usr/local/php7.0.7/etc/php.ini && \
    sed -i "/;extension=php_xsl.dll/a\extension=pdo_sqlsrv.so" /usr/local/php7.0.7/etc/php.ini && \
    sed -i "/;extension=php_xsl.dll/a\extension=sqlsrv.so" /usr/local/php7.0.7/etc/php.ini && \
    sed -i "/;extension=php_xsl.dll/a\extension=xhprof.so" /usr/local/php7.0.7/etc/php.ini && \
    sed -i "/;extension=php_xsl.dll/a\zend_extension=opcache.so" /usr/local/php7.0.7/etc/php.ini && \
    sed -i "s/;date\.timezone =/date\.timezone = \"Asia\/Shanghai\"/g" /usr/local/php7.0.7/etc/php.ini && \
    cp  /usr/local/exts/opcache.so  `/usr/local/php7.0.7/bin/php -r "phpinfo();" |grep 'extension_dir => /usr' | awk '{print $3}'` && \
    cp  /usr/local/exts/opcache.a  `/usr/local/php7.0.7/bin/php -r "phpinfo();" |grep 'extension_dir => /usr' | awk '{print $3}'` && \
    cp  /usr/local/exts/calendar.so  `/usr/local/php7.0.7/bin/php -r "phpinfo();" |grep 'extension_dir => /usr' | awk '{print $3}'` && \
    cp  /usr/local/exts/xhprof.so  `/usr/local/php7.0.7/bin/php -r "phpinfo();" |grep 'extension_dir => /usr' | awk '{print $3}'`

RUN cd /usr/local/exts/imagick-3.4.3 && /usr/local/php7.0.7/bin/phpize && \
    ./configure --with-php-config=/usr/local/php7.0.7/bin/php-config --prefix=/usr/local/imagemagick && \
    make -j3 && make install
RUN cd /usr/local/exts/librdkafka-master && ./configure && \
    make -j3 && make install
RUN cd /usr/local/exts/rabbitmq-c-0.8.0 && ./configure --prefix=/usr/local/rabbitmq-c && \
    make -j3 && make install
RUN cd /usr/local/exts/amqp-1.9.4 && \
    /usr/local/php7.0.7/bin/phpize && \
    ./configure --with-php-config=/usr/local/php7.0.7/bin/php-config --with-amqp --with-librabbitmq-dir=/usr/local/rabbitmq-c && \
    make -j3 && make install
RUN cd /usr/local/exts/rdkafka-3.0.5 && \
    /usr/local/php7.0.7/bin/phpize && \
    ./configure --with-php-config=/usr/local/php7.0.7/bin/php-config --with-rdkafka && \
    make -j3 && make install
RUN cd /usr/local/exts/apcu-5.1.8 && /usr/local/php7.0.7/bin/phpize && \
    ./configure --with-php-config=/usr/local/php7.0.7/bin/php-config && \
    make -j3 && make install
RUN cd /usr/local/exts/mongodb-1.1.6 && /usr/local/php7.0.7/bin/phpize && \
    ./configure --with-php-config=/usr/local/php7.0.7/bin/php-config && \
    make -j3 && make install
RUN cd /usr/local/exts/redis-3.1.2 && /usr/local/php7.0.7/bin/phpize && \
    ./configure --with-php-config=/usr/local/php7.0.7/bin/php-config && \
    make -j3 && make install && \
    cd  /usr/local/exts/zookeeper-0.4.0 && /usr/local/php7.0.7/bin/phpize && \
    ./configure --with-php-config=/usr/local/php7.0.7/bin/php-config --with-libzookeeper-dir=/usr/local/zookeeper-lib && \
    make -j3 && make install
RUN cd /usr/local/exts/swoole-1.7.21 && /usr/local/php7.0.7/bin/phpize && \
    ./configure --with-php-config=/usr/local/php7.0.7/bin/php-config && \
    make -j3 && make install
RUN yum install unixODBC-devel -y && \
    cd /usr/local/exts/pdo_sqlsrv-5.2.0 && /usr/local/php7.0.7/bin/phpize && \
    ./configure --with-php-config=/usr/local/php7.0.7/bin/php-config && \
    make -j3 && make install
RUN cd  /usr/local/exts/sqlsrv-5.2.0 && /usr/local/php7.0.7/bin/phpize && \
    ./configure --with-php-config=/usr/local/php7.0.7/bin/php-config && \
    make -j3 && make install
RUN groupadd nginx && \
    useradd nginx -g nginx && \
    strip /usr/local/php7.0.7/bin/php && \
    strip /usr/local/php7.0.7/bin/php-cgi && \
    strip /usr/local/php7.0.7/sbin/php-fpm && \
    sed -i "s/prefix=@prefix@/#prefix=@prefix@/g" /etc/init.d/php-fpm && \
    sed -i "s/exec_prefix=@exec_prefix@/#exec_prefix=@exec_prefix@/g" /etc/init.d/php-fpm && \
    sed -i "s/php_fpm_BIN=@sbindir@\/php-fpm/php_fpm_BIN=\/usr\/local\/php7\.0\.7\/sbin\/php-fpm/g" /etc/init.d/php-fpm && \
    sed -i "s/php_fpm_CONF=@sysconfdir@\/php-fpm.conf/php_fpm_CONF=\/usr\/local\/php7\.0\.7\/etc\/php-fpm\.conf/g" /etc/init.d/php-fpm && \
    sed -i "s/php_fpm_PID=@localstatedir@\/run\/php-fpm\.pid/php_fpm_PID=\/var\/run\/php-fpm\.pid/g" /etc/init.d/php-fpm && \
    sed -i "s/;error_log = log\/php-fpm\.log/error_log = \/var\/log\/php-fpm\.log/" /usr/local/php7.0.7/etc/php-fpm.conf && \
    sed -i "s/listen = 127\.0\.0\.1\:9000/listen = 0\.0\.0\.0\:9000/g" /usr/local/php7.0.7/etc/php-fpm.d/www.conf && \
    chmod a+x /etc/init.d/php-fpm && \
    rm -rf /usr/local/exts && \
    rm -rf /usr/local/php-7.0.7 && \
    yum erase wget deltarpm autoconf automake make gcc gcc-c++ -y && \
    cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    yum clean all 

ENV YII_ENV=dev
ENV PATH=$PATH:/usr/local/php7.0.7/bin
ENV PATH=$PATH:/usr/local/php7.0.7/sbin

#启动php70
CMD /etc/init.d/php-fpm start && tail -f /dev/null
EXPOSE 9000
