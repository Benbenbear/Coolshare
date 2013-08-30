**1. IFS**  
IFS（Internal Field Separator，内部字段分隔符）是脚本中一个非常重要的概念，它是存储定界符的环境变量，默认值是空白符（换行符、制表符和空格）。看下面实例：  
``` shell 
#!/bin/bash

person="name,age,sex,location"

oldIFS=$IFS
IFS=,
for i in $person;
do
  echo Iterm: $i
done

IFS=$oldIFS
for i in $person;
do
  echo Iterm: $i
done
```
运行结果如下：
``` shell
[benbenbear@benbenbear shell]$ sh IFS.sh 
Iterm: name
Iterm: age
Iterm: sex
Iterm: location
Iterm: name,age,sex,location
```
**2. 循环**  
`for循环`
``` shell
for var in list;
do
commands;
done
```
``` shell
for i in {a..z}; do actions; done;        #注意括号中间是两个点
for i in {3..13}; do actions; done;
```
``` shell
[benbenbear@benbenbear shell]$ for i in {1..5}; do echo $i; done;  
1
2
3
4
5
```
也可以像C语言一样的for循环：
``` shell
for((i=0;i<5;i++))          #注意要两个括号
{
  echo $i;
}
```
`while循环`
``` shell
while condition
do
  commands;
done
```
如果condition为true就会变成无限循环。  
`until循环`
``` shell
#!/bin/bash
x=0;
until [ $x -eq 9 ];
do let x++; echo $x;
done
```
until它会一直执行循环直到给定的条件为真。上面这个示例会输出1到9。

_ _ _
OK, Good Luck!
