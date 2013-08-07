---
layout: post
title: "Linux下LNMP环境的简单搭建"
date: 2013-05-05 15:35
comments: true
categories: Linux Web 
---

前几天因为我师傅申请了个新的VPS，但是发现Apache很耗资源，想换成Nginx，他又没时间折腾，我就帮他折腾了一下。
趁周末把它记录一下，要不然过一段时间又忘记了的。关于Web服务器的搭建也可以参考[Linux下搭建LAMP环境](http://www.coolshare.pw/blog/2013/04/12/linuxxia-da-jian-lamphuan-jing/)，下面转入正题：     
我的系统是Scientific Linux。<pre><code>[benbenbear@benbenbear Work]$ lsb_release -a
LSB Version:    :base-4.0-ia32:base-4.0-noarch:core-4.0-ia32:core-4.0-noarch:graphics-4.0-ia32:graphics-4.0-noarch:printing-4.0-ia32:printing-4.0-noarch
Distributor ID:	Scientific
Description:	Scientific Linux release 6.4 (Carbon)
Release:	6.4
Codename:	Carbon</pre></code>
1. 安装nginx<pre><code>[benbenbear@benbenbear Work]$ sudo yum installnginx</pre></code>
2. 安装php<pre><code>[benbenbear@benbenbear Work]$ sudo yum installphp</pre></code>
3. 安装mysql-server<pre><code>[benbenbear@benbenbear Work]$ sudo yum installmysql-server</pre></code>
4. 安装php-mysql<pre><code>[benbenbear@benbenbear Work]$ sudo yum installphp-mysql</pre></code>
5. 安装php-fpm<pre><code>[benbenbear@benbenbear Work]$ sudo yum installphp-fpm</pre></code>
6. 安装php-mbstring<pre><code>[benbenbear@benbenbear Work]$ sudo yum installphp-mbstring</pre></code>
7. 安装php-gd<pre><code>[benbenbear@benbenbear Work]$ sudo yum installphp-mbstring</pre></code>
8. 安装php-pear<pre><code>[benbenbear@benbenbear Work]$  sudo yum installphp-pear</pre></code>
9. 安装php-mcrypt<pre><code>[benbenbear@benbenbear Work]$ sudo yum installphp-mcrypt</pre></code>
10. 安装php-eaccelerator<pre><code>[benbenbear@benbenbear Work]$ sudo  yum installphp-eaccelerator</pre></code>
11. 修改php-fpm的配置文件<pre><code>[benbenbear@benbenbear Work]$ sudo vi /etc/php-fpm.d/www.conf</pre></code>把第39行和41行修改为`user=nginx`和`group=nginx`。  
12. 设置mysql密码<pre><code>[benbenbear@benbenbear Work]$ service mysqld start
[benbenbear@benbenbear Work]$ mysqladmin -u root password 'xxxxxx'</pre></code>
13. 设置它们开机启动<pre><code>
[benbenbear@benbenbear Work]$ sudo chkconfig nginx on
[benbenbear@benbenbear Work]$ sudo chkconfig mysqld on
[benbenbear@benbenbear Work]$ sudo chkconfig php-fpm on</pre></code>
14. 修改nginx的配置文件<pre><code>[benbenbear@benbenbear Work]$ sudo vi /etc/nginx/conf.d/default.conf</pre></code>
<pre><code>
	 12     location / {
     13         root   /usr/share/nginx/html;
     14         index  index.php index.html index.htm;
     15     }

 	 37     location ~ \.php$ {
     38         fastcgi_pass   127.0.0.1:9000;
     39         fastcgi_index  index.php;
     40         fastcgi_param  SCRIPT_FILENAME  /usr/share/nginx/html$fastcgi_script_name;
     41         include        fastcgi_params;
     42     }
</pre></code>    
15. 开启80端口<pre><code>
[benbenbear@benbenbear Work]$ sudo /sbin/iptables -I INPUT -p tcp --dport 80 -j ACCEPT
[benbenbear@benbenbear Work]$ sudo /etc/rc.d/init.d/iptables save
[benbenbear@benbenbear Work]$ sudo /etc/rc.d/init.d/iptables restart</pre></code>
16. 启动nginx和php-fpm<pre><code>
[benbenbear@benbenbear Work]$ sudo /etc/init.d/nginx start
[benbenbear@benbenbear Work]$ sudo /etc/init.d/php-fpm start</pre></code>
17. 测试结果<pre><code>[benbenbear@benbenbear Work]$ cat /usr/share/nginx/html/index.php</pre></code>
``` php
<?php
phpinfo();
?>
```
在浏览器输入`http://localhost`，会出现下面的图片，说明已经可以解析PHP了。 
{% img /images/php-nginx.png %}     
Good Luck!



