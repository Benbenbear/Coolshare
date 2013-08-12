#####Chapter 3 列表与数组
* perl里标量代表的是单数,列表与数组代表复数  
  列表指数据,数组指变量 列表的值不一定放在数组里,但是数组至少包含一个列表
* 访问数组中的元素  
  $fred[0] = "yabba"; (下标从0开始,如果不是整数,则会自动舍弃小数；下标超出数组尾端或者未使用则为undef)
* 特殊的数组索引  
  最后一个元素的索引值 $#rocks  
  $number\_of\_rocks = $#rocks + 1;  
  超出数组大小的负数索引值是不会绕回来的.  
* 列表直接量  
  注意 (5..1) //空列表,只能向上计数
* qw简写  
  可以使用任何标点符号作为界定符  
  qw( hello world perl language );  
* 列表的赋值  
  ($fred, $barney, $dino) = ("flintstone", "rubble", undef);  
  交换2个值 ($fred, $barney) = ($barney, $fred);  
  ($betty[0], $betty[1]) = ($betty[1], $betty[0]);  
  @rocks = qw/ bedrock slate lave /;  
  @copy = @quarry; //将一个数组中的列表复制到另一个数组  
* pop和push操作符  
  数组当作堆栈(stack)  
  pop:取出数组中最后一个元素,并将其作为返回值返回  
  @array = 5..9;  
  $fred = pop(@array); //$fred变成9,@array是(5,6,7,8)  
  $barney = pop(@array);//$barney变成8,@array是(5,6,7)  
  pop @array; //@array现在是(5,6),相当于删除数组中的最后一个元素  
  push:添加一个元素或者一串元素到数组尾端  
  push(@array,0); //@array现在是(5,6,0)  
  push @array,8; //@array现在是(5,6,0,8)  
  push @array,1..10;  
  @others = qw/ 9 0 2 1 0 /;  
  push @array,@others;  
  注意:pop的唯一参数或者push的第一个参数都必须是要操作的数组变量,对列表进行pop(弹出)或者push(压入)操作是没有意义的
* shift和unshift操作符  
  处理数组的开头,与pop,push相反  
  @array = qw# dino fred barney #;  
  $m = shift (@array); //$m变成"dino",@array是"fred, barney"  
  $n = shift @array; //$n变成"fred",@array是"barney"  
  shift @array; //现在@array变成空了  
  $o = shift @array; //$o变成undef,@array还是空的  
  unshift (@array,5); //@array现在仅包含一个元素的列表(5)  
  unshift @array,4; //@array现在是(4,5)  
  @others = 1..3;  
  unshift @array, @others; //@array现在是(1,2,3,4,5)  
  注意:对一个空数组变量,shift会返回undef  
* splice操作符：添加或移除数组中间的某些元素  
  可接受4个参数,后两个是可选参数
<pre><code>perl @array = qw( pebbles dino fred barney betty );
@removed = splice @array,2; //@removed现在是qw( fred barney betty )
@array现在是qw( pebbles dino )
@array = qw ( pebbles dino fred barney betty );
@removed = splice @array,1, 2; //@removed现在是qw( dino fred )
@array现在是qw( pebbles barney betty )
@array = qw ( pebbles dino fred barney betty );
@removed = splice @array,1,2,qw(wilma);//@removed现在是qw( dino fred )
@array现在是qw( pebbles wilma barney betty )
@array = qw ( pebbles dino fred barney betty );
@removed = splice @array,1,0,qw(wilma); //@removed现在是qw()
@array现在是 qw ( pebbles wilma dino fred barney betty );</pre><code>
* 字符串中的数组内插  
  $email = "fred@bedrock.edu"; 错误  
  $email = "fred\@bedrock.edu";正确  
  $email = 'fred@bedrock.edu';正确  
  注意:索引表达式会被当成普通字符串表达式处理  
  @fred = qw(hello world);  
  $y = 2;  
  $x = "This is $fred[1]'s place";//This is world's place  
  $x = "This is $fred[$y-1]'s place";(同上)  
  $y = '2*2';  
  $x = "This is $fred[$y-1]'s place";//This is world's place  
* 如果要在某个标量后面写[],需要先将这个[]隔开,才不至于被识别为数组的一部分.    
<pre><code>perl @fred = qw(eating rock is wrong);  
  $fred = "right";
  print "this is $fred[3]\n";
  print "this is ${fred}[3]\n";
  print "this is $fred"."[3]\n";
  print "this is $fred\[3]\n";</pre><code>
运行结果:
<pre><code>this is wrong
this is right[3]
this is right[3]
this is right[3]</pre><code>
* foreach控制结构  
  控制变量(control variable)并不是列表元索引的复制品,实际上它就是列表元素本身.假如在循环中修改了控制变量的值,也就同时修改了这个列表的元素.  
  perl会自动保存foreach循环的控制变量的值并在循环结束后还原  
  Perl最喜欢用的默认变量:$_  
* reverse操作符  
  读取列表的值,并按相反的次序返回该列表.但它并不会传递进来的参数  
  reverse @fred; 错误--这不会修改@fred的值  
  @fred = reverse @fred; 正确  
* sort操作符  
  有点和reverse类似,但是对数字排序时以1开头的会排在以9开头的字符串前面  
* each操作符  
  perl5.12版本开始,可以针对数组使用each操作符.(提取哈希的键值对,提取数
  组元素的索引和值)  
* 标量上下文和列表上下文(非常重要!!!)  
<pre><code>eg. @people = qw ( fred barney betty );
@sorted = sort @people; //列表上下文:barney betty fred
$number = 42 + @people; //标量上下文: 42 + 3 得45
在标量上下文中使用产生列表的表达式
@backwards = reverse qw/ yabba dabba doo /;
//会得到 doo,dabba,yabba
$backwards = reverse qw/ yabba dabba doo /;
//会得到 oodabbadabbay
在列表上下文中使用产生标量的表达式
@betty = (); //清空数组的正确方法
@wilma = undef; //糟糕,得到是包含一个元素为undef的列表
强制指定标量上下文
scalar 切换到标量上下文
列表上下文中的<STDIN>
chomp(@lines = <STDIN>);//读入所有行,换行符除外</pre><code>

_ _ _
OK,将就这样吧！Good Luck！
