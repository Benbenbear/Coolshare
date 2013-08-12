__LAMP__，顾名思义就是`Linux+Apache+MySQL+PHP`的组合。通常这套组合更适宜在`linux`环境下搭建，因为`Apache`，`MySQL`和`PHP`最初都是在`Unix`或者`Linux`下开发运行的，后来才慢慢转移到`Windows`下的，并且在`Linux`下的运行效率更高，很多的第三方软件只支持`Unix`和`Linux`。本文主要以`Scientific Linux`（SL也是基于RHEL的发行的）为例，其他的像`centos`，`ubuntu`，`debian`系列的等等都可以参考本文进行安装。
在SL下安装有二进制软件包（rpm包）和源代码包两种方式，因为二进制包的可定制性不是很强，并且看不到源码。所以推荐大家使用源代码包安装，可以先到官方网站下载相应的软件，搭建`LAMP`环境相对较复杂，大概需要安装以下13个软件。搭建LAMP环境不一定要是最新的软件，重要的是稳定性。
```
[benbenbear@wanghs lamp]$ ls | awk '1'
autoconf-2.61.tar.gz
freetype-2.3.5.tar.gz
gd-2.0.35.tar.gz
httpd-2.2.9.tar.gz
jpegsrc.v6b.tar.gz
libmcrypt-2.5.8.tar.gz
libpng-1.2.31.tar.gz
libxml2-2.6.30.tar.gz
mysql-5.0.41.tar.gz
php-5.2.6.tar.gz
phpMyAdmin-3.0.0-rc1-all-languages.tar.gz
ZendOptimizer-3.2.6-linux-glibc21-i386.tar.gz
zlib-1.2.3.tar.gz
[benbenbear@wanghs lamp]$
```
然后依次对这些`*.tar.gz`文件进行解压，但是我个人比较懒，可以写一个简短的脚本`tar.sh`来替我们完成这个工作。
``` 
cd ~/lamp
ls *.tar.gz > ls.list

for TAR in `cat ls.list`
do
tar -zxf $TAR
done
```
然后运行 `sh -x tar.sh` 即可完成全部的解压缩过程。           
在正式安装之前应该确保当前系统安装了`make` ，`gcc`，`gcc-c++`三个编译工具，通常make都是安装的，倘若没有安装gcc,gcc-c++,最好使用`yum installgcc,yum install gcc-c++`来安装，因为它会自动解决依赖关系的问题，比rpm省事的多。假如你的linux实在Vmware或者单机的情况下使入互联网，也可以修改yum的配置文件`/etc/yum.repos.d/` 让其去你的镜像或者光盘搜索yum源而不是到互联网上去搜索。具体步骤在这里就不详细阐述了。     
当安装好编译工具之后，就是要确保防火墙和SElinux先关闭，倘若你还没有安装linux，建议你在安装时选择先禁用SElinux和防火墙，如果你已经安装好了，也可以参考下面的方法先禁用。`service iptables stop`或者`iptables -F` (禁用Netfilter iptables或者删除防火墙规则，因为默认是把80端口禁用的，如果不先关闭，有可能安装完了也没办法正常测试，这并不是我们想看到的情况)。至于SElinux可以修改`/etc/sysconfig/selinux`下面的配置文件，将其中的`SELINUX=enforcing`修改为`disabled`，重启Linux就会生效。

最后一个准备工作就是把系统上原先有的Apache,MySQL和PHP先卸载了，因为你不可能同时启动两个Apache，MySQL，默认情况下它们的端口是一致的，而且混在一起不好管理，所以推荐大家在安装之前先卸载以前安装的版本。至此所有准备工作就做完了，可以开始正式的安装过程了的。

1.安装libxml2库文件
```
./configure --prefix=/usr/local/libxml2
make
make install
```
2.安装libmcrypt库文件
```
./configure --prefix=/usr/local/libmcrypt
make
make install
```
3.安装zlib库文件
```
./configure --prefix=/usr/local/zlib
make
make install
```
4.安装libpng库文件
```
./configure --prefix=/usr/local/libpng
make
make install
```
5.安装jpeg6库文件，这个安装起来相对较麻烦，我当时主要是参考lampbrother论坛
```
mkdir /usr/local/jpeg6 //建立jpeg6软件安装目录
mkdir /usr/local/jpeg6/bin //建立存放命令的目录
mkdir /usr/local/jpeg6/lib //创建jpeg6库文件所在目录
mkdir /usr/local/jpeg6/include //建立存放头文件目录
mkdir -p /usr/local/jpeg6/man/man1 //建立存放手册的目录
./configure --prefix=/usr/local/jpeg6/ --enable-shared --enable-static
make && make install
```
6.安装freetype库文件
```
./configure --prefix=/usr/local/freetype
make
make install
```
7.安装autoconf库文件
```
./configure
make
make install
```
8.安装GD库文件
```
./configure \ //配置命令
> --prefix=/usr/local/gd2/ \ //指定软件安装的位置
> --with-zlib=/usr/local/zlib/ \ //指定到哪去找zlib库文件的位置
> --with-jpeg=/usr/local/jpeg6/ \ //指定到哪去找jpeg库文件的位置
> --with-png=/usr/local/libpng/ \ //指定到哪去找png库文件的位置
> --with-freetype=/usr/local/freetype/ //指定到哪去找freetype 2.x字体库的位置
make && make install
```
9.安装Apache服务器
```
./configure \ //配置命令
> --prefix=/usr/local/apache2 \ //指定Apache软件安装的位置
> --sysconfdir=/etc/httpd \ //指定Apache服务器的配置文件存放位置
> --with-z=/usr/local/zlib/ \ //指定zlib库文件的位置
> --with-included-apr \ //使用捆绑APR/APR-Util的副本
> --enable-so \ //以动态共享对象(DSO)编译
> --enable-deflate=shared \ //缩小传输编码的支持
> --enable-expires=shared \ //期满头控制
> --enable-rewrite=shared \ //基于规则的URL操控
> --enable-static-support //建立一个静态链接版本的支持
make && make install
```
测试Apache服务器     
检查安装目录，配置文件目录;启动Apache `/usr/local/apache2/bin/apachectl start`;停止Apche `/usr/local/apache2/bin/apachectl stop`; 还可以使用 `netstat -tnl|grep 80` 去查看80端口是否开启;通过`http://localhost/`去访问Apache服务器，出现`“It works!”`字样表示你安装成功了的。还可以使用`echo "/usr/local/apache2/bin/apachectl start" >> /etc/rc.d/rc.local` 添加到自动启动项里。

