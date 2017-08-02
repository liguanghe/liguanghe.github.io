

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

- 处理数据
(所有的处理方式是一样的, 无论做什么, 都随时 print , 确定知道自己在做什么)

isDATE 是全局变量, 是状态值, 随着每行的内容不同,如果某行有date 就是0, 没有是1, 为0的时候处理上面的, 为1 的时候处理下面的. 

现在处理下面的. 
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
        # print(isDATE)

        if isDATE:
            print (','.join(l.split()))
        else:
            # print (l)
            print (','.join(l.split()))

if __name__ = '__main__':
    if 1! = len(sys.argv)
        print ('''usage:
$ cat path/2/XXX.csv |python stdin0handlog.py
$ python stdin0handlog.py < path/2/XXX.csv
               ''')
           else:
               main()
```

把单纯的数据连起来了. 有不对劲的地方, 要调. 
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
        # print(isDATE)

        if isDATE:
            print (','.join(l.split()))
        else:
            # print (l)
            print (','.join(l.split()))
            print (l.split())


if __name__ = '__main__':
    if 1! = len(sys.argv)
        print ('''usage:
$ cat path/2/XXX.csv |python stdin0handlog.py
$ python stdin0handlog.py < path/2/XXX.csv
               ''')
           else:
               main()
```

- 用 print(l.split())看split之后是什么 
- 发现的问题是, 前面的还是一整条, 后面的会变成用用都好和分号把每个都分出来. 
- 后面的需要删掉逗号.

如何去逗号?

小白|高手
---|---
多了逗号|逗号位置错了
strit?|
空格问题|

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
        # print(isDATE)

        if isDATE:
            print (','.join(l.split()))
        else:
            # print (l)
            print (','.join(l.split()))
            print (l.split(','))


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
多了逗号|逗号位置错了
strit?|
空格问题|
?|先试着用逗号分, 调试,会出现前面的数据多了逗号, 后面的数据没有逗号, 但是多了空格. 
?|有两种思路处理, 都可以. 一种是去多余逗号, 一种是去多余空格. 

