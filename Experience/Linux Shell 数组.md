Bash从4.0版本之后开始支持关联数组，普通数组只能使用整数作为数组索引，而关联数组可以使用字符串作为索引。具体查看bash version可以通过`echo $BASH_VERSION`或者`bash --version`来获得。
定义数组可以在单行中通过一列值来定义，也可以将数组定义成索引-值。
``` shell
[benbenbear@benbenbear shell]$ array_value=(1 2 3 4 5 6)

[benbenbear@benbenbear shell]$ array[0]="test1"
[benbenbear@benbenbear shell]$ array[1]="test2"
[benbenbear@benbenbear shell]$ array[2]="test3"
# 打印出特定索引的数组元素内容
[benbenbear@benbenbear shell]$ echo ${array[0]}
test1
[benbenbear@benbenbear shell]$ index=2
[benbenbear@benbenbear shell]$ echo ${array[$index]}
test3
# 打印出数组中的所有值
[benbenbear@benbenbear shell]$ echo ${array_value[*]}
1 2 3 4 5 6
[benbenbear@benbenbear shell]$ echo ${array_value[@]}
1 2 3 4 5 6
# 列出数组索引
[benbenbear@benbenbear shell]$ echo ${!array_value[@]}
0 1 2 3 4 5
[benbenbear@benbenbear shell]$ echo ${!array_value[*]}
0 1 2 3 4 5
# 打印数组长度
[benbenbear@benbenbear shell]$ echo ${#array_value[@]}
6
[benbenbear@benbenbear shell]$ echo ${#array_value[*]}
6
```
定义关联数组需要使用单独的声明语句将一个变量名声明为关联数组。
```
[benbenbear@benbenbear shell]$ declare -A array_ass                         #声明语句
[benbenbear@benbenbear shell]$ array_ass=([apple]='5.0' [orange]='8.0')     #内嵌索引-值列表法
[benbenbear@benbenbear shell]$ array_ass[banana]='4.0'                      #利用独立的索引-值进行赋值
[benbenbear@benbenbear shell]$ array_ass[pear]='6.0'
[benbenbear@benbenbear shell]$ echo "Apple costs ${array_ass[apple]} yuan." #输出关联数组内容
Apple costs 5.0 yuan.
[benbenbear@benbenbear shell]$ echo ${!array_ass[*]}                        #列出数组索引
orange apple pear banana
[benbenbear@benbenbear shell]$ echo ${!array_ass[@]}
orange apple pear banana
[benbenbear@benbenbear shell]$ echo ${#array_ass[@]}                        #列出数组中元素的个数
4
[benbenbear@benbenbear shell]$ echo ${#array_ass[*]}
4
``` 

_ _ _
OK, Good Luck!

