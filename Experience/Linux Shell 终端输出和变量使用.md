* shell脚本通常是一个以`#!`开始的文本文件，如：`#!/bin/bash`。通常有两种方式运行脚本，一是`sh script.sh`，这种将脚本作为sh的参数来运行，那么脚本中开头的shebang行也就没有用了；二是赋予脚本可执行权限，通过`./script.sh`运行，这种方式shell程序就会先去读取脚本的shebang行，识别到`#!/bin/bash`，然后在内部以`/bin/bash script.sh`执行脚本。
* echo  
echo在每次调用之后会增加一个换行符。当在echo中使用带双引号的文本时，需要在之前加上`set +H`,才能正常显示“！”。
<pre><code>[benbenbear@benbenbear shell]$ echo Welcome to shell !
Welcome to shell !
[benbenbear@benbenbear shell]$ echo 'Welcome to shell !'
Welcome to shell !
[benbenbear@benbenbear shell]$ echo "Welcome to shell !"
-bash: !": event not found
[benbenbear@benbenbear shell]$ set +H
[benbenbear@benbenbear shell]$ echo "Welcome to shell !"
Welcome to shell !
</code></pre>
当然使用不带引号的echo时，没法在所要显示的文本中显示分号；使用单引号时，不会对引号中的变量（$var）求值。   
echo可以使用-n来忽略结尾的换行符，也可以使用-e来接受包含转义字符的字符串。如：`echo -e "1\t2\t3\t"`。  
终端中产生彩色输出很好玩了，常用的颜色码：重置=0，黑色=30，红色=31，绿色=32，黄色=33，蓝色=34，洋红=35，青色=36，白色=37。要设置彩色背景，经常使用的颜色码是：重置=0，黑色=40，红色=41，绿色=42，黄色=43，蓝色=44，洋红=45，青色=46，白色=47。示例如下：
![colorful terminal.jpg](https://s3.amazonaws.com/logdown-production/user/3286/blog/3333/post/87506/lYskRMNSVK3M1YMWaHBB_colorful%20terminal.jpg)
* printf    
printf和C语言中的printf函数类似，它不像echo一样会自动添加换行符。示例如下：
<pre><code>[benbenbear@benbenbear shell]$ cat printf.sh 
#!/bin/bash
printf "%-5s %-10s %-4s\n" No Name Score
printf "%-5s %-10s %-4.2s\n" 01 James 87.3
printf "%-5s %-10s %-4.2s\n" 02 Grace 98.32
printf "%-5s %-10s %-4.2s\n" 03 Paul 56
</code></pre>
输出结果：
<code><pre>[benbenbear@benbenbear shell]$ sh printf.sh 
No    Name       Score
01    James      87  
02    Grace      98  
03    Paul       56
</code></pre>

* 变量与环境变量  
每个进程在运行时都可以通过`cat /proc/$PID/environ`来获取与该进程相关的环境变量，但是彼此之间是由null字符分隔，可以把`\0`换成`\n`，格式更好看一些：`cat /proc/$PID/environ | tr '\0' '\n'`，里面竟然还可以看到SSH_CONNECTION，里面有显示你ssh上来的ip，有点意思。。。。  
一个变量可以通过`var=value`进行赋值，千万要注意在shell中`var = value`是相等操作，而不是赋值操作，这和其他很多语言是不一样的。可以通过`echo $var`或者`echo ${var}`输出变量的内容。  
export命令可以用来设置环境变量，之后从当前shell脚本执行的任何程序都会继承这个变量。如：
<pre><code>PATH="$PATH:/home/user/bin”
export PATH
</code></pre>
这样我们就把`/home/user/bin`添加到了PATH中了。  
* 变量与环境变量技巧  
    * 获得字符串长度 
<pre><code>[benbenbear@benbenbear shell]$ var="welcome to shell !"
[benbenbear@benbenbear shell]$ echo ${#var}
18
</code></pre>
    * 识别当前的shell版本：$0 或者 $SHELL
<pre><code>[benbenbear@benbenbear shell]$ echo $0
-bash
[benbenbear@benbenbear shell]$ echo $SHELL
/bin/bash
</code></pre>
    * 通过$UID判断是否为超级用户， root用户的UID是0。
    * 修改Bash提示字符串，通常默认可以通过`cat ~/.bashrc | grep PS1`，`cat /etc/bashrc | grep PS1`或者`cat /etc/bash.bashrc | grep PS1`找到配置文件，然后根据我们的意愿进行修改。例如：\u可以扩展为用户名，\h可以扩展为主机名，\w可以扩展为当前工作目录。

_ _ _
OK, Good Luck! 
