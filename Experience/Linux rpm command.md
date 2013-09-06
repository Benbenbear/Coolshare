RPM 是 Red Hat Package Manager 的缩写，是Redhat系列（RHEL，CentOS，Fedora）的常用包管理工具。通过root的权限，可以对rpm软件包进行恰当的管理， rpm 命令通常有五种基本的模式：
> Install:      安装
> Remove/Erase: 卸载
> Upgrade：     升级
> Query：       查询
> Verify：      验证

下面是一些常用的实例：

1. 安装一个rpm包 `rpm -ivh rpm-file`
```
[root@benbenbear]/home/benbenbear/Downloads# rpm -ivh synergy-1.4.12-Linux-i686.rpm  
[root@benbenbear]/home/benbenbear/Downloads# rpm -ivh --test synergy-1.4.12-Linux-i686.rpm 
```
其中： 
  * -i: install a package
  * -v: verbose
  * -h: print hash marks as the package archive is unpacked.

2. 升级一个rpm包 `rpm -Uvh rpm-file`
```
[root@benbenbear]/home/benbenbear/Downloads# rpm -Uvh synergy-1.4.12-Linux-i686.rpm
[root@benbenbear]/home/benbenbear/Downloads# rpm -Uvh --test synergy-1.4.12-Linux-i686.rpm
```

3. 移除一个已经安装的rpm包 `rpm -ev package`，`rpm -ev -nodeps package`
```
[root@benbenbear]/home/benbenbear/Downloads# rpm -ev synergy 
[root@benbenbear]/home/benbenbear/Downloads# rpm -ev --nodeps synergy #在移除时不检测依赖关系
```

4. 列出安装的所有rpm包 `rpm -qa`
```
[root@benbenbear]/home/benbenbear/Downloads# rpm -qa
[root@benbenbear]/home/benbenbear/Downloads# rpm -qa | less
[root@benbenbear]/home/benbenbear/Downloads# rpm -qa --last  #列出最近安装的包
[root@benbenbear]/home/benbenbear/Downloads# rpm -qa --last | less
[root@benbenbear]/home/benbenbear/Downloads# rpm -qa | grep 'MySQL' #检查MySQL这个包是否安装
```
补充：
```
[root@benbenbear lib]# rpm -q synergy #查询一个特定的rpm包是否安装，注意package name一定要准确
synergy-1.4.12-1.i386
[root@benbenbear lib]# rpm -ql synergy #列出安装的rpm包的所有文件
/usr/bin/synergy
/usr/bin/synergyc
/usr/bin/synergyd
/usr/bin/synergys
/usr/share/applications/synergy.desktop
/usr/share/icons/synergy.ico
```

5. 查询已经安装的包的信息（版本和短暂描述） `rpm -qi package`
```
[root@benbenbear]/home/benbenbear/Downloads# rpm -qi synergy
Name        : synergy                      Relocations: (not relocatable)
Version     : 1.4.12                            Vendor: The Synergy Project
Release     : 1                             Build Date: Fri 03 May 2013 01:17:43 PM CST
Install Date: Fri 06 Sep 2013 12:28:44 PM CST      Build Host: sci2
Group       : unknown                       Source RPM: synergy-1.4.12-1.src.rpm
Size        : 19154816                         License: unknown
Signature   : (none)
Summary     : Synergy server and client
...
```

6. 查找文件是属于哪个包 `rpm -qf /path/to/file`
```
[root@benbenbear]/home/benbenbear/Downloads# rpm -qf /bin/bash
bash-4.1.2-14.el6.i686
```

7. 查看一个包的配置文件信息 `rpm -qc package-name`
```
[root@benbenbear]/home/benbenbear/Downloads# rpm -qc bash 
/etc/skel/.bash_logout
/etc/skel/.bash_profile
/etc/skel/.bashrc
```

8. 列出一个命令的配置信息 `rpm -qcf /path/to/file`
```
[root@benbenbear]/home/benbenbear/Downloads# rpm -qcf /usr/bin/yum   
/etc/logrotate.d/yum
/etc/yum.conf
/etc/yum/version-groups.conf
```

9. 找出rpm包的依赖关系 `rpm -qpR rpm-file`, `rpm -qR package`
```
[root@benbenbear]/home/benbenbear/Downloads# rpm -qpR synergy-1.4.12-Linux-i686.rpm 
[root@benbenbear]/home/benbenbear/Downloads# rpm -qR synergy
```

10. 验证一个指定的rpm包 `rpm -Vp rpm-file`
```
[root@benbenbear]/home/benbenbear/Downloads# rpm -Vp synergy-1.4.12-Linux-i686.rpm
[root@benbenbear]/home/benbenbear/Downloads# rpm -Va #验证所有的安装的包
```

11. 导入RPM GPG key
```
[root@benbenbear Downloads]# rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-sl6 #导入GPG key
[root@benbenbear Downloads]# rpm -qa gpg-pubkey* #列出已经导入的GPG key
gpg-pubkey-9b1fd350-4a576be4
gpg-pubkey-7fac5991-4615767f
gpg-pubkey-1d1e034b-42bfd0c5
gpg-pubkey-192a7d7d-4a5769d0
```

_ _ _ 
OK! Good Luck!
