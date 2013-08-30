哈希是一种数据结构，它和数组在于不同的索引方式，数组是以数字来索引，哈希是通过键来索引的，哈希就是一堆键-值对的集合罢了。这些键和值都是任意的标量，但键总会被转换成字符串。例如键50/20，会被转成含有三个字符的字符串”2.5“。值得一提的是：哈希里的键是唯一的，但它们对应的值是可以重复的，可以是数字、字符串、undef或是这些类型的组合。
* 访问哈希元素
使用如下方法可以访问哈希元素： $hash{$some_key}

```
$name{'James'} = 'jameswang';
$name{'Tom'} = 'tomyou';
```
访问哈希表里不存在的值会得到undef。
* 访问整个哈希  
要指代整个哈希，可以用百分号（%）作为前缀。
展开哈希 `@any_array = %some_hash;` 当然得到的键-值对不一定是按照当初赋值时的顺序展开，但是列表里的键还是会”黏着“相应的值。
* 哈希赋值  
哈希可以用一般的赋值语法来复制，但不常见。 `my %new_hash = %old_hash;` 但是根据现有哈希转换得到一个新的哈希是很常见的 `my %inverse_hash = reverse %any_hash;`，这个技巧最好在确定原始哈希的值是唯一的情况下使用。
* 胖箭头

``` perl
my %name = (
  'james' => 'jameswang', #箭头左边的单引号通常也可以省略
  'tom' => 'tomyou',
);
```
* 哈希函数  
**keys和values函数**

``` perl
#!/usr/bin/perl
use warnings;

my %hash = ('a' => 1, 'b' => 2, 'c' => 3);
my @keys = keys %hash;
my @values = values %hash;
print "@keys\n";
print "@values\n";

my $count = keys %hash;           #在标量上下文中，这2个函数都会返回哈希中元素的个数。
my $number = values %hash;
print "$count\n";
print "$number\n";
```
``` perl hash_result
[benbenbear@benbenbear perl]$ perl hash 
c a b
3 1 2
3
3
```
**each函数**

``` perl
#!/usr/bin/perl
use warnings;

my %hash = ('a' => 1, 'b' => 2, 'c' => 3);
while (($key,$value) = each %hash) {
  print "$key => $value\n";
}
```
``` perl each_result
[benbenbear@benbenbear perl]$ perl each 
c => 3
a => 1
b => 2
```
当然，each返回键-值对的顺序是乱的，但它与keys和values返回的顺序相同，假如要一次处理哈希，只要对键排序就可以了。
**exists 函数**
若要检查哈希中是否存在某个键，可以使用exists函数。

``` perl
#!/usr/bin/perl
use warnings;

my %hash = ('a' => 1, 'b' => 2, 'c' => 3);
if(exists $hash{"a"}) {
  print "Existsed!\n";
}
```
**delete 函数**
delete函数能从哈希中删除指定的键及其相应的值，假如没有这样的键，它就会直接结束，而不会出现任何警告和错误信息。

``` perl
#!/usr/bin/perl
use warnings;

my %hash = ('a' => 1, 'b' => 2, 'c' => 3);
delete $hash{"a"};
while (($key,$value) = each %hash) {
  print "$key => $value\n";
}
```
* 哈希元素内插
可以将单一哈希元素内插到双引号引起的字符串中，但这种方式不支持内插整个哈希。
* %ENV哈希
从%ENV中读取PATH键的值：`print "PATH is $ENV{PATH}\n";`

_ _ _
OK, Good Luck!