10.安装MySQL数据库管理系统
```
groupadd mysql //添加一个mysql标准组
useradd -g mysql mysql //添加mysql用户并加到mysql组中
./configure --prefix=/usr/local/mysql --with-extra-charsets=all
make && make install
```
配置MySQL数据库
```
# cp support-files/my-medium.cnf /etc/my.cnf //创建MySQL数据库服务器的配置文
bin/mysql_install_db --user=mysql //创建授权表
# chown -R root //将文件的所有属性改为root用户
# chown -R mysql var //将数据目录的所有属性改为mysql用户
# chgrp -R mysql //将组属性改为mysql组
# /usr/local/mysql/bin/mysqld_safe --user=mysql & 启动数据库
# netstat -tnl|grep 3306 //查看3306端口是否开启
# bin/mysqladmin version //简单的测试
# bin/mysqladmin variables //查看所有mysql参数
# bin/mysql -u root //没有密码可以直接登录本机服务器
mysql> DELETE FROM mysql.user WHERE Host='localhost' AND User='';
mysql> FLUSH PRIVILEGES;
mysql> SET PASSWORD FOR 'root'@'localhost' = PASSWORD('password');
# bin/mysql -u root -h localhost –p //回车进入MySQL客户端
# bin/mysqladmin -u root –p shutdown //关闭MySQL数据库
```
稍微提醒一最好下使用`bin/mysql -u root -h localhost –p`回车之后输入密码进入MySQL客户端，不要直接`bin/mysql -u root -h localhost –ppassword`的方式，这样别人移动一下方向键就会看到你的密码了哟。

11.安装PHP
```
./configure \ //执行当前目录下软件自代的配置命令
> --prefix=/usr/local/php \ //设置PHP5 的安装路径
> --with-config-file-path=/usr/local/php/etc \ //指定PHP5配置文件存入的路径
> --with-apxs2=/usr/local/apache2/bin/apxs \ //告诉PHP查找Apache 2的地方
> --with-mysql=/usr/local/mysql/ \ //指定MySQL的安装目录
> --with-libxml-dir=/usr/local/libxml2/ \ //指定PHP放置libxml2库的地方
> --with-png-dir=/usr/local/libpng/ \ //指定PHP放置libpng库的地方
> --with-jpeg-dir=/usr/local/jpeg6/ \ //指定PHP放置jpeg库的地方
> --with-freetype-dir=/usr/local/freetype/ \ //指定PHP放置freetype库的地方
> --with-gd=/usr/local/gd2/ \ //指定PHP放置gd库的地方
> --with-zlib-dir=/usr/local/zlib/ \ //指定PHP放置zlib库的地方
> --with-mcrypt=/usr/local/libmcrypt/ \ //指定PHP放置libmcrypt库的地方
> --with-mysqli=/usr/local/mysql/bin/mysql_config \ //变量激活新增加的MySQLi功能
> --enable-soap \ //变量激活SOAP和Web services支持
> --enable-mbstring=all \ //使多字节字符串支持
> --enable-sockets //变量激活socket通讯特性
make && make install
```
12.LAMP环境整合
```
cp php.ini-dist /usr/local/php/etc/php.ini //创建配置文件
```
在Apache的配置文件 `/etc/httpd/httpd.conf`中添加如下代码
```
Addtype application/x-httpd-php .php .phtml
```
运行 `cd /usr/local/apache2/htdocs` ,在该目录下新建一个`test.php`的文件
```
#emacs test.php //编辑test.php文件
<?php
phpinfo();
?>
```
通过浏览器访问 `http://localhost/test.php` 就可以得到`PHP Version`的网页。说明你的LAMP环境差不多已经搭建好了。

13.安装Zend加速器,据说可以提高访问网页30%～100%的速度
```
./install.sh //执行安装
```
就只剩最后一个`phpMyAdmin`了，安装方式和其他的差不多，在这就略写了.反正装不装这个影响不大的。

至于在windows下如何构建PHP开发环境和集成式的PHP学习环境，可以到google或者lamp论坛上去找了的。如果您在看此文时遇到什么问题可以找benbenbear(QQ:516967436)交流哈。     
Good Luck!!!!
