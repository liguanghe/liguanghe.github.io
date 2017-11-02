---
title: Basic Element and Grammer of Coding
date: 2017/9/11 08:25:32
categories: 
- python
tags:
- python
- code
- English
- study
- tutorial
- basic
- words and sentence
---

## 前言

you must begin at this page: [3. An Informal Introduction to Python — Python 3.5.4rc1 documentation](https://docs.python.org/3.5/tutorial/introduction.html)

python is a language, like nature language, built by basic elements. English is built by letters, Python is built by letters, numbers and symbols.

type|letter|number|symbol|
---|---|---|---
Function|replace/refer to|calculation/index|处理
e.g.|variy/def|+/[]|1/1/[-1]

mix them to be a word, then to be sentence, and then a paragraph. a single line of code can translate to a pargraph of natule language. 

## 数字和符号放一起, 是计算
e.g. 


```python
1 + 1 #addition
```




    2




```python
2 ** 7 #square
```




    128



## 字母词 = 数字 是变量
e.g.1


```python
girl = 10
boy = 20
girl + boy
```




    30

e.g.2
变量赋值任何数字后, 之后继续使用这个变量. 
```
line_n = 0 
limit > 10000
lm = Counter() 
line_n += 1 
```

## 引号里面有文字, 整个是字符串
e.g.


```python
l = 'hello world'
print (s)
```

    hello world



```python
n = '1'
print (n)
```

    1



```python
s = '*'
print (s)
```

    *


string is like word, same as number , it can be deal with.

## '字母词 后面跟的[ ]表示位置索引 : -  ' 'number' 
e.g.


```python
w = 'python'
w[0] #the first letter of 'python'
```




    'p'




```python
w[:2]#the first letter to the second letters of 'python'
```




    'py'




```python
w[-1]# the last letter of 'python'
```




    'n'




```python
w[:-2]# the first letter to the last two letters of 'python'
```




    'pyth'

## '字母词做容器( list/counter/dict)时 后面跟的[ ]表示其中的元素( elements)
```
lm = Counter()
lm[key]
```

## The built-in function len() returns the length of a string:
e.g.


```python
s = 'ninwoebnihgiyi'
len(s)
```




    14



## s = [  ,  ] is list
e.g.


```python
s = [1,2,3,4]
s
```




    [1, 2, 3, 4]




```python
s[0]
```




    1




```python
s[2]
```




    3




```python
s[2:5]
```




    [3, 4]



## begin programing


```python
a, b =0, 1
while b < 1000:
    print (b, end = ',')
    a, b = b, a+b
```

    1,1,2,3,5,8,13,21,34,55,89,144,233,377,610,987,

## print ()
- writes the value of the argument(s) it is given.
- multiple arguments, floating point quantities, strings


```python
i = 256*256
print('the value of i is', i)
```

    the value of i is 65536


## xx.xx() is module.function for (content)

### 数据科学最小工具链

python|numpy|pandas|Matplotlib|machine learning?
---|---|---|---|---
list|array|matrix|plot|
.     |.       |index,column,column,column|.|
l=[,,]|a=[[,,] |index,,,|
.     |   [,,]]|index,,,|
l|np.xxx|pd.dataframe(np.xxx)|plot.xxx.(pd.dataframe(np.xxx),x,x)
|[NumPy's Structured Arrays](https://jakevdp.github.io/PythonDataScienceHandbook/02.09-structured-data-numpy.html)|[Pandas df operates like a tructured array](https://jakevdp.github.io/PythonDataScienceHandbook/03.01-introducing-pandas-objects.html)|[Visualization with Matplotlib](https://jakevdp.github.io/PythonDataScienceHandbook/04.00-introduction-to-matplotlib.html)




