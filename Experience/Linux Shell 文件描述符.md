最常见的文件描述符是`stdin`，`stdout`和`stderr`。文件描述符0、1、2是系统预留的。

> 0 ----------- stdin （标准输入）  
> 1 ----------- stdout（标准输出）  
> 2 ----------- stderr（标准错误）  

``` shell
[benbenbear@benbenbear shell]$ echo "This is test1" > test.txt
[benbenbear@benbenbear shell]$ echo "This is test2" >> test.txt
[benbenbear@benbenbear shell]$ cat test.txt 
This is test1
This is test2
```
重定向操作符默认使用标准输出，如想使用特定的文件描述符，必须将描述符置于操作符之前才能生效。`>``和>>`都可以将文本进行重定向，但是前者在写入内容之前会清空之前的内容，而后者是把内容追加到原有内容的后面。
* 把stderr重定向到一个文件：`$ cmd 2> out.txt`.
* 把stderr重定向到一个文件，把stdout重定向到另一个文件： `$ cmd 2> stderr.txt 1> stdout.txt`.
* 把stderr转成stdout,把它们都重定向到一个文件： `$ cmd > out.txt 2>&1` OR `$ cmd &> out.txt`.
其实在实际中，我们经常会把有些信息重定向到`/dev/null`，该文件是个特殊的设备文件，这个文件接收到的任何数据都会被丢弃，所以常把null设备成为黑洞或者位桶（bit bucket）.
* 当然还有一个tee命令，可以一方面把数据重定向到文件，同时还可以提供一份重定向的副本作为后续命令的stdin。当然默认情况下tee会将文件覆盖，所以可以使用“-a”选项进行追加。
<pre><code>[benbenbear@benbenbear shell]$ echo how are you | tee test.txt | cat -n
     1	how are you
[benbenbear@benbenbear shell]$ echo how are you | tee -  #这里-代表tee命令的文件名参数
how are you
how are you
</code></pre>

文件描述符是用于访问文件的一个抽象指针。通常文件的打开模式有三种:
> 0 只读模式  
> 1 截断模式  
> 2 追加模式  

我们可以使用`exec`命令创建自定义的文件描述符。`<`用于从文件中读取至stdin，`>`用于截断模式的文件写入，`>>`用于追加模式的文件写入。
* 为读取文件创建一个文件描述符：  
<pre><code>[benbenbear@benbenbear shell]$ echo this is the test1 > input.txt 
[benbenbear@benbenbear shell]$ exec 3< input.txt 
[benbenbear@benbenbear shell]$ cat <&3
this is the test1
[benbenbear@benbenbear shell]$ cat <&3
[benbenbear@benbenbear shell]$ exec 8< input.txt
[benbenbear@benbenbear shell]$ cat <&8
this is the test1
</code></pre>
如果要再次读取，我们就不能再继续使用文件描述符3了，而是需要用exec重新分配以便于读取。  
* 为截断模式写入创建一个文件描述符：
<pre><code>[benbenbear@benbenbear shell]$ exec 4> output.txt
[benbenbear@benbenbear shell]$ echo hello shell >&4
[benbenbear@benbenbear shell]$ cat output.txt
hello shell
</code></pre>
* 为追加模式写入创建一个文描述符：
<pre><code>[benbenbear@benbenbear shell]$ exec 5>> output.txt
[benbenbear@benbenbear shell]$ echo hello shell again >&5
[benbenbear@benbenbear shell]$ cat output.txt 
hello shell
hello shell again
</code></pre>
最后补充一点小建议：就是当我们在进行重定向的时候最好在`>`，`>>`与文件之间保留一个空格，这也是《The UNIX-HATERS Handbook》一书中提到的。

_ _ _
The end! Good Luck!
