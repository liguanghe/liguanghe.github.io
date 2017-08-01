

- 大妈的时间记录账单
    - 手写
    - 2012年增加时段(tI, tO...)和番茄时间(Pt, Pd...)
```
$ls
$cat 
```

- 普适的可视化
    + 数据清理
    + 数据整理
    + 可视化
- 数据清理
```
# demo:
get all data line
fix format as .csv
clean no need space
```
文本字符串 转成 时间格式, 以我们喜欢的方式把文本输出出去. 


- 最终通过一组命令, 得到清洗过的数据
    - 命令
```
ls ../raw/zoomquiet/0812-1303/zq-*.txt | xargs -I{} cat {} | python stdin0handlog.py | python stdin1head.py | python stdin2year2sec.py | python stdin4pt2sec.py
```

    - 得出的最终数据
1364313600,6300,19800,3600,12600,20700,19800,9000,0,3000,9000
...

    - 对比原始人工数据
date,tI,tO,tC,tM,tF,tS   Pt,Pd,Pl,Po
120104, 0.00....

- 开发之前看 README.md

小白|高手
---|---
16-20行,看到把时间转成秒, 我也来写个脚本转秒,关键词是"yy",在标准库里面找, 没有找到.google 里面找,看到又现成的 app, 再搜这个关键词,不懂|先看默认库和模块, 标准库里都有.最常见的 demo.
?|doc.python.org/ 下载到本地, 常用200个库, 经常看. 跟 time 有关的, 到默认库检索 time.(官方模块千锤百炼)

- README.md
    + readme改了十几次, 可以回溯版本( git),对比不同版本的 README
    + 解释人工文本
        * 输入时间和番茄钟两种度量衡, 这局限于输入条件. 
        * 理解不同, 熊本把输入理解成输出.

小白|高手
---|--- 
串不起思路,是一次想到这几步么?|用命令行下的管道, 把一件事情拆分成不同的步骤.ls 的含义是把文件夹下面的文件打印出来, 加上条件,以 zq开头的参数,把每一行打印出来, 不用一个一个打. 用 python 处理.stdin0, 处理数据, 第二步处理 head, 第三步把时间转成秒, 第四部把番茄钟转换成秒. 
只想到前两步,看到番茄钟的, 会认为没有必要就删掉. | 尽可能把有效数据全部转换出来,供下一步程序员使用. 除非确定无用, 否则都要清洗. 
不知道先干哪一步,理解项目要完全依赖 README,自己拿到原始数据无从下手, 没有思路|看到问题瞬间有200多个方法, 但不知道哪个有效.用思维工具把思维速度降下来. 用纸和笔把目的写下来,由果到因往回回溯. 定义清楚需求. 
要转换成什么都不知道|知道所有的变成秒,知道最后输出的是什么样子

```
$ xargs -I{} cat{}
```
把每一行组合成一个命令,

小白|高手
---|---
没有常识, 不知道什么是良构. csv|没经历过, 就官方文档
不知道实际工作需求|明知卡住了,不问, 不知道搜什么.搜索时间太长了.
不知道什么时候提问,要在 slack 上么?|认真提问, 
80%陈述猜想, 而不是事实|事实, 环境/现象/问题/分析/方案, 描述过程中会产生方案. 尝试方案, 走通, 走不通,都记下来.一个方案15分钟走不下去, 就停止. 走不下去的方案是因为问题没有描述清楚. 不知道自己要干什么, 别人也无法回答. 

```$ cat raw.... | python stdin0handlog.py
```
- 把空格去掉了, 去掉所有格式.是怎么做到的呢?

重写stdin0handlog.py

- 每个.py 都会有默认的头和格式.直接复制下来
```
#!/usr/bin/python
# -*- encoding = utf-8 -*-
'''
专门处理非期待空格
'''
on__ = 'v17.8.1.0019'
__author__ = 'ZoomQuiet'
__license__ = 'MIT@2017-05'
```

- 
```
import sys

if __name__ = '__main__':
    if 1! = len(sys.argv)
        print ('''usage:
$ cat path/2/XXX.csv |python stdin0handlog.py
$ python stdin0handlog.py < path/2/XXX.csv
               ''')
           else:
               pass
```

测试
```
$ python stdin0handlog.py
```

调试结果:
- 没有错误.
- 非期待, 因为要有输入, 把上面的 if 1! 改成 if 2!
- 如果不是2 就会报错, 是2 , 会 print ()里的内容

把可以用的固定下来
```
$ git st
$ git add
$ git ci 
$ git log
```

```
$ python stdin0handlog.py ../raw/zoomquiet/0812-1303.data/
```

输出所有列表,不出错,但也没有任何处理. 

```
import sys
def main():
    for line in sys.stdin: 
        print (line)

if __name__ = '__main__':
    if 1! = len(sys.argv)
        print ('''usage:
$ cat path/2/XXX.csv |python stdin0handlog.py
$ python stdin0handlog.py < path/2/XXX.csv
               ''')
           else:
               main()
```

调试:
以上的作用是为了打印行的内容出来看一下, 出现了一个问题: 比原始的数据多空行. 因为把换行符也当做一行来打印了. 

