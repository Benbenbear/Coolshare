
    有两种方式构建软件设计：一种是把软件做得很简单以至于明显找不到缺陷；另一种是把它做得很复杂以至于找不到明显的缺陷。
                                                                                   ——C.A.R. Hoare

    获得人生中的成功需要的专注与坚持不懈多过天才与机会。
                                                                                   ——C.W. Wendte
`pro1.py`     
``` python      
     #!/usr/bin/python
     
     i = 5     
     print i    
     
     i = i + 1    
     print i     
     
     s = '''This is a multi-line string,    
     This is the second line.'''    
     print s       
```           
<pre><code>[benbenbear@benbenbear python]$ python pro1.py    
5 
6 
This is a multi-line string, 
This is the second line.
</pre></code>    

`pro2.py`     
``` python 
#!/usr/bin/python

length = 5
breadth = 2
area = length * breadth

print 'Area is', area
print 'Perimeter is', 2 * (length + breadth)
```     
<pre><code>[benbenbear@benbenbear python]$ python pro2.py 
Area is 10
Perimeter is 14
</pre></code>
`PS: 在'Area is'和area之间没有打空格，输出结果python自动加上空格，很漂亮吧！`

`pro3.py`
``` python
#!/usr/bin/prthon

number = 23
guess = int(raw_input('Enter a integer : '))

if guess == number:
    print 'Congratulations, you guessed it'
    print "(but you do not win any prizes!)"
elif guess < number:
    print 'No, it is a little higher than that'
else:
    print 'No, it is a little lower than that'

print 'Done'
```    
<pre><code>[benbenbear@benbenbear python]$ python pro3.py 
Enter a integer : 21
No, it is a little higher than that
Done
[benbenbear@benbenbear python]$ python pro3.py 
Enter a integer : 25
No, it is a little lower than that
Done
[benbenbear@benbenbear python]$ python pro3.py 
Enter a integer : 23
Congratulations, you guessed it
(but you do not win any prizes!)
Done
</pre></code>
`PS: 行首的空白在python中很重要，同一层次的语句必须有相同的缩进．强烈建议使用一个TAB，两个空格或者四个空格进行缩进，并且坚持下去．`

`pro4.py`
``` python
#!/usr/bin/prthon

number = 23
running = True

while running:
    guess = int(raw_input('Enter a integer : '))

    if guess == number:
        print 'Congratulations, you guessed it'
        running = False
    elif guess < number:
        print 'No, it is a little higher than that'
    else:
        print 'No, it is a little lower than that'
else:
    print 'The while loop is over.'
print 'Done'
```      
<pre><code>[benbenbear@benbenbear python]$ python pro4.py 
Enter a integer : 24
No, it is a little lower than that
Enter a integer : 14
No, it is a little higher than that
Enter a integer : 23
Congratulations, you guessed it
The while loop is over.
Done
</pre></code>
`PS: 可以在while循环中使用一个else从句．`

`pro5.py`
``` python
#!/usr/bin/python

for i in range(1, 10, 2):
    print i
else:
    print 'The for loop is over'
```
<pre><code>[benbenbear@benbenbear python]$ python pro5.py 
1
3
5
7
9
The for loop is over
</pre></code>                
`PS: for循环中range默认歩长是１，可在第三参数指定．else部分是可选的，它总是在for循环结束后执行一次，除非遇到break语句．`

`pro6.py`
``` python
#!/usr/bin/python

while True:
    s = raw_input('Enter something : ')
    if s == 'quit':
        break
    print 'Length of the string is', len(s)
print 'Done'
```
<pre><code>[benbenbear@benbenbear python]$ python pro6.py 
Enter something : hello
Length of the string is 5
Enter something : what are
Length of the string is 8
Enter something : quit
Done
</pre></code>
`PS:break语句是用来终止循环语句，如果从for或while中终止，对应的else语句块将不会执行．`

`pro7.py`
``` python
#!/usr/bin/python

while True:
    s = raw_input('Enter something : ')
    if s == 'quit':
        break
    if len(s) < 3:
        continue
    print 'Input is of sufficient length'
```
<pre><code>[benbenbear@benbenbear python]$ python pro7.py 
Enter something : hello
Input is of sufficient length
Enter something : ben
Input is of sufficient length
Enter something : hi
Enter something : quit
</pre></code>
`PS: continue用来跳过当前循环中的剩余语句，重新开始下一伦循环，对for循环也有效．`

`pro8.py`
``` python
#!/usr/bin/python

def sayHello():
    print 'Hello World!'

sayHello()
```
<pre><code>[benbenbear@benbenbear python]$ python pro8.py
Hello World!
</pre></code>
`PS: 函数通过def关键字定义．`

`pro9.py`
``` python
#!/usr/bin/python

def printMax(a, b):
    if a > b:
        print a, 'is maximum'
    else:
        print b, 'is maximum'

printMax(3, 4)

x = 5
y = 7

printMax(x, y)
```
<pre><code>[benbenbear@benbenbear python]$ python pro9.py 
4 is maximum
7 is maximum
</pre></code>

第一次主要是熟悉Emacs和Octopree,下次再继续了．该休息了，明早还上班！     
Good Luck!!!    
