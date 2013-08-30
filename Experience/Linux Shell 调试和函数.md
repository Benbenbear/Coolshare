**1. 脚本调试**  
在Bash脚本中，可以使用`bash -x script.sh`或者`sh -x script.sh`来启动跟踪调试功能。其实也可以在脚本中使用set built-in来启动或禁止调试打印。
* set -x: 在执行时显示参数和命令 
* set +x: 禁止调试
* set -v：当命令进行读取时显示输入
* set +v: 禁止打印输入

其实我们巧妙利用shebang把`#!/bin/bash`改成`#!/bin/bash -xv`,这样一来不用任何其他选项就可以启动调试功能了。

**2. 函数**  
定义函数：
``` shell
function fname() #function可以省略不写
{
statements;
}
```
只需要使用函数名就可以调用，也可以传递参数给函数进行访问。
一些常用的参数如下：
* $0: 脚本名称
* $1: 第一个参数
* $2: 第二个参数
* $n: 第n个参数
* "$@"：被扩展成”$1“ ”$2“ ”$3“等，这个用多一些。
* "$*“：被扩展成”$1c$2c$3“,其中c是IFS（Internal Field Separator）的第一个字符,默认是空白键。
* $#: 传递给脚本的参数个数
* $?: 最后运行的命令的返回值（通常返回0表示成功）
* $$：Shell本身的PID
* $!：Shell最后运行的后台processer的PID
* $-: 使用set命令设定的Flag一览

_ _ _
OK! Good Luck!
