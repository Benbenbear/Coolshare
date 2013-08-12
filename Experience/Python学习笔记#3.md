接着之前的[Python学习笔记#1](https://github.com/Benbenbear/Coolshare/blob/master/Experience/python%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0%231.md), [Python学习笔记#2](https://github.com/Benbenbear/Coolshare/blob/master/Experience/python%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0%232.md).         
这次主要是有关Python的数据结构的知识。Python有三种内建的数据结构--列表，元组和字典。 
     
`pro19.py 列表`
``` python 
#!/usr/bin/python

friends = ['jack', 'paul', 'kevin', 'david']

print 'I have', len(friends), 'good friends.'

print 'They are:',
for friend in friends:
    print friend,

print '\nI also have a new friend.'
friends.append('roger')
print 'my friends list is now', friends

print 'I will sort my list now'
friends.sort()
print 'Sorted friends list is', friends

print 'The first friend is' ,friends[0]
oldfriend = friends[0]
del friends[0]
print 'Old frined is', oldfriend
print 'my friends list is now', friends
```
<pre><code>[benbenbear@benbenbear python]$ python pro19.py
I have 4 good friends.
They are: jack paul kevin david 
I also have a new friend.
my friends list is now ['jack', 'paul', 'kevin', 'david', 'roger']
I will sort my list now
Sorted friends list is ['david', 'jack', 'kevin', 'paul', 'roger']
The first friend is david
Old frined is david
my friends list is now ['jack', 'kevin', 'paul', 'roger']
</pre></code>
`PS: 列表是可变的而字符串是不可变的。可以在print语句的末尾使用逗号来消除每个print语句自动打印的换行符。`

`pro20.py 元组`
``` python
#!/usr/bin/python

zoo = ('wolf', 'elephant', 'penguin')
print 'Number of animals in the zoo is', len(zoo)

new_zoo = ('monkey', 'dolphin', zoo)
print 'Number of animals in the new zoo is', len(new_zoo)
print 'All animals in the new zoo are', new_zoo
print 'Animals brought from old zoo are', new_zoo[2]
print 'Last animal brought from old zoo is', new_zoo[2][2]
```
<pre><code>[benbenbear@benbenbear python]$ python pro20.py 
Number of animals in the zoo is 3
Number of animals in the new zoo is 3
All animals in the new zoo are ('monkey', 'dolphin', ('wolf', 'elephant', 'penguin'))
Animals brought from old zoo are ('wolf', 'elephant', 'penguin')
Last animal brought from old zoo is penguin
</pre></code>
`PS: `
`1. 列表中的列表不会像perl中那样被打散，同样元组中的元组，元组中的列表，列表中的元组都一样不会被打散。在python中，始终使用另一个对象存储的对象。`
`2. 含有0个或1个项目的元组.一个空的元组由一对空的括号组成，如：empty=();含有单个元素的元组必须在唯一一个项目后面跟一个逗号，如：hello(2,)。`

`pro21.py 元组与打印语句`
``` python
#!/usr/bin/python

age = 22
name = 'James'

print '%s is %d years old' % (name, age)
print 'Why is %s playing with that python?' % name
```
<pre><code>[benbenbear@benbenbear python]$ python pro21.py
James is 22 years old
Why is James playing with that python?
</pre></code>
`PS: 如果字符串中只有一个定制的时候，%后面可以不加括号，像上面的第二个语句。`

`pro22.py 字典`
``` python
#!/usr/bin/python

ab = { 'james' : 'james@hello.com',
       'paul'  : 'paul@world.com',
       'tom'   : 'tom@share.org',
       'robin' : 'robin@python.info'
     }
print "james's address is %s" % ab['james']

ab['david'] = 'david@boss.org'
del ab['robin']

print '\nThere are %d contacts in the address-book\n' % len(ab)
for name, address in ab.items():
    print 'Contact %s at %s' % (name, address)

if 'david' in ab:
    print "\ndavid's address is %s" % ab['david']
```
<pre><code>
[benbenbear@benbenbear python]$ python pro22.py
james's address is james@hello.com

