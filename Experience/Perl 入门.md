来公司实习接触了Perl语言，当时整理了一些杂记，现在把它同步过来吧。参考书是《Learning Perl》。
#####Chapter 1 简介
* 一个简单的perl程序
``` perl
#!/usr/bin/perl
print "hello,world!\n";
```
* `perldoc` 可以查看perl的相关文档
* 可以通过`which`查看perl在哪里
* `perl myprogram` 可以执行或者`./myprogram`运行(前提是先赋予x权限)

#####Chapter 2 标量数据
* 数字 所有数字的内部格式都相同(都是按照double-precision
floating-point)     
   浮点数直接量   
   整数直接量 61298040283768 612\_980\_4028\_3768(它们是一样的,不是用逗号来分隔)     
   非十进制的整数直接量   
   数字操作符    
* 字符串  
  单引号内的字符串直接量 ` '\'\\' ` 表示单引号和斜线2个字符   
  双引号内的字符串直接量   
* 字符串操作符  
  连接操作符 `.`  
```
"hello" . "world"        //"helloworld"
"hello" . ' ' . "world"  //'hello world'
'hello world' . "\n"     //"hello world\n"
```
  重复操作符 x `5 x 4.8` //本质上是"5"x4 5555 当重复次数小于1时会生成
  长度为0的字符串    
  数字与字符串之间的自动转换  
<ul><li>Perl内置警告信息<br/></ul>   
```
a. #!/usr/bin/perl
   use warnings;
b. $ perl -w my_program
c. #!/usr/bin/perl-w
d. #!perl -w
```  
* 标量变量   
  给变量取个好名字   
  标量的赋值   
  双目赋值操作符(+= *= .=)   
* 用print输出结果   
  字符串中的标量变量内插   
```
$hello = "my name is $name";(看起来舒服)
$hello = 'my name is' .$name;
print "$hello";
print $hello;(尽量用下面,免得被嘲笑)
```  
  借助代码点创建字符  
<ul><li>操作符的优先级与结合性(尽量用括号,不要自己为难自己)</br></ul>   
  比较操作符   
```
比较 数字 字符串
相等 == eq
不等 != ne
小于 < lt
大于 > gt
小于等于 <= le
大于等于 >= ge
```
* if控制结构   
``` perl
  if(...){
  ....
  }
  
  if(...){
  ...
  }else{
  ...
  }
```
  **important:if条件语句中的代码块周围一定要加上{}.**   
  布尔值  
  字符串` '0' `会被当成假的唯一非空字符串  
<ul><li>获取用户输入</br></ul>  
```
$line = <STDIN>;     
chomp操作符   
chomp($text = <STDIN>);读入文字,略过最后的换行符  
chomp()本质上是函数,返回值是移除的字符数,如果后面有2个换行符,移除其中一个；如果没有就什么也不做,返回0.
```     
* while控制结构  
  undef值(0或者空字符串)  
  defined函数
_ _ _   
OK，将就看一下吧！