解决方法: 

```
import sys
def main():
    for line in sys.stdin: 
        print (line[:-1])

if __name__ = '__main__':
    if 1! = len(sys.argv)
        print ('''usage:
$ cat path/2/XXX.csv |python stdin0handlog.py
$ python stdin0handlog.py < path/2/XXX.csv
               ''')
           else:
               main()
```

小白|高手
---|---
with open|line[:1]
?|目前只写了四行代码, 调试五次(在命令行下面运行), 知道现在干嘛.

- 处理表头
    - 先看表头的特点: date 只在表头出现

```
import sys
def main():
    for line in sys.stdin: 
        # print (line[:-1])
        l = line[:-1]
        if 'date' in l:
            print ('is head:\n\t{}'.format(l))
        else:
            pass

if __name__ = '__main__':
    if 1! = len(sys.argv)
        print ('''usage:
$ cat path/2/XXX.csv |python stdin0handlog.py
$ python stdin0handlog.py < path/2/XXX.csv
               ''')
           else:
               main()
```

- 不同时期的表头都可以识别出来
- 识别表头之后, 要把现象记录下来
- 现在用行处理. 行之外是文件处理, 每个文件都会有新的表头或新的什么
调试

```
import sys

isDATE = 0
def main():
    for line in sys.stdin: 
        # print (line[:-1])
        l = line[:-1]
        if 'date' in l:
            isDATE = 1
            # print ('is head:\n\t{}'.format(l))
        else:
            pass

if __name__ = '__main__':
    if 1! = len(sys.argv)
        print ('''usage:
$ cat path/2/XXX.csv |python stdin0handlog.py
$ python stdin0handlog.py < path/2/XXX.csv
               ''')
           else:
               main()
```


以上鉴别出表头.下面是对其他数据进行处理.

```
import sys

isDATE = 0
def main():
    for line in sys.stdin: 
        # print (line[:-1])
        l = line[:-1]
        if 'date' in l:
            isDATE = 1
            # print ('is head:\n\t{}'.format(l))
        else:
            isDATE = 0
            pass

        if isDATE:
            pass
        else:
            pass

if __name__ = '__main__':
    if 1! = len(sys.argv)
        print ('''usage:
$ cat path/2/XXX.csv |python stdin0handlog.py
$ python stdin0handlog.py < path/2/XXX.csv
               ''')
           else:
               main()
```

新加的两行的功能是: 可以对不同数据的门类进行处理, 区别出表头和不是表头. 不是表头的用其他方式处理.

先处理头. 

```
import sys

isDATE = 0
def main():
    for line in sys.stdin: 
        # print (line[:-1])
        l = line[:-1]
        if 'date' in l:
            isDATE = 1
            # print ('is head:\n\t{}'.format(l))
        else:
            isDATE = 0
            pass

        if isDATE:
            print (l)
        else:
            pass

if __name__ = '__main__':
    if 1! = len(sys.argv)
        print ('''usage:
$ cat path/2/XXX.csv |python stdin0handlog.py
$ python stdin0handlog.py < path/2/XXX.csv
               ''')
           else:
               main()
```


- print 一下, 确保代码变化,之前的功能有没有变化, 还是不是一样处理.
- 数据是有番茄钟的和没番茄钟的.
- 需要把时间账单和番茄钟连起来, 需要先区分

```
import sys

isDATE = 0
def main():
    for line in sys.stdin: 
        # print (line[:-1])
        l = line[:-1]
        if 'date' in l:
            isDATE = 1
            # print ('is head:\n\t{}'.format(l))
        else:
            isDATE = 0
            pass

        if isDATE:
            print (l.split())
        else:
            pass

if __name__ = '__main__':
    if 1! = len(sys.argv)
        print ('''usage:
$ cat path/2/XXX.csv |python stdin0handlog.py
$ python stdin0handlog.py < path/2/XXX.csv
               ''')
           else:
               main()
```

调试, 可以区分表头中的时间账单和番茄钟标识

- 连起来. 
```
import sys

isDATE = 0
def main():
    for line in sys.stdin: 
        # print (line[:-1])
        l = line[:-1]
        if 'date' in l:
            isDATE = 1
            # print ('is head:\n\t{}'.format(l))
        else:
            isDATE = 0
            pass

        if isDATE:
            print (','.join(l.split()))
        else:
            pass

if __name__ = '__main__':
    if 1! = len(sys.argv)
        print ('''usage:
$ cat path/2/XXX.csv |python stdin0handlog.py
$ python stdin0handlog.py < path/2/XXX.csv
               ''')
           else:
               main()
```

- join 是字符串的功能, 简单好懂

小白|高手
---|---
_s = l.split()|print (','.join(l.split()))
print('{},{}'.format(_s[0],_s[1]))|
两行|一行,简洁

_s 短杠变量是指临时变量






## question
- 怎么看默认库
- 如何形成 .csv 的良构
    + 用 Excel 打开. csv 是, 会跳出文本框, 问你隔断是引号还是什么.
-  if 1! = len(sys.argv) 是什么
- stdin 是什么?
    + 标准串流
- README 的不同版本有什么不同? 