There are 4 contacts in the address-book

Contact james at james@hello.com
Contact paul at paul@world.com
Contact david at david@boss.org
Contact tom at tom@share.org

david's address is david@boss.org
</pre></code>
`PS: 键必须是唯一的，只能使用不可变的对象作为字典的键。d = {key1 ：value1, key2 : value2}.`

`pro23.py 序列`
``` python
#!/usr/bin/python

shoplist = ['apple', 'mango', 'carrot', 'banana']

print 'Item 0 is', shoplist[0]
print 'Item 1 is', shoplist[1]
print 'Item 2 is', shoplist[2]
print 'Item 3 is', shoplist[3]
print 'Item -1 is', shoplist[-1]
print 'Item -2 is', shoplist[-2]

print 'Item 1 to 3 is', shoplist[1:3]
print 'Item 2 to end is', shoplist[2:]
print 'Item 1 to -1 is', shoplist[1:-1]
print 'Item start to end is', shoplist[:]

name = 'benbenbear'
print 'characters 1 to 3 is', name[1:3]
print 'characters 2 to end is', name[2:]
print 'characters 1 to -1 is', name[1:-1]
print 'characters start to end is', name[:]
```
<pre><code>
[benbenbear@benbenbear python]$ python pro23.py
Item 0 is apple
Item 1 is mango
Item 2 is carrot
Item 3 is banana
Item -1 is banana
Item -2 is carrot
Item 1 to 3 is ['mango', 'carrot']
Item 2 to end is ['carrot', 'banana']
Item 1 to -1 is ['mango', 'carrot']
Item start to end is ['apple', 'mango', 'carrot', 'banana']
characters 1 to 3 is en
characters 2 to end is nbenbear
characters 1 to -1 is enbenbea
characters start to end is benbenbear
</pre></code>
`PS: 序列的两个特点是索引操作符和切片操作符。列表，元组和字符串都是序列。python从0开始计数。切片操作符中的第一个数表示切片开始的位置，第二个数表示切片到哪里结束，不包含第二个数。`  
`pro24.py 对象与参考`
``` python
#!/usr/bin/python

print 'Simple Assignment'
shoplist = ['apple', 'mango', 'carrot', 'banana']
mylist = shoplist

del shoplist[0]

print 'shoplist is ', shoplist
print 'mylist is', mylist

print 'Copy making a full slice'
mylist = shoplist[:]
del mylist[0]

print 'shoplist is', shoplist
print 'mylist is', mylist
```
<pre><code>
[benbenbear@benbenbear python]$ python pro24.py
Simple Assignment
shoplist is  ['mango', 'carrot', 'banana']
mylist is ['mango', 'carrot', 'banana']
Copy making a full slice
shoplist is ['mango', 'carrot', 'banana']
mylist is ['carrot', 'banana']
</pre></code>
`PS: 如果要复制一个列表或者类似的序列，必须使用切片操作符来取得拷贝。`

`pro25.py 字符串的方法`
``` python
#!/usr/bin/python

name = 'benbenbear'

if name.startswith('ben'):
    print 'Yes, the string starts with "ben"'

if 'r' in name:
    print 'Yes, it contains the string "r"'

if name.find('bear') != -1:
    print 'Yes, it contains the string "bear"'

delimiter = '_*_'
mylist = ['Brazil', 'Russia', 'India', 'China']
print delimiter.join(mylist)
```
<pre><code>[benbenbear@benbenbear python]$ python pro25.py 
Yes, the string starts with "ben"
Yes, it contains the string "r"
Yes, it contains the string "bear"
Brazil_*_Russia_*_India_*_China
</pre></code>
`PS: startswith用来测试字符串是否以给定字符串开始，in检查某个字符串是不是另一个字符串的一部分，find用于找出特定字符串在某字符串中的位置，返回-1表示找不到,join返回一个生成的大字符串。`

关于Pyhthon的数据结构就先到这吧，忘记带笔记本电源回来，没法work了。下次继续吧！Good Luck！
