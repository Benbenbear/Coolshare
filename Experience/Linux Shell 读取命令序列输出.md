Linux通常有两种方式来读取命令序列的输出。

1. 子shell（subshell）
```
$ cmd_output=$(ls | cut -n)
$ echo $cmd_out
```

2. 反引用（back-quote）
```
$ cmd_output=`ls | cut -n` #反引号是位于键盘的”~“上，可不是单引号哟
$ echo $cmd_out
```
利用子shell生成一个独立的进程：可以使用”（）“来定义一个子shell。
```
pwd;
(cd /etc; ls);
pwd;
```

当命令在子shell中执行时，不会对当前shell有任何影响，所有的改变仅限于子shell内。
假设我们使用subshell和back-quote的方式将命令的输出读入一个变量中，可以将它放入双引号中，以保留空格和换行符。
``` shell
[benbenbear@benbenbear shell]$ cat test.txt 
how
are
you
[benbenbear@benbenbear shell]$ echo $(cat test.txt)
how are you
[benbenbear@benbenbear shell]$ echo "$(cat test.txt)"
how
are
you
```
read是一个重要的Bash命令，下面介绍一些read的重要选项。
``` shell
read -n number_of_chars var #从输入中读取n个字符存入变量var中 ie. $ read -n 2 var
read -s var  #以不回显的方式读取密码                          ie. $ read -s var
read -p "Enter input: " var #显示提示信息                    ie. $ read -p "Enter input: " var
read -t timeout var #在特定时间内读取输入                     ie. $ read -t 2 var
read -d dellim_char var #用定界符结束输入行                   ie. $ read -d ":" var
```

_ _ _ 
OK, Good Luck!
