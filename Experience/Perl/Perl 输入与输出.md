* 读取标准输入  
读取标准输入流使用`<STDIN>`。

``` perl 
#!/usr/bin/perl
use warnings;

while (<STDIN>) {
  print "I saw $_";
}

foreach (<STDIN>) {
  print "I saw $_";
}
```
对于上面两个程序，最好的做法是尽量使用while循环的简写，因为二者背后的运作方式是不一样的。在while循环里，Perl会读取一行输入，把它存入某个变量并且执行循环的主体，接下来再回头寻找其他的输入行，但是在foreach循环里，它必须先将输入行全部读进来。加入输入来自一个大文件，差异显而易见。  

* 来自钻石操作符的输入

``` perl
#!/usr/bin/perl
use warnings;

while (<>) {
  chomp;
  print "I saw $_!\n";
}
```
钻石操作符通常会处理所有的输入，所以一旦看到它出现在程序中多处时，通常是错误的。

* 调用参数
钻石操作符会查看数组@ARGV，然后决定用哪些文件名，如果为空就使用标准输入流，否则使用@ARGV里的文件。

``` perl
#!/usr/bin/perl
use warnings;

@ARGV = qw# test1 test2 #;
while (<>) {
  chomp;
  print "I saw $_!\n";
}
```
``` perl stdin_result
[benbenbear@benbenbear perl]$ perl stdin2 
I saw AAAAAAAAAA!
I saw BBBBBBBBBB!
I saw CCCCCCCCCC!
I saw DDDDDDDDDD!
```
* 输入到标准输出
print会读取后续列表中的所有元素，并把每一项依次送到标准输出。

```
print @array;   #把数组的元素打印出来
print "@array"; #打印出一个字符串
print "@array\n" #其实在使用引号的场合，最好在后面加上“\n”，如果数组字符串中包含换行符避免没有对齐的状况

print <>;      #相当于Unix下的cat命令
print sort <>; #相当于Unix下的sort命令

$result = print("hello world!\n"); #通常是1，print的返回值不是真就是假。

print (2+3)*4; #输出结果是5，不是20哟，其实相当于 (print(2+3))*4;
```
* 用printf格式化输出
这个和C语言非常类似。如果想输出恰当的数字形式，可以使用%g，它会自动选择浮点数，整数甚至是指数。%d表示十进制整数，会无条件截断小数点后面的数字，如果宽度字段是负数，则会左对齐，%%表示百分号。
* 数组和printf
在程序运行时动态产生格式字符串，对于调试是非常有帮助的。

``` perl
#!/usr/bin/perl
use warnings;

my @items = qw( hello perl world );
my $format = "The items are:\n".("%10s\n" x @items);
printf $format, @items;
printf "The items are:\n".("%10s\n" x @items), @items; #上面两句可以合并为下面一句
```
``` perl print_result
[benbenbear@benbenbear perl]$ perl print 
The items are:
     hello
      perl
     world
The items are:
     hello
      perl
     world
```
* 文件句柄
建议使用全大写字来命名文件句柄，避免与Perl保留字冲突。有6个特殊文件句柄名是Perl保留的，它们是：STDIN、STDOUT、STDERR、DATA、ARGV、ARGVOUT。
* 打开文件句柄

``` perl
open CONFIG, 'dino';
open CONFIG, '<dino';   #和上一句完全相同
open BEDROCK, '>fred';
open LOG, '>>logfile';

open CONFIG, '<', 'dino';         #尽量使用三参数形式写法
open BEDROCK, '>', $file_name;
open LOG, '>>', &logfile_name();

open CONFIG, '<:encoding(UTF-8)', 'dino'; #指定编码方式
open BEDROCK, '>:utf8', $file_name; #可能会有问题
```
* 关闭文件句柄
`close BEDROCK;` 但是如果想写得工整一些，请为每个open搭配一个close，最好是在每个文件句柄用完之后就立刻关闭它。
* 用die处理致命错误

``` perl
if (@ARGV < 2) {
  die "Not enough arguments: $!"; #这种方式有利于调试过程中追踪相关的错误信息，例如行号，权限不足等。
}
if (@ARGV < 2) {
  die "Not enough arguments.\n"; #这种用于提示用法错误。
}
```
请一定记得检查open的返回值，因为之后的代码必须在文件打开成功时才顺利运行。
* 用warn送出警告信息  
warn的功能就是产生类似于Perl的内置警告信息的信息，和die差不多，不同之处在于它不会终止程序的运行。
* 自动检测致命错误  
`use autodie;` 一旦发现系统调用出错，autodie便会自动帮你调用die，而它发出的错误信息也大体和我们自己组织的不相上下。
* 使用文件句柄

```
printf (STDERR "%d percent complete.\n", 100); #注意文件句柄和输出的内容之间没有逗号
printf STDERR ("%d percent complete.\n", 100);
```
* 改变默认的文件输出句柄
可以使用select操作符来改变默认的文件句柄，但是请注意当你用完之后，最好把它设为原先的默认值STDOUT。

``` perl
select LOG;
...
select STDOUT;
```
* 标量变量中的文件句柄

``` perl
#!/usr/bin/perl
use warnings;

open my $rock_fh, '<', 'rock.txt'
  or die "Could not open rock.txt: $!";
```
``` perl die_result
[benbenbear@benbenbear perl]$ perl die 
Could not open rock.txt: No such file or directory at die line 4.
```
```
print STDOUT;
print $rock_fh;  #错误，这应该不是你的本意
print { $rock_fh }; #默认打印$_中的内容
print { $rocks[0] } "sandstone\n";
```
根据实际情况，选择使用裸字或者标量变量都没问题，小程序用裸字也可以，不过对于大一点的项目，使用标量方式可以精确控制文件句柄的作用域，方便调试和维护。
_ _ _
OK! Good Luck!
