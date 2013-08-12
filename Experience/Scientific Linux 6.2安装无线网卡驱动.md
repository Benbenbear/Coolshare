我的`Scientific Linux 6.2`装完之后，发现不可以无线上网，我的无线网卡是`Broadcom BCM4311`的，网上查阅了很多资料，都说是没有无线网卡驱动，我>网上找了很多资料，都没有搞成功。大家可以参考以下的方法：

[方法1](http://www.xnlinux.cn/thread-1503-1-1.html)
[方法2](http://wiki.centos.org/zh/HowTos/Laptops/Wireless/Broadcom#head-3f2ee861edb7870fe117952cd96b78da22088d25)
[方法3](http://www.broadcom.com/docs/linux_sta/README.txt)

貌似是可以成功的，也许是我电脑的问题，我的参照上述方法没有成功。我
最后是参考了_Sudhaker's Blog_中的方法，成功了的，具体如下：
```
$ /sbin/lspci -vnn | grep 14e4
04:00.0 Network controller [0280]: Broadcom Corporation BCM4311 802.11a/b/g [14e4:4312] (rev 02)
```
```
yum install b43-fwcutter b43-openfwwf
mkdir ~/b43-driver; cd ~/b43-driver
wget http://downloads.openwrt.org/sources/broadcom-wl-4.150.10.5.tar.bz2
tar jxf broadcom-wl-4.150.10.5.tar.bz2
cd broadcom-wl-4.150.10.5/driver
b43-fwcutter -w /lib/firmware/ wl_apsta_mimo.o
```
然后重启，这样就可以无线上网了的。希望遇到类似问题的同学，可以有帮助！

Good Luck!!!
