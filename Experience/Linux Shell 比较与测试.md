**1. if和else** 
```
if condition;
then
  commands;
fi
```
```
if condition;
then
  commands;
elif condition;
then
  commands;
else
  commands;
fi
```
if和else语句可以嵌套，但是可以用逻辑运算符将它变得简洁一些：
```
[ condition ] && action; #如果condition为真，则执行action
[ condition ] || action; #如果condition为假，则执行action
```
**2. 算术比较**
[ $var -eq 0 ] #一定要注意在[]与操作数之间有一个空格。
 一些重要的操作符：
 * -gt： 大于
 * -lt： 小于
 * -ge： 大于或等于
 * -le： 小于或等于
 * -eq： 等于
 * -ne： 不等于  
 
还可以结合使用：
```
[ $var1 -ne 0 -a $var2 -gt 3 ] #使用逻辑与-a
[ $var1 -ne 0 -o $var2 -gt 3 ] #使用逻辑或-o
``` 

**3. 文件系统相关测试**
* [ -f $var ]: 如果是正常的文件路径或文件名，则返回真
* [ -x $var ]: 如果文件可执行，则返回真
* [ -d $var ]: 如果是目录，则返回真
* [ -e $var ]: 如果文件存在，则返回真
* [ -c $var ]: 如果是字符设备文件，则返回真
* [ -b $var ]: 如果是块设备文件，则返回真
* [ -w $var ]: 如果文件可写，则返回真
* [ -r $var ]: 如果文件可读，则返回真
* [ -L $var ]: 如果是一个符号链接，则返回真

**4. 字符串比较**
* [[ $str1 = $str2 ]]: 如果str1等于str2时返回真      # 在等号”=“前后各有一个空格，如果不加空格，就变成赋值了
* [[ $str1 == $str2 ]]：如果str1等于str2时返回真 
* [[ $str1 != $str2 ]]： 如果str1不等于str2时返回真 
* [[ $str1 > $str2 ]]： 如果str1大于str2时返回真 
* [[ $str1 < $str2 ]]： 如果str1小于str2时返回真 
* [[ -z $str ]]： 如果str包含的是空字符串时返回真
* [[ -n $str ]]： 如果str包含的是非空字符串时返回真

**5. test命令**
test命令也可以用来作条件检测，前面所述的`[]`中的测试条件同样可以用于test命令。
```
if [ $var -eq 0 ]; then echo "True"; fi
if test $var -eq 0; then echo "True"; fi
```
上面两种写法是等价的。

_ _ _
OK, Good Luck!
