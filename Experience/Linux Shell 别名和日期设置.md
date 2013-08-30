**1. 别名 alias**
别名其实就是按照User自己的习惯定制的一种便捷方式。可以通过`$ alias new_command='command sequence'`来设定，但是这样设置的话如果当前终端关闭的话所设置过的别名也就无效了，所以更常用的做法是把它加入到`~/.bashrc`中。下面是我常用的一些别名：
```
[benbenbear@benbenbear Work]$ cat ~/.bashrc | grep alias
# User specific aliases and functions
alias vi='vim'
alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'
# alias grep='grep -inr --color=auto'
alias 99="seq 9 | sed 'H;g' | awk -v RS='' '{for(i=1;i<=NF;i++)printf(\"%dx%d=%d%s\",i,NR,i*NR,i==NR?\"\n\":\"\t\")}'"
```
如果我们创建别名的时候，已经有同名的别名存在，那么原有的设置会被当前的设置所取代。如果要删除别名，只需要将对应语句从`~/.bashrc`中移除或者使用unalias。
补充一点，通常在不信任的环境中执行重要命令可以在前面加上“\”,`$ \command`,这样我们就可以执行原始的命令从而防止有人利用别名做的手脚。
**2. 日期设置**
在类UNIX系统中，日期被存储为一个整数，其大小为时间标准时间（UTC）1970年1月1日0时0分0秒起所流逝的秒数（不包括闰秒）。
下面是常用的一些日期格式字符串列表：

| 日期内容        | 格式                | 
| -------------  |:------------------: | 
| 星期            | %a（例如：Sat）；%A（例如：Saturday）|
| 月              | %b（例如：Nov）；%B（例如：November）|  
| 日              | %d（例如：31）         |   
| 固定格式日期(mm/dd/yy)| %D（例如：10/18/13）            
| 年              | %y（例如：13）；%Y（例如：2013）            
| 小时            | %I或%H（例如：07）           
| 分钟            | %M（例如：31）            
| 秒              | %S（例如：31）            
| 纳秒            | %N（例如：695209412）            
| UNIX纪元时      | %s（例如：1290098654）            

用格式串结合+作为date命令的参数，可以按照你的选择打印出对应格式的日期。`# date -s "格式化的日期字符串"`可以设置日期和时间。
```
[benbenbear@benbenbear shell]$ date "+%d %B %Y"
18 August 2013
[benbenbear@benbenbear shell]$ date --date "Aug 18 2013" +%A #判断给定的日期是星期几
Sunday
[benbenbear@benbenbear shell]$ date --date "Sun Aug 18 14:50:56 CST 2013" +%s #转换为纪元时
1376808656
[benbenbear@benbenbear shell]$ sudo date -s "18 Aug 2013 15:16:03"
Sun Aug 18 15:16:03 CST 2013
```
其实现实中，有时我们需要检查一组命令所花费的时间也可以在命令前后分别插入date，最后两者的差值就是改组命令所花费的时间了的。

_ _ _
OK! Good Luck!

