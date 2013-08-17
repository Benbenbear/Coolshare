在Bash shell环境中，可以利用`let`,`(())`和`[]`执行基本的算术运算，而在进行高级操作时，`expr`和`bc`也会非常有用。
``` shell
#!/bin/bash

no1=4
no2=5
let sum=no1+no2    #9 使用let进行计算时，变量名前不需要再添加$.
let no1++          #5
let no2--          #4
let no1+=6         #11
let no2+=6         #10

result=$[ no1 + no2] #21 使用[]可以使用$前缀也可以不使用.
result=$[$no1 + 5]   #16

result=$(($no1 + 50)) #61 使用(())，必须使用$前缀.

result=`expr 3 + 4`   #7
result=$(expr $no1 + 10) #21
```
以上这些方法只能用于整数运算，而不支持浮点数运算。而bc则不一样：
``` shell
#!/bin/bash

echo "4 * 0.56" | bc               #2.24

a=12
result=`echo "$a * 1.5" | bc`
echo $result                       #18.0

echo "scale=3;3/8" | bc   #0.375 通过参数scale=2设置小数位个数为3

echo "sqrt(100)" | bc     #10 计算平方根和平方
echo "10^2" | bc          #100

num1=100                            
echo "obase=2;$num1" | bc          #1100100 把十进制转为二进制 

num2=1100100
echo "obase=10;ibase=2;$num2" |bc  #100 把二进制转为十进制
```

_ _ _ 
OK! The end!
