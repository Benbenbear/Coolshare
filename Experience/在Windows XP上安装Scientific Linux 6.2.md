以前用linux系统都是装在VMware中的，感觉不太真实，一直想在真机上尝试一下，最近在网上看了一些资料，终于在真机上尝试了一下，感觉蛮好的。其实开始是想用centos的，毕竟我接触的时间稍微多一些，还有看网上ubuntu的资源也很多，在虚拟机上试试了一下，还是redhat系列的用着习惯一点，后来师兄>推荐用这个，反正也是redhat系列吧，差别不是很大，如果遇到什么困难还可以找他帮忙的。好吧，说正题了的。 

1. 首先从网上download Scientific linux 6.2的镜像文件（SL-62-i386-2012-02-06-Install-DVD.iso）和 [grub4dos](http://www.linuxidc.com/Linux/2009-01/18027.htm)。解压grub4dos后把其中的grldr，grub.exe,menu.lst，grldr四个文件放到C盘根目录下。      

2. 把SL-62-i386-2012-02-06-Install-DVD.iso放在一个格式为FAT32的盘里（据说是U盘或者移动硬盘也可以），然后提取出里面的isolinux文件夹拷贝到C盘根目录，再提取出里面的images文件夹放在该盘的根目录下。       
 
3. 把windows下隐藏文件全部显示出来，就可以在C盘根目录下看到boot.ini,先解除其只读属性，在cmd下输入 `attrib -s -r -h c:\boot.ini`。用记事本>打开该文件，在最后面添加一行`c:\grldr=“Scientific linux” `，编辑完成后再恢复boot.ini的只读属性，即在cmd下输入`attrib +s +r +h c:\boot.ini`>即可。    

4. 打开打开C:\menu.lst文件添加以下内容(注意kernel和initrd后面有空格)：    
      ```title Scientific Linux //指定在grldr中显示的标题    
      kernel (hd0,0)/isolinux/vmlinuz //指定内核文件在哪个磁盘的哪个分区的哪个目录中    
      initrd (hd0,0)/isolinux/initrd.img //指定initrd.img文件路径，用于在内核启动之后加载硬件驱动```    

5. 现在重启就可以进行安装了，安装过程中注意磁盘分区选择手动分区（安装Scientific Linux的分区是可以先在windows下格式化之后预留好，也可以临格式化处理），根据自己的实际需要进行分区，要不然有可能整个硬盘的数据被干掉。时间设置时不要勾选UTC时钟，要不然有可能装完后系统时间会过快或过慢。

6. 安装完成后进入Scientific linux 6.2系统后：`vim /boot/grub/grub.conf`， 把hiddenmenu 注释掉：这样就会显示出启动菜单。 把title Other 改r 直观的名称：如title windows xp （你随便改都可以，你可以改成别人看到你电脑不知道是什么系统都可以，哈哈。。。。）。

7. 最后进入xp清除安装时的解压出的文件以及boot.ini中的语句。我是按照上述步骤实现了的，如果有问题可以和我联系哟！欢迎批评指正！

最后感谢Nicol一直对我的帮助和鼓励！！哈哈。。。。。。。
