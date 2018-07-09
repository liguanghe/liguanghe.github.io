---
title: python | Pandas/bokeh 实现交互数据可视化报告
date: 2017/11/21 11:45:32
categories: 
- python


tags: 
- python
- Record
- time
- report
- TimeReport
- thinking
- skill
- atl4dama
- lghPR
- pandas
- bokeh
- matplotlib
- function
- needs

---


## 前言
- 这是一篇写给过去自己的教程, 如果你跟四个月前的我一样, 对编程几乎没认知, 也可以看懂. 
- 这也是一篇写给未来自己的备忘, 以后重现这个项目, 或做类似项目时, 不需重构思路, 也不需再次检索已经检索过的内容. 
- 时间报告见: [Time Report](https://liguanghe.github.io/2017/11/17/TimeReport/)
- 设计原理见: [Time Report's Report 时间报告的报告 | Li Guanghe's blog](https://liguanghe.github.io/2017/11/18/PythonTimeReport1/)

## 需求
- 图文展示一年中时间分配
- 类型频率及持续时间

## tools
### Python 

Python 做数据分析有完整的工具链条.

往深, 可以实现 Deep Learning 的项目(Scikitlearn/Tensorflow)

往浅, 也可以实现表格(二维矩阵)的处理

本次即使用较浅的部分,处理表格(虽然只有一张, 但很长)

### Pandas

数据科学最小工具链

python|numpy|pandas|Matplotlib(/bokeh)|Scikit-Learn(/tensorflow)
---|---|---|---|---
list|array|matrix|plot|
.     |.       |index,column,column,column|.|
l=[,,]|a=[[,,] |index,,,|
.     |   [,,]]|index,,,|
l|np.xxx|pd.dataframe(np.xxx)|plot.xxx.(pd.dataframe(np.xxx),x,x)
|[NumPy's Structured Arrays](https://jakevdp.github.io/PythonDataScienceHandbook/02.09-structured-data-numpy.html)|[Pandas df operates like a tructured array](https://jakevdp.github.io/PythonDataScienceHandbook/03.01-introducing-pandas-objects.html)|[Visualization with Matplotlib](https://jakevdp.github.io/PythonDataScienceHandbook/04.00-introduction-to-matplotlib.html)


### Bokeh

matplotlib 和 bokeh 选哪个?
    - [Jupyter 常见可视化框架的选择](https://mp.weixin.qq.com/s/FiuwSoaeNTfk9BYS-sswzw)
    - 我希望导出 html并且可交互, 故选择 bokeh.
    - 内部显示的话, matplotlib也很顺手, 有时会现用它展示, 再重新用 bokeh写一次. 

## 需求->代码实现

以需求为底, 逐步拆解到实现. 

### 处理 .csv 格式的表格 
- 导入, 并将其转化为 DataFrame(以下简称df, pandas 可以处理的数据形式. 如上表格显示, 与 list 相似,也是数据形式, 但可以被 pandas 处理.  [pandas.DataFrame.from_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.from_csv.html)
- 导出也可为 .csv, 因在本项目中不需要导出表格, 故省略.
- 举例
    - 原始数据格式如下:
``` 
du_start,du_end,act_type,wday,wn4y
1491088707.0,1491088708.0,05.Career,6,13
1491088708.0,1491088865.0,07.social,6,13
```
        - 转换后格式如下: 


```python
import pandas as pd

df = pd.read_csv('/Users/liguanghe/atl4dama/src/_rp4lgh/df_isocalendar4lgh.csv')
df.head(3) #显示头部, 还可以显示尾部 tail(), 显示描述 describ() ,括号里填写数字, 即可限定显示多少行
```

![](https://ws2.sinaimg.cn/large/006tKfTcgy1flpozwcu2fj31520ee75u.jpg)
### 计算各类型每周总用时

#### 目标: 上述列表转化成如下列表
- columns 是各类别
- index 是 week
- values 是 总用时 即每类别每周的总用时


```python
df3[44:45]
```

![](https://ws1.sinaimg.cn/large/006tKfTcgy1flpp09az0gj315g07g75o.jpg)
### 实现
- 增加列, 这列的内容可以根据前面各列的数据, 计算得出. 
    - [lambda](https://pandas.pydata.org/pandas-docs/stable/basics.html#general-dataframe-combine)
    - [pandas.DataFrame.apply](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.apply.html)
    - du_start 是开始的秒数, du_end 是结束的秒数. du_time 即结束减去开始, 即持续时间. 


```python
df['du_time'] = df.apply(lambda x: x.du_end-x.du_start, axis=1)
df.tail(1)
```


![](https://ws4.sinaimg.cn/large/006tKfTcgy1flpp0uiehoj314i08emy3.jpg)
- df中 某一列, 去掉重复的元素后, 有哪些, 可用来分类和计数.
    - 计算有多少类行为, 这些行为都在 act_type 这一列中. 
    - 计算有多少周 都在 wn4y 这一列中.


```python
import numpy as np
UniqueAct = df.act_type.unique()
```

- 按照某一列中特有的某一元素 提取行, 
    - eg:要从 df 中提取出 在 act_type 中都是 sleep 的行 重组一个矩阵. c = df[df['act_type'].isin(['sleep'])
    - 在矩阵 c中提取出 在wn4y 中都是 14 的行 重组一个矩阵 c[c['wn4y'].isin(['14'] 即第14周的所有 sleep 的数据.
- 某一列求和 np.sum(df).['columnA'], eg: np.sum((c[c['wn4y'].isin([week])])['du_time'] 及某一行为某一周的总秒数, /60/60, 可得小时.
- 使用 for in 循环, 即可将所有行为不同周的总小时数计算出来. 添加到 list l. 同时列出 list a(行为) , list w(week). 将三个列表连在一起, 形成新的矩阵. d4 = {'act':a, 'week':w,'sum':l} pd.DataFrame(d4) 
- 矩阵里的元素只取小数点后一位 .round(1)


```python
l = []
a = []
w = []
for i in UniqueAct:
    c = df[df['act_type'].isin([i])]
    Uniqueweeks = df.wn4y.unique()
    for week in Uniqueweeks:
        a.append(i)
        w.append(week)
        l.append(np.sum((c[c['wn4y'].isin([week])])['du_time'])/60/60)
        d4 = {'act':a,
        'week':w,
        'sum':l}
to= (pd.DataFrame(d4).round(1)).set_index('act')
```

- 将某一列的内容变成 columns 另外一列的内容变成 index, 第三列的内容作为 values的方法. 
    - 以' act'作为 index, pandas 针对 index 提供检索的功能 .loc[]
    - eg: ((pd.DataFrame(d4).round(1)).set_index('act')).loc['sleep] 即在所有 index 中检出行为 在这个基础上, 再使用 .set_index('week'), 将周作为 index
    - 事先建立一个纵轴为52周的矩阵, 在这个矩阵后面添加过滤过的矩阵. 


```python
ls = list(range(52))
df3=pd.DataFrame(ls)
for act in UniqueAct:
    df3[act]= (to.loc[act]).set_index('week')
df3.tail(1)
```

![](https://ws4.sinaimg.cn/large/006tKfTcgy1flpp0uiehoj314i08emy3.jpg)
### 分类制表
有了按照类型分周的总用时的矩阵 df3,可根据自己的希望的分类选择类型, 组建新表. 下面是特有的类型 


```python
df3.columns
```


    Index([                              0,                     '05.Career',
                               '07.social',          '07.social:networking',
                      '09.HealthFun:sport',            '12.sleep:noonsleep',
                    '04.StudyGrow:reading',                    '11.traffic',
                     '04.StudyGrow:writer', '04.StudyGrow:ComputerThinking',
                        '09.HealthFun:fun',   '08.familylife:washingbeauty',
                                '12.sleep',        '08.familylife:families',
                    '08.familylife:dinner',   '08.familylife:generalAffair',
                            '04.StudyGrow',              '04.StudyGrow:law',
                   '08.familylife:finance',                  '09.HealthFun',
                    '09.HealthFun:fantasy'],
          dtype='object')



- select data with loc [Indexing and Selecting Data](https://pandas.pydata.org/pandas-docs/stable/indexing.html)
- 举例, 睡眠包括午睡和晚上的睡眠


```python
sl =df3.loc[:,['12.sleep','12.sleep:noonsleep']]# :指所有的index,即所有的行, ['','']是要选择的 column, 即列
sl[44:45]
```

![](https://ws2.sinaimg.cn/large/006tKfTcgy1flpp19ck6uj314c07i3yv.jpg)

下面分别为 live, healthfun, input,output 的分类表格


```python
fa = df3.loc[:,['08.familylife:washingbeauty','08.familylife:generalAffair','08.familylife:dinner','08.familylife:families','08.familylife:finance']]
hf = df3.loc[:,['09.HealthFun:sport', '09.HealthFun:fun','09.HealthFun', '09.HealthFun:fantasy']]
ip = df3.loc[:,['04.StudyGrow:reading','07.social', '07.social:networking']]
op = df3.loc[:,['04.StudyGrow:ComputerThinking','04.StudyGrow:writer','05.Career', '04.StudyGrow:law',
       '04.StudyGrow']]
```

- 计算以上各类的总用时, 添加到 df3后面
- 将各大类的总用时再列一张表, 就是5大类总用时的表格


```python
df3['Sleep'] = df3.apply(lambda x: x['12.sleep:noonsleep']+x['12.sleep'], axis=1)
df3['Live'] = df3.apply(lambda x: x['08.familylife:washingbeauty']+x['08.familylife:families']+x['08.familylife:dinner']+x['08.familylife:generalAffair']+x['08.familylife:finance'], axis=1)
df3['HealthFun'] = df3.apply(lambda x: x['09.HealthFun:sport']+x['09.HealthFun']+x['09.HealthFun:fantasy']+x['09.HealthFun:fun'], axis=1)
df3['Input'] = df3.apply(lambda x: x['04.StudyGrow:reading']+x['07.social']+x['07.social:networking'], axis=1)
df3['Output'] = df3.apply(lambda x: x['04.StudyGrow:ComputerThinking']+x['04.StudyGrow:writer']+x['05.Career']+x['04.StudyGrow:law']+x[
    '04.StudyGrow'], axis=1)

ti =df3.loc[:,['Output','Input','Sleep','Live','HealthFun']]
ti[44:45]
```

![](https://ws2.sinaimg.cn/large/006tKfTcgy1flpp1hgyo9j314m070mxq.jpg)
### 制图
#### 经典的Matplotlib
开篇分析了可视化框架的选择, 虽然本报告使用 bokeh, 但因 [Matplotlib](https://matplotlib.org/) 是经典的 jupyter notebook 可视化框架, 这里快速展示一下, 其他可视化框架的原理都跟这差不多.


```python
import matplotlib.pyplot as plt

ti.plot.bar(stacked=True); #ti 是矩阵名称, .plot是制图, .bar 是制作柱状图 (stacked=True) 是说折叠的柱状图
plt.show() #展示图片

```


![](https://ws3.sinaimg.cn/large/006tKfTcgy1flpcgep189j30ai073aa1.jpg)


#### 本报告使用 bokeh
主要是其可导出为 .html, 这样可直接发布到公网, 无需再另行排版或上传图片取得链接等等. 

且 bokeh 与 jupyter notebook 对接良好, 图片可直接在notebook 里预览.  


```python
#from bokeh.io import show, output_file #生成的图片在 html网页显示
from bokeh.io import output_notebook, show #生成的图片在 jupyter notebook 中的 .ipynb 中显示

output_notebook()
#output_file('/Users/liguanghe/liguanghe.github.io/source/_posts/TimeReport.html', title = 'Time Report')
```


bokeh 也可以直接处理 矩阵, 比 matplotlib 多一步


```python
from bokeh.models import ColumnDataSource
# 下文中 source3 = ColumnDataSource(ti) source1 = ColumnDataSource(op)... 等
```

#### bokeh 生成图片
```
pt = figure(title='5 types')
pt.vbar_stack(ti.columns, x = ti.index,width = 0.9,color=Spectral5,source = source3, 
              legend=[value(x) for x in ti.columns])
pt.legend.location = "top_left"
```
- 画一个空白的图 p5= figure(height=HEIGHT) ,同时可以设置这个图的长度和高度, 在括号里赋值 height 和 width...
- 这个图是折叠柱状图 .vbar_stack
- 要折叠的内容的 矩阵 ti 中 columns 里的各类. ti.columns( 几个类型)
- 横轴(x)是 矩阵 ti 中的 index (周)
- 每个bar 的宽度是0.9 width = 0.9
- bar 里的不同类要有不同颜色, 用 color 来赋值
    - 这里需要特别注意, 有几类, 就用几个颜色. 
    -  ```from bokeh.palettes import GnBu5,Greens3,Spectral5,Oranges5,Reds4``` 
    - 在[bokeh.palettes](https://bokeh.pydata.org/en/latest/docs/reference/palettes.html)可以选取颜色组合 
    - 这些组合最少三个色, 你只有两个也没关系, 可以自己设定两个颜色, 见下面代码中 ps 那张图.
- source 就是用什么来做图.
- legend 是给每一截bar打标签, 即在图中显示每截不同颜色的 bar 是什么. 这里也要注意, 长度和内容应该与图中实际情况一样. ```legend=[value(x) for x in ti.columns```
- 以上内容在[Quickstart — Bokeh](https://bokeh.pydata.org/en/latest/docs/user_guide/quickstart.html)有介绍.


```python
from bokeh.plotting import figure
from bokeh.palettes import GnBu5,Greens3,Spectral5,Oranges5,Reds4
from bokeh.core.properties import value

#WIDTH = 500
HEIGHT = 300

source3 = ColumnDataSource(ti)
pt = figure(title='5 types')
pt.vbar_stack(ti.columns, x = ti.index,width = 0.9,color=Spectral5,source = source3, 
              legend=[value(x) for x in ti.columns])
pt.legend.location = "top_left"

po = figure(height=HEIGHT)
source1 = ColumnDataSource(op)
po.vbar_stack(op.columns, x = op.index,width = 0.9,color=GnBu5,source = source1,
legend=[value(x) for x in op.columns])
po.legend.location = "top_left"

source2 = ColumnDataSource(ip)
pi = figure(height=HEIGHT,title='Input')
pi.vbar_stack(ip.columns, x = ip.index,width = 0.9,color=Greens3,source = source2,
             legend=[value(x) for x in ip.columns])
pi.legend.location = "top_left"

colors = ['#ffffcc','#FDE724' ]

ps = figure(height=HEIGHT)
source4 = ColumnDataSource(sl)
ps = figure(height=HEIGHT,title='sleep')
ps.vbar_stack(sl.columns, x = sl.index,width = 0.9,color=colors,source = source4,
             legend=[value(x) for x in sl.columns])
ps.legend.location = "top_left"

source5= ColumnDataSource(fa)
pf = figure(height=HEIGHT,title='live')
pf.vbar_stack(fa.columns, x = fa.index,width = 0.9,color=Oranges5,source = source5,
             legend=[value(x) for x in fa.columns])
pf.legend.location = "top_left"


source6= ColumnDataSource(hf)
ph = figure(height=HEIGHT,title='healthfun')
ph.vbar_stack(hf.columns, x = hf.index,width = 0.9,color=Reds4,source = source6,
             legend=[value(x) for x in hf.columns])
ph.legend.location = "top_left"

```



![](https://ws3.sinaimg.cn/large/006tKfTcgy1flp95kgmcbj30z60h0di7.jpg)
#### bokeh HTML 排版及插入视窗
- 前面说 bokeh 可输出漂亮的可交互的 html, 将多张图片按照你希望的格式排列在网页上. 不仅是图片, 也可以插入文字/按钮等等
- 先说插入文字/按钮等视窗
    - [Div](https://bokeh.pydata.org/en/latest/docs/user_guide/interaction/widgets.html#userguide-interaction-widgets)是可以识别 html 排版语言的小窗口, 把你想要显示的文字填在 ```Div(text=''' ''')``` 中. 可赋值长度和宽度


```python
from bokeh.layouts import widgetbox
from bokeh.models.widgets import Div

t0 = Div(text="""
    <h1 align="center">Time Report</h1>
    <p>Each Nature week has 168 hours(24h*7d=168h).</p>
    <p>Hours in this form are a little more or less. 
    One reason is some time may not be recorded,the other reason 
    is an event time may cross two weeks.</p>
    <p>Each bar in the plot nearly touchs 168(y), 
    this shows I record all time-spent every week.  </p>
    <h2> 5 big types</h2>
    <p>Label daily action to 5 big types, like the plot shows. </p>
    """,width=WIDTH, height=200)
```

- 除了文字, 还可以填写 function, 给 variable 赋值, 即可显示对应的输出结果. 
- frequency 是我编写的 function, 会在下文详解. 


```python
from lgh7SumFrequency import frequency
t1 = Div(text='''<h2>Output ↑</h2>'''
    +frequency(cvsf,'04.StudyGrow:ComputerThinking')+'''<p>\n</p>'''
    +frequency(cvsf,'04.StudyGrow:writer')+'''<p>\n04.StudyGrow shows  curious.</p>''',width=WIDTH, height=100)
t2 = Div(text='''<h2>Input ↑</h2>
    <p>Reading without output is input.</p>
    <p>Meaningly social is in this part. Others belong to live:familes.\n<p>'''
    +frequency(cvsf,'04.StudyGrow:reading'),width=WIDTH, height=100)
t3 = Div(text='''<h2>Sleep ↓</h2>
    <p>sleep < 59h</p>''',width=WIDTH, height=100)
t4 = Div(text='''<h2>Live</h2><p>08.familylife:familes includes other social.</p>'''
    +frequency(cvsf,'08.familylife:washingbeauty'),width=WIDTH, height=100)
t5 = Div(text='''<h2>HealthFun</h2>'''+frequency(cvsf,'09.HealthFun:sport')+'''\n<p>09.Healthfun shows curious.</p>
    <p>09.Healthfun:fun should be down.</p>
    ''',width=WIDTH, height=100,)
```

- 排版, 可以按照坐标的方式, 即 grid, 也可以按照 row 和 column 排列, 这里选择 grid , [widgetbox(t0),none] 则会将他们排在一行, 其他的一次排下去. [Laying out Plots and Widgets](https://bokeh.pydata.org/en/latest/docs/user_guide/layout.html#)


```python
from bokeh.layouts import gridplot

grid = gridplot([[widgetbox(t0)],[pt],[t1], [po],[t2],[pi],[t3],[ps],[t4],[pf],[t5],[ph]])
    save(grid)

show(grid)
```


即可生成 HTML, 输出成果见[time report](https://liguanghe.github.io/2017/11/17/TimeReport/)

### 计算频率的 function

#### 制表
- 一个行动类型一张表
- index: 周
- column: 7天
- value: 有行动是0, 没有行动是1


```python
import pandas as pd
import numpy as np
#import matplotlib.pyplot as plt

u = (((df.loc[:,['act_type','wday','wn4y']]).set_index('act_type')).loc['09.HealthFun:sport']).set_index('wn4y')
yo =[]
we=[]
da = []
for week in u.index.unique():
    for i in range(7):
        if i in (u.loc[week].values):
            y = 0
        else:
            y = 1
        yo.append(y)
        we.append(week)
        da.append(i)
        d = {'you':yo,
            'week':we,
            'day':da}  
y= pd.DataFrame(d).set_index('week')
ls = list(range(7))

yu = pd.DataFrame(ls)             
for we in u.index.unique():
    yu[we] = (y.loc[we]).set_index('day')
(yu.T).loc[30:33]

```

![](https://ws4.sinaimg.cn/large/006tKfTcgy1flpp1oubpfj313u0f8wfi.jpg)
#### 根据表格内容输出话语
- 如果 每行的总和是0, 输出: 每天都运动
- 如果 每行总和不是0, 输出: 总和 天没有运动

```python
for we in u.index.unique():
            yu[we] = (y.loc[we]).set_index('day')
            ''' sum = 0 / sum = n, n is not sport last week'''
        if (yu.sum(axis = 0)<=0)[-1:].values == True:
            return stype + ' everyday.'
        else:
            return str(yu.sum(axis = 0).iloc[-1]) + " days didn't "+ stype +' last week.'
```

- 转成 function,处理不同的行为
    - 如果输入的不是行为列表中的元素, 则输出, 请输入你行为列表中的行为
    - 调用这个函式如上文小窗口 t1,t3,t4 中的 ```frequency(cvsf,'04.StudyGrow:ComputerThinking')```


```python
import sys
import pandas as pd
import numpy as np



def frequency(cvsf,stype):
    '''read .csv to df'''
    df = pd.read_csv(cvsf)
    df['du_time'] = df.apply(lambda x: x.du_end-x.du_start, axis=1)
    '''sport index=week, column = day'''
    
    if stype in str(df['act_type']):
        u = (((df.loc[:,['act_type','wday','wn4y']]).set_index('act_type')).loc[stype]).set_index('wn4y')

        '''index = 0-6, column = week, value = 0/1'''
        Uniqueday = u.wday.unique()    
        UniqueWeeks = df.wn4y.unique()

        yo =[]
        we =[]
        da =[]
        for week in u.index.unique():
            for i in range(7):
                if i in (u.loc[week].values):
                    y = 0
                else:
                    y = 1
                yo.append(y)
                we.append(week)
                da.append(i)
                d = {'you':yo,
                    'week':we,
                    'day':da}  
        y= pd.DataFrame(d).set_index('week')
        ls = list(range(7))

        yu = pd.DataFrame(ls)             
        for we in u.index.unique():
            yu[we] = (y.loc[we]).set_index('day')
            ''' sum = 0 / sum = n, n is not sport last week'''
        if (yu.sum(axis = 0)<=0)[-1:].values == True:
            return stype + ' everyday.'
        else:
            return stype+' ' +str(yu.sum(axis = 0).iloc[-1]) + " days off last week."
        
    else:
        print ('please input one act_type in your data')
    

if __name__ == '__main__':
    print(__version__)
    _csv = sys.argv[1]
    _ty = sys.argv[2]
    frequency(_csv,_ty)
```

## 心

- 照着 [Learn Python the Hard Way](https://learnpythonthehardway.org/book/) 抄了一个月的代码. 
- 看 pandas 来写代码了. 大妈提供了 [Python Data Science Handbook | Python Data Science Handbook](https://jakevdp.github.io/PythonDataScienceHandbook/index.html) 这本数据科学工具书. 我并没有全看完, 只是把每个工具都有的10分钟快速掌握看完, 知道它主要实现什么功能, 然后就去完成自己的需求. 千万不要抱着都看完才去学, 这样无法开动, 带着项目搜索怎么做, 并不断的实验, 是最快的. 
- 经常会遇到报错, 见这篇: [When Your Computer Answer 'Error' 写代码遇到报错怎么办? | Li Guanghe's blog](https://liguanghe.github.io/2017/11/18/pythonErrorSolution/)
- 这中间遇到的最大的坑, 是 type. 这篇教程一定要仔细看. [Understanding Data Types in Python | Python Data Science Handbook](https://jakevdp.github.io/PythonDataScienceHandbook/02.01-understanding-data-types.html) 
- 整个尝试过程在 Ipython 中完成, 然后导出成为脚本. 设置成 function 供调用. 
- 尝试过程的 Ipython 文档本身导出到 .md 格式, 就是本教程. 
