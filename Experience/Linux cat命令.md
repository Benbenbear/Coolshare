cat本身表示concatenate（拼接），在我们日常工作中经常会用到。下面列举一些常用用法：

1. 读取文件内容
``` shell
[benbenbear@benbenbear temp]$ cat file1 file2 
AAAAAAAAA
BBBBBBBBB
CCCCCCCCC
DDDDDDDDD
```

2. 读取标准输入
``` shell
[benbenbear@benbenbear temp]$ ls | cat
file1
file2
file3
file4
file.py
[benbenbear@benbenbear temp]$ echo "hello" | cat - file1
hello
AAAAAAAAA
BBBBBBBBB
```

3. 显示行号(不会修改文件本身的内容)
``` shell
[benbenbear@benbenbear temp]$ cat -n file1
     1	AAAAAAAAA
     2	BBBBBBBBB
```

4. 空白行不显示行号
```
[benbenbear@benbenbear temp]$ cat -b file4
     1	GGGGGGGGGG


     2	HHHHHHHHHH

     3	IIIIIIIIII
```

5. 压缩空白行(会把文本中的多个空行压缩成单个空行，其实也可以用tr移除空行)
``` shell
[benbenbear@benbenbear temp]$ cat -ns file4
     1	GGGGGGGGGG
     2	
     3	HHHHHHHHHH
     4	
     5	IIIIIIIIII
[benbenbear@benbenbear temp]$ cat -n file4
     1	GGGGGGGGGG
     2	
     3	
     4	HHHHHHHHHH
     5	
     6	IIIIIIIIII
[benbenbear@benbenbear temp]$ cat file4 | tr -s '\n' 
GGGGGGGGGG
HHHHHHHHHH
IIIIIIIIII
[benbenbear@benbenbear temp]$ cat -n file4 | tr -s '\n' #这样是不对的
     1	GGGGGGGGGG
     2	
     3	
     4	HHHHHHHHHH
     5	
     6	IIIIIIIIII
[benbenbear@benbenbear temp]$ cat -b file4 | tr -s '\n'  #这样是可以的
     1	GGGGGGGGGG
     2	HHHHHHHHHH
     3	IIIIIIIIII
```

6. 显示文本原始格式（制表符显示为^I）
```
[benbenbear@benbenbear temp]$ cat file.py
def function():
	var = 5
        next = 6
	third = 7   
[benbenbear@benbenbear temp]$ cat -T file.py 
def function():
^Ivar = 5
        next = 6
^Ithird = 7 
```
其实我们可以用`cat -A`来显示得更好，也可以用`sed`来完成这项工作。
```
[benbenbear@benbenbear temp]$ cat -A file.py 
def function():$
^Ivar = 5$
        next = 6$
^Ithird = 7   $
[benbenbear@benbenbear temp]$ sed l -n file.py
def function():$
\tvar = 5$
        next = 6$
\tthird = 7   $
```

关于cat更多的详细信息请参考man手册。Gook Luck!