(进行下一步之前, 先把print 调试的部分, 前面加#)

第一种, 去多余逗号. 
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
        # print(isDATE)

        if isDATE:
            print (','.join(l.split()))
        else:
            #print (l)
            print (','.join(l.split()))
            print (l.split())
            _s = l.split()
            _exp = []
            for i in _s:
                print (i)
                

            #print (l.split(','))


if __name__ = '__main__':
    if 1! = len(sys.argv)
        print ('''usage:
$ cat path/2/XXX.csv |python stdin0handlog.py
$ python stdin0handlog.py < path/2/XXX.csv
               ''')
           else:
               main()
```


上面添加的这段, 是把按逗号分隔的字符串变成不同行. 

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
        # print(isDATE)

        if isDATE:
            print (','.join(l.split()))
        else:
            #print (l)
            print (','.join(l.split()))
            print (l.split())
            _s = l.split()
            _exp = []
            for i in _s:
                print (i)
                if len(i) = 2:
                    print (i)
                else:
                    pass

            #print (l.split(','))


if __name__ = '__main__':
    if 1! = len(sys.argv)
        print ('''usage:
$ cat path/2/XXX.csv |python stdin0handlog.py
$ python stdin0handlog.py < path/2/XXX.csv
               ''')
           else:
               main()
```

后面数据打了两行
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
        # print(isDATE)

        if isDATE:
            print (','.join(l.split()))
        else:
            #print (l)
            print (','.join(l.split()))
            print (l.split())
            _s = l.split()
            _exp = []
            for i in _s:
                print (i)
                if len(i) = 2:
                    print (i[0])
                    _exp.append(i[0])
                else:
                    _exp.append(i)#pass
            #print (l.split(','))
            print (','.join(_exp))


if __name__ = '__main__':
    if 1! = len(sys.argv)
        print ('''usage:
$ cat path/2/XXX.csv |python stdin0handlog.py
$ python stdin0handlog.py < path/2/XXX.csv
               ''')
           else:
               main()
```


这样可以去掉逗号, 但是很复杂, 可以集合到一行当中. 列表推导式.

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
        # print(isDATE)

        if isDATE:
            print (','.join(l.split()))
        else:
            #print (l)
            #print (','.join(l.split()))
            #print (l.split())
            _s = l.split()
            _exp = []
            for i in _s:
                #print (i)
                if len(i) = 2:
                    #print (i[0])
                    _exp.append(i[0])
                else:
                    _exp.append(i)#pass
            #print (l.split(','))
            print (','.join(_exp))


if __name__ = '__main__':
    if 1! = len(sys.argv)
        print ('''usage:
$ cat path/2/XXX.csv |python stdin0handlog.py
$ python stdin0handlog.py < path/2/XXX.csv
               ''')
           else:
               main()
```

调试结果: 同一行前后数据都由逗号隔开. 
接下来确保兼容性:试试打开别的文件.
把所有的文件都一起处理. 
```
$ ls ../raw/zoomquiet/0812-1303data/zq-tilog-* | | python stdin0handlog.py
```

-* 是指全部文件. 
处理后的文档又有问题: 多出来的空行, 多出来的表头(表头另行处理).


```
import sys

isDATE = 0
def main():
    for line in sys.stdin: 
        # print (line[:-1])
        l = line[:-1]
        # print (len(l))
        if len(l) < 2:
            pass
        else:
            if 'date' in l:
                isDATE = 1
                # print ('is head:\n\t{}'.format(l))
            else:
                isDATE = 0
            # print(isDATE)

            if isDATE:
                print (','.join(l.split()))
            else:
                #print (l)
                #print (','.join(l.split()))
                #print (l.split())
                _s = l.split()
                _exp = []
                for i in _s:
                    #print (i)
                    if len(i) = 2:
                        #print (i[0])
                        _exp.append(i[0])
                    else:
                        _exp.append(i)#pass
                #print (l.split(','))
                print (','.join(_exp))


if __name__ = '__main__':
    if 1! = len(sys.argv)
        print ('''usage:
$ cat path/2/XXX.csv |python stdin0handlog.py
$ python stdin0handlog.py < path/2/XXX.csv
               ''')
           else:
               main()
```

 print (len(l)) 把每行的长度打出来, 有额外空行的, 长度是0. 把长度小于2的都 pass, 其他的继续处理. 
 调试.

 - 去掉多余表头: python stdin1head.py
 - 转换年月日到秒: python stdin2year2sec.py
     + 两步, 第一步是把对象变成 datetime 对象, 第二步是把 datetime对象变成 time对象. 
     + 
```
#!/usr/bin/python
# -*- encoding = utf-8 -*-
'''
transform year as src
'''
on__ = 'v17.8.1.0019'
__author__ = 'ZoomQuiet'
__license__ = 'MIT@2017-05'

import sys
#import pandas as pd
import time
import datetime

def read4stdin():
    #isDATA = 0
    for line in sys.stdin():
        dl = line[:1]split(',')
        # print(dl[0])
        _day = datetime.datetime.strptime(dl[0], '%y%m%d')
        _ts = time.mktime(_day.timetuple())
        _exp = "{},{}".format(int(_ts),",".join(dl[1:]))
        print (_exp)
    return None

if __name__ = "__main__":
    if 1 != len(sys.argv):
        print ('''usage:
        $ cat path/2/XXX.csv | python stdin2year2sec.py
        or
        $ python stdin2year2sec.py < path/2/XXX.csv
               ''')
    else:
        read4stdin() 

```

- 目的: 人工可读130312, 变成机器可读的秒数1364227220
- strptime 是把文本字符串, 人工告诉字符串是由什么组成的, 转换成内部的时间对象. 
- 被大规模滥用

小白|高手
---|---
先识别年, 月, 正则表达式等等|strptime


整体方法如上, 只有注释不可以这么写, 应该是三节: 目的是什么,在调什么,用时, 要完成什么功能/探索
可以在git log 里很快的知道你做了什么事情. 

每一个 print 都会# , 都在反复验证当时是怎么想的. 
代码写出来是读的形式, 但读的形式和运行的次序是不同的.骰子,给出所有的通道,但是每行从哪个通道走, 你要清楚. 

怎么读代码: print都留下来了,就是给你读. 不懂哪一行, 就print你不懂的地方. 
怎么运行, 我有三种运行方法, 

数据有两类, 先调一类, 用经典文档处理, 再换一类再给, 都好了, 再把目标全部给.

代码是完成态,  

看代码,严格搞清楚写代码是为了解决什么问题. 目标是把问题搞定.目标有哪些子问题,如果观察不出来, 就看不懂代码. 

代码每两三行解决一个问题. 

除了纯化, 制造数据麻烦之外, 还可以把代码注释掉, 看不懂, 就注释掉不让他运行, 看差别, 就知道代码是在做什么. 
查 bug, 冷冻调试法和二分法, 都是同样的. 找 bug 和制造可控 bug 以理解改行代码的意义. 
定位到这一行是做什么. 缩小到可以理解代码. 

if else, 是代码里的分支, 每个分支是做什么的, 你要清楚. 根据理解一个分支, 其他的不处理. 先处理 if, 再处理 else, 看哪个分支随你. 







## question
- 怎么看默认库
- 如何形成 .csv 的良构
    + 用 Excel 打开. csv 是, 会跳出文本框, 问你隔断是引号还是什么.
-  if 1! = len(sys.argv) 是什么
- stdin 是什么?
    + 标准串流
- README 的不同版本有什么不同? 
- 诗颖说的去逗号的 strit怎么拼写? 
- 以下有什么区别? 
```print (i[:-1])```
```print (i[-1])```
```print (i[0])```
- strptime 是什么?








