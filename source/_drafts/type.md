## 数据类型
## 行动
- 线性记录大妈给了哪些反馈
    + [x] slack(如下)
    + [x] issue(如下)
    + [x] ipynb(如下)
    + src
    + ... 
- 怼明白我出这个血案的根本原因.  
    - int and types
    
```
TypeError: cannot do slice indexing on <class 'pandas.core.indexes.numeric.Int64Index(整数)'> with these indexers [otn] of <class 'str'>
类型错误, 不能分开索引, 用 类' ..... 数字,整数', 系列功能是类, 通过 这些 索引[otn],它是 字符串类.
```
大妈说这里的意思其实是, otn这个字符串类需要是 int64index (整数) 

[4. Built-in Types — Python 3.6.2 documentation](https://docs.python.org/3/library/stdtypes.html#typesnumeric)

```
4. Built-in Types
The following sections describe the standard types that are built into the interpreter(解释器) .

? The principal built-in types are numerics(数字), sequences(序列), mappings, classes(类), instances and exceptions.

Some collection classes are mutable(易变的). The methods that add, subtract(减), or rearrange(重新布置) their members in place, and don’t return a specific item, never return the collection instance itself but None.

Some operations are supported by several object types; in particular, practically all objects can be compared, tested for truth value, and converted to a string (with the repr() function or the slightly different str() function). The latter function is implicitly used when an object is written by the print() function.

一些操作被几种对象类型支持, 所有对象可以被比较, 测试真值, 修改成一个字符串(使用 repr() function 或 各种轻微不同 str() function). 较后面的function 被绝对使用,当一个对象被 print()function 写的时候. 
```
大概了解 types
```
- function 处理数据. 数据有不同是的类型, types, 有些 fhunciton 处理的数据类型是有限制的. 在特定的地方只能填入特定的数据类型. 
```

```
1. Truth Value Testing
2. 
```




    - str is not callable
    - 动态语言?
    - 调试?
- 跑一遍大妈的新代码
    - 重新更新 readme
    - 重新把最小信息链放进去. 
        - 写 wiki 强调最小信息链的重要性
    + 对比高手和小白的区别
        * 代码行数
        * 问题解决
        * 调试思维?

## 大妈的帮助
### slack 上的快速解释

pandas 说了…不能是字串…
是说内容啊………
type(otn)
就知了……
英文理解反了…
int(otn) 就过了
TypeError: ‘str’ object is not callable

x= time[0:int(otn)]
TypeError: ‘str’ object is not callable
dir type id help 等一系列内建自省函式都要熟练啊………

所以…你完全可以先
z=2
df[0:z]
测试一下…………
分解问题

你得定义你的问题…并检证…然后深入…直到解决
很好…进了一步…然后…两者的差异在哪?

所以…你原先的问题不是引发现象的问题…

所以…又一个血案故事…
原因和乱合 master 一样…
从未尝试改进第一偏见…



我原先的问题, 进一步的问题是: df[0:x], 这个 x 到底应该是什么
我觉得这是我底层知识的原因.
再次提醒… type
 
就是字面的 整数
问题是你们死也不给整数


只是之前这里显示的是4, type后的类型居然是str…
终于撞上动态语言的专有坑了………

### issue 的留言
看错误报告…清清楚楚…问题不是变量形式…是内容
![2017-09-10 15 31 40](https://user-images.githubusercontent.com/22494/30247056-3aa24d22-95d0-11e7-971a-30577182d90b.png)

~ [zq2analyse.ipynb](https://github.com/DebugUself/du4proto/blob/atl4dama/ipynb/zq2analyse.ipynb)

所以,是从根儿上怀疑错方向了, 又没有立即设计实验检验自己的想法,
然后,习惯性的期望用相同的行为,获得不同的结果, 
必然的卡死没商量了...

6h[QUESTION][atl4dama]pandas 想选取的行数是个变量, 如何实现? 中提及的问题和标题是没有关系的...
    - pd 的提示是非常精确和友好的
    - 但是, 我们自己的先见之明, 导致了一系列误解
    - 进一步的, 又没有在第一时间用 py 的自省能力完成检验
    - 导致进行了错误的 google , 自然越来越乱, 无法寸进了...
