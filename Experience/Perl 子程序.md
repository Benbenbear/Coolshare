Perl中子程序也就是用户自定义函数，子程序的名称也是由字母、下划线和数字组成，但不能以数字开头。
* 定义子程序  
使用关键字sub,子程序名以及花括号封闭起来的代码块。子程序可以定义在程序中的任意位置，如果有两个重名的子程序，后面一个会覆盖前面一个。
* 调用子程序   
可以在任意表达式中使用子程序名（前面加上&）来调用，通常还会在后面加上一对括号。

``` perl
#!/usr/bin/perl
use warnings;

sub hello {
  $n += 1;
  print "Hello, $n!\n";
}

&hello;
&hello();
```
``` perl sub_define_result
[benbenbear@benbenbear perl]$ perl sub_define 
Hello, 1!
Hello, 2!
```
* 返回值  
在Perl中，所有子程序都有一个返回值，最后执行的表达式（而非程序代码的最后一行）的结果，不管是什么都会自动当成子程序的返回值。
* 参数、子程序中的私有变量  
默认情况下，Perl里面所有的变量都是全局变量，但是可以借助`my`操作符来创建私有变量。

``` perl
#!/usr/bin/perl
use warnings;

sub max {
  my($m, $n) = @_;                    #这个程序具有2个标量参数，在程序内部，分别是$m和$n.
  if ($m > $n) { $m } else { $n }
}
$n = &max(10, 15);
print "$n\n";
```
``` perl subroutine_result
[benbenbear@benbenbear perl]$ perl subroutine 
15
```
* 变长参数列表

``` perl
sub max {
  if (@_ != 2) {
    print "Warning! &max should get exactly two arguments!\n";
  }
  ... #其余代码和上面一样
}
```
* 改进的&max子程序

``` perl
#!/usr/bin/perl
use warnings;

$maximum = &max(3, 5, 23, 13, 9); #可以接受任意数目的参数
print "$maximum\n";
sub max {
  my($max_so_far) = shift @_;
  foreach (@_) {
    if ($_ > $max_so_far) {
      $max_so_far = $_;
    }
  }
  return $max_so_far; #return????
}
```
``` perl max_result
[benbenbear@benbenbear perl]$ perl max 
23
```
* 关于词法（my）变量  
在my操作符不加括号时，只能用来声明单个词法变量：

```
my $m, $n;  #错，没声明$n
my($m, $n); #两个都声明了
```
在日常的Perl编程中，最好对每个新变量都使用my声明，让它保持在自己所在的词法作用域内。
* use strict 编译指令  
* return 操作符  
关键字return常见的用法：立即返回某个值，而不再执行子程序的其余部分。
* 省略与号&  
除非你知道Perl所有的内置函数名，否则请务必在调用函数时使用与号&。
* 持久性私有变量  
在子程序中可以使用my操作符来创建私有变量，但每次调用这个子程序的时候，这个变量都会被重新定义。而使用`state`操作符来声明变量，我们便可以在子程序的多次调用期间保留变量之前的值，并将变量的作用域局限于子程序内部。
具体细节可以参考：[Perldoc](http://perldoc.perl.org/perlsub.html#Persistent-Private-Variables "Perldoc"), [Perlmaven ](http://cn.perlmaven.com/what-is-new-in-perl-5.10--say-defined-or-state "Perlmaven")。

_ _ _
OK! Good Luck!



