前几天有位同学电脑出故障了，由于需要，他想要装`win7`和`linux`的双系统。`win7`的安装就不多说了的，稍微说一下就是他的电脑是三星R467的，装完`win7`之后不能激活（大家都懂的。。。。），后来网上找了一下，三星有的机子貌似用`win7 action`这个东东不管用的，有的貌似还说要修改`BIOS`之类的能激活，听着有点虚，后来仔细看了下，找到一款`sxwinjih.zip`的软件 ，就激活成功了的。

接下来就是安装`linux`了的，把`SL-62-i386-2012-02-06-Install-DVD.iso`放在一个格式为`FAT32`的盘里（据说是U盘或者移动硬盘也可以），然后提取出>里面的`isolinux`文件夹和`images`文件夹放在该盘的根目录下（假设F盘）。`win7`和`XP`是不一样的，`win7`下可以用`EasyBCD`这款软件来设置引导，安>装并打开软件，选择左侧的`Add New Entry`，然后选择`NeoGrub`，再选择`Install`，再选择`Configure`,会弹出一个记事本一样的`menu.lst`,在文件后面>补充
```
title Scientific Linux
kernel (hd0,6)/isolinux/vmlinuz//指定内核文件在哪个磁盘的哪个分区的哪个目录中
initrd (hd0,6)/isolinux/initrd.img//指定initrd.img文件路径，用于在内核启动之后加载硬件驱动
```
现在重启就可以进行安装了，安装过程中注意磁盘分区选择手动分区（安装`Scientific Linux`的分区是可以先在`windows`下格式化之后预留好，也可以临格式化处理），根据自己的实际需要进行分区，要不然有可能整个硬盘的数据被干掉。时间设置时不要勾选`UTC`时钟，要不然有可能装完后系统时间会过快者过慢。

安装完成后进入`Scientific linux 6.2`系统后：`vim /boot/grub/grub.conf`， 把`hiddenmenu `注释掉：这样就会显示出启动菜单。 把`title Other `成直观的名称：如`title win7` （你随便改都可以，你可以改成别人看到你电脑不知道是什么系统都可以，哈哈。。。。）

最后进入`win7`通过`EasyBCD`在刚才点击`configure`的页面`remove`掉刚才的`Neogrub`，再卸载该软件即可，清除`F`盘提取出来的两个文件夹。
It`s over! Enjoy your win7 and Linux！！！！
