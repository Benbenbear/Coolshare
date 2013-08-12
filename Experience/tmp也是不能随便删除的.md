今天在做文件练习的时候，看到`/tmp`里文件太多，就把`/tmp`给干掉了，结果用着感觉就不正常了的，然后重启就进入不了系统了的，提示 `/usr/libexec/gconf-sanity-check-2` 退出状态`256`，`X-window`也不可以进去，屏幕黑漆漆的。一开始还想用安装镜像重新安装升级一下，结果没用。后来上网找了一，就是因为把`/tmp`目录干掉了的，具体修复如下：
重启时在读秒时按下`e`进入`grub`编辑模式，大概是这样：
```
root(xxx,x)

kernel /vmlinuz-2.6 xxxxxxxxx

initrd /initrdxxxxxx
```
把光标移动到`kernel`那一行，按下`e`进入编辑模式，在最后加上`single`，再按`b`就可以进入单用户模式了，把`/tmp`的权限修改为`777`即可。准确说该是`drwxrwxrwt`,所以最好 `chmod 1777 /tmp` 或者`chmod o+t /tmp`.（因为`SBIT`可以防止在公共目录`/tmp`创建的目录被别人随意删除，只有`owner`和`root`可以删除！）
哎！！！`/tmp`也不是可以随便删除的哈！！！

另外，今天发现个`ntfs-3g`的东东，安装之后就可以看`NTFS`的文件系统了的，因为偶的是双系统，以前`windows`下的是`NTFS`的，这样我就不用重启电脑>来查看原来的东西了的，还是很方便的。安装也很简单：

```
yum -y install ntfs-3g
```
或者到 [这个网站](http://www.tuxera.com/community/ntfs-3g-download)下载，然后解压之后在本目录下运行`./configure && make && make install`就可以搞定了的。
