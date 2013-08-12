Linux用户标识符（User identifier）,简称UID，在类Unix系统中是内核用来辨识用户的一个无符号整型数值，也是文件系统与进程的必要组成部分之一。  
前几天刚好有个customer遇到了一些用户管理的场景，总结一下：  
1. 如果一个用户属于多个群组，在作业的时候到底是以哪个群组为准呢？这里就涉及到有效群组的问题：  
```
[root@benbenbear Downloads]# usermod -G test benbenbear  --->给用户benbenbear添加到次要群组test
[root@benbenbear Downloads]# grep benbenbear /etc/passwd /etc/group /etc/gshadow
/etc/passwd:benbenbear:x:500:500:benbenbear:/home/benbenbear:/bin/bash
/etc/group:benbenbear:x:500:   --->benbenbear是初始群组，所以/etc/group的第四字段不需要填入
/etc/group:test:x:501:benbenbear   --->test是次要群组，所以要在/etc/group的第四字段填入
/etc/gshadow:benbenbear:!!::
/etc/gshadow:test:!::benbenbear   --->test是次要群组
```
我们可以通过`groups`来查看有效群组，第一个输出的群组即为有效群组。  
```
[benbenbear@benbenbear Work]$ groups     
benbenbear test  --->benbenbear即为有效群组
```
可以通过`newgrp`来切换有效群组，`exit`返回原来的状态。  
2. useradd
```
useradd -u 后面接uid
useradd -g 后面接initial group
useradd -G 后面接次要群组
useradd -M 强制不要添加用户家目录（系统账户默认设置）
useradd -m 强制创建用户家目录（普通账户默认配置）
useradd -d 指定某个目录为家目录，一定要使用绝对路径
useradd -s后面指定shell
useradd -c 后面接用户的comment，也就是/etc/passwd的第五个字段的内容
```
`usermod`也类似如此。  
可以通过`useradd -D`改变默认选项：
```
[root@benbenbear Work]# useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
CREATE_MAIL_SPOOL=yes
```  
PS:有时我们运行`useradd username`时会出现`useradd: cannot lock /etc/passwd , try it again later.`
我们可以这样解决：
```
[root@benbenbear Work]# cd /etc/
[root@benbenbear etc]# ls -l *.lock
[root@benbenbear etc]# rm –rf /etc/passwd.lock 
[root@benbenbear etc]# rm –rf /etc/shadow.lock
[root@benbenbear etc]# rm –rf /etc/group.lock
[root@benbenbear etc]# rm –rf /etc/gshadow.lock
```

OK，Good Luck!!!
