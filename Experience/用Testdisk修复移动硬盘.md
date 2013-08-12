前几天遇到一个问题，同学的500G的移动硬盘无论插到哪台电脑上都识别不出来，里面又有很多数据不知道要怎么办，而我刚好前几天逛论坛在`Geekfan`上看到一些数据恢复的工具，于是就想尝试一下。   
首先尝试了`safecopy`，它可以从发生故障的存储设备中把数据拷贝出来，很不幸的是由于同学的硬盘mount不了，所以没有成功，使用命令方法和copy很类似。   
接下来就是立功的Testdisk了，它可以解决一些由于分区原因而导致硬盘无法访问的问题，可以帮助你恢复丢失的分区，恢复主引导记录，以及文件系统表，还可以从文件系统中恢复被删除的文件，总之功能很强大了的，所以最好在使用前看看它的官方手册和文档了的。   
在终端直接输入`sudo testdisk`即可使用，会看到下面的画面。  
![Testdisk.jpg](https://s3.amazonaws.com/logdown-production/user/3286/blog/3333/post/84325/Isy2eoFLTgS42lrxZXbS_Testdisk.jpg)      
回车之后找到我们需要修复的盘，我为了保险起见，我先是使用了Advanced选项里的List，把重要文件先拷贝出来，然后才进行Analyse修复。
![testdisk2.jpg](https://s3.amazonaws.com/logdown-production/user/3286/blog/3333/post/84325/YnQKHFI5SyiSYLeZclg8_testdisk2.jpg)  
最后使用Gparted把全盘格式化后重新新建了分区，算是完工。
![Gparted.jpg](https://s3.amazonaws.com/logdown-production/user/3286/blog/3333/post/84325/TlGhBaBrRlSp3PRNzMIR_Gparted.jpg)  
我只是简短记录一下大概过程，其实当时查资料远不止这么简单，也算为平时我使用linux争口气;同时呢也建议大家500G这么大的硬盘还是应该分一下区，那样的话一个分区坏了其他的分区还可以用，当然还有就是不要强制拔掉，以免造成不必要的麻烦!   
OK! Have a good day!
