接着之前的[python学习笔记#1](https://github.com/Benbenbear/Coolshare/blob/master/Experience/python%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0%231.md).         
`pro10.py 局部变量`
``` python
#!/usr/bin/python

def func(x):
    print 'x is', x
    x = 2
    print 'Changed local x to', x

x = 50
func(x)
print 'x is still', x
```
<pre><code>[benbenbear@benbenbear python]$ python pro10.py 
x is 50
Changed local x to 2
x is still 50
</pre></code>
`PS: x是函数的局部变量，当我们在函数内改变时，在主块中定义的x不受影响。`

`pro11.py global全局变量`
``` python
#!/usr/bin/python

def func():
    global x
    print 'x is', x
    x = 2
    print 'Changed local x to', x
x = 50
func()
print 'Value of x is', x
```
<pre><code>
[benbenbear@benbenbear python]$ python pro11.py
x is 50
Changed local x to 2
Value of x is 2
</pre></code>
`PS: 可以使用同一个global语句指定多个全局变量，global x, y, z。`

`pro12.py 默认参数值`
``` python
#!/usr/bin/python

def say(message, times = 1):
    print message * times
say('Hello')
say('World', 5)
```
<pre><code>[benbenbear@benbenbear python]$ python pro12.py
Hello
WorldWorldWorldWorldWorld
</pre></code>
`PS: 只有在形参表末尾的那些参数可以有默认参数值。def func(a, b = 5)是有效的，而def func(a = 5, b)是无效的。`

`pro13.py 关键参数`
``` python
#!/usr/bin/python

def func(a, b = 5, c = 10):
    print 'a is', a, 'and b is', b, 'and c is', c

func(3, 7)
func(25, c = 24)
func(c = 50, a = 100)
```
<pre><code>[benbenbear@benbenbear python]$ python pro13.py
a is 3 and b is 7 and c is 10
a is 25 and b is 5 and c is 24
a is 100 and b is 5 and c is 50
</pre></code>
`PS: 关键参数不必担心参数的顺序。`

`pro14.py return语句`
``` python
#!/usr/bin/python

def maximum(x, y):
    if x > y:
        return x
    else:
        return y

print maximum(2,3)
```
<pre><code>[benbenbear@benbenbear python]$ python pro14.py
3
</pre></code>
`PS: 没有返回值的return语句等价于return None,None是python中表示没有任何东西的特殊类型，除非提供自己的return语句，每个函数都在结尾含有return None。`

`pro15.py DocStrings`
``` python
#!/usr/bin/python

def printMax(x, y):
    '''Prints the maximum of two numbers.

    The two values must be integers.'''
    x = int(x)
    y = int(y)

    if x > y:
        print x, 'is maximum'
    else:
        print y, 'is maximum'

printMax(3, 5)
print printMax.__doc__
help(printMax)
```
``` 
[benbenbear@benbenbear python]$ python pro15.py
5 is maximum
Prints the maximum of two numbers.

    The two values must be integers.
Help on function printMax in module __main__:

printMax(x, y)
    Prints the maximum of two numbers.
    
    The two values must be integers.

```
`PS: 在函数的第一个逻辑行的字符串是这个函数的文档字符串。文档字符串的惯例是一个多行字符串，首行以大写字母开始，句号结尾；第二行是空行，从第三行开始是详细描述。可以使用__doc__调用printMax函数的文档字符串属性。`

`pro 16.py 使用sys模块`
``` python
#!/usr/bin/python

import sys

print 'The command line arguments are:'
for i in sys.argv:
    print i
print '\n\nThe PYTHONPATH is', sys.path, '\n'
```
<pre><code>[benbenbear@benbenbear python]$ python pro16.py hello world !
The command line arguments are:
pro16.py
hello
world
!


The PYTHONPATH is ['/home/benbenbear/Work/python', '/usr/lib/python26.zip', '/usr/lib/python2.6', '/usr/lib/python2.6/plat-linux2', '/usr/lib/python2.6/lib-tk', '/usr/lib/python2.6/lib-old', '/usr/lib/python2.6/lib-dynload', '/usr/lib/python2.6/site-packages', '/usr/lib/python2.6/site-packages/gtk-2.0', '/usr/lib/python2.6/site-packages/webkit-1.0']
</pre></code>
`PS: 利用import语句输入sys模块，脚本的名称总是sys.argv列表的第一个参数。为了在其他程序中重用模块，模块的文件名必须以.py为扩展名。如果想输入argv变量到程序中，可以使用from sys import argv语句,如果想输入所有sys模块使用的名字，可以使用from sys import *。`

`pro17.py 模块的__name__`
``` python
#!/sur/bin/python

if __name__ == '__main__':
    print 'This program is being run by itself'
else:
    print 'I am being imported from another module'
```
<pre><code>[benbenbear@benbenbear python]$ python pro17.py
This program is being run by itself
[benbenbear@benbenbear python]$ python
Python 2.6.6 (r266:84292, Feb 21 2013, 19:27:01) 
[GCC 4.4.7 20120313 (Red Hat 4.4.7-3)] on linux2
Type "help", "copyright", "credits" or "license" for more information.
\>>> import pro17
I am being imported from another module
\>>> 
</pre></code>
`PS: 每个python模块都有它的__name__,如果它是'__main__',这说明这个模块被用户单独运行。`

`pro18 编写自己的模块`
<pre><code>[benbenbear@benbenbear pro18]$ tree
.
|-- demo.py
|-- mymodule.py
`-- pro18.py

0 directories, 3 files
</pre></code>
``` python 
#!/usr/bin/python

def sayhello():
    print 'Hello, This is benbenbear.'

version = '0.1'
``` 
``` python 
#!/usr/bin/python

import mymodule

mymodule.sayhello()
print 'version', mymodule.version
```
<pre><code>[benbenbear@benbenbear pro18]$ python pro18.py 
Hello, This is benbenbear.
version 0.1
</pre></code>
`PS: 这个模块应该放置在我们输入它的程序的同一目录中，或者在sys.path所列目录之一。`
``` python
#!/usr/bin/python

from mymodule import sayhello, version

sayhello()
print 'version', version
```
<pre><code>[benbenbear@benbenbear pro18]$ python demo.py 
Hello, This is benbenbear.
version 0.1
</pre></code>

`dir()函数`      
可以用来列出模块定义的标识符，包括函数，类和变量。当给`dir()`提供一个模块名的时候，它返回模块定义的名称列表，如果不提供参数，它返回当前模块中定义的名称列表。
<pre><code>[benbenbear@benbenbear python]$ python
Python 2.6.6 (r266:84292, Feb 21 2013, 19:27:01) 
[GCC 4.4.7 20120313 (Red Hat 4.4.7-3)] on linux2
Type "help", "copyright", "credits" or "license" for more information.
\>>> dir()
['__builtins__', '__doc__', '__name__', '__package__']
\>>> a = 10
\>>> dir()
['__builtins__', '__doc__', '__name__', '__package__', 'a']
\>>> del a
\>>> dir()
['__builtins__', '__doc__', '__name__', '__package__']
\>>> 
</pre></code>
好吧，第二次就到这了。接下来第三次会更新一些python的数据结构。
