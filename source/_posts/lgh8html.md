---
title: Part Achievement in Python Project named atl4dama 时间账单项目阶段成果 
date: 2017/9/25 08:25:32
categories: 
- python
tags:
- python
- code
- English
- study
- achievement
- atl4dama
- visual
- pandas
- bokeh
- line
- plot
- data
- time recording
- record
---

In this month, I'm part of a Python project named atl4dama. Here is the achievements.

## Project Background
- Object data
    + ZoomQuiet 5 years time recording data
    + Jianfei 5 years time recording data
    + guanghe 6 months time recording data
- Goal
    + visual the affection
- Step
    + data cleaning -> data analysis -> data visual
    + begin from a MVP to test tools and thinking, have a global perspective.
    + imporves it.
    + compares the final achievement and first MVP, to show the project meaning.
## Part achievements
data cleaning -> data analysis -> data visually. My job is data visually. I begin here, so show this part first. Of course, I should understand the whole project then to give right codes.So after visual achievements, I also tell you what I have done for data cleaning and data analysis. 

## Achievements
- As follow.
 

***

本博客记录9月整月广鹤作为 atl4dama python 项目成员的行为及输出作品. 因项目还处于中间阶段, 其他成员输出及项目成果暂不展示. 

## 项目背景
- 分析对象
    - ZoomQuiet 大妈五年时间记录数据
    - 剑飞五年时间记录数据, 
    - 广鹤数月时间记录数据
- 目标
    + 可视化展示效能
- 阶段
    - 过程: 数据清洗 -> 数据分析 -> 可视化
    - 从一个可能错误的 MVP 打通 数据清洗->统计->可视化 的流程, 了解整体图景
    - 针对性的逐一改进
    - 对比最终成果与最初 MVP 的差异程度


## 阶段成果
数据清洗 -> 数据分析 -> 可视化
小鹤主要负责可视化部分. 因此先展示可视化部分的成果. 当然, 项目作为一个整体, 对前面的步骤不了解是不可能产出符合整个项目要求的可视化成果的. 在可视化成果后面, 会展示小鹤在数据清洗和数据分析中的输出. 

### 可视化 visual: SET4 折线图 line plot html 版生成
~ [lgh4BokehHtml.ipynb](https://github.com/DebugUself/du4proto/blob/atl4dama/ipynb/lgh4BokehHtml.ipynb)的探索成果应用


    _atl2log
    ༄  python lgh8html.py atl2SET4lgh_all.csv

in _atl2log : lghset4lines.html show every year line plot in browser.

![](https://ws4.sinaimg.cn/large/006tKfTcgy1fjv8qch7m2j30xu0ysn16.jpg)

- 代码 code
```

#!/usr/bin/python
# -*- coding: utf-8 -*-
'''base bokeh make inline html plot
    - deal with atl2SET4dama_all.csv
    - damaset4lines.html in _atl2log 
    - df-> bokeh source
    - years in different html
    - all years htmls for one time
'''

__version__ = "v17.9.21.0922"
__author__ = 'lgh'
__license__ = 'MIT@2017-05'

'''
make line plot
'''
import sys
from bokeh.plotting import figure, output_file, show
from bokeh.models import ColumnDataSource
import pandas as pd
import numpy as np
#import matplotlib.pyplot as plt

def set4plot(cvsf):
    
# open .csv and add column 
    tr = pd.read_csv(cvsf, names=['year','week','set4'])
    #print(tr.head())
    
    #mr= tr[tr['year'] == 2016]
    #print(mr2013)

        #create unique list of year
    UniqueYears = tr.year.unique()
    #print (UniqueNames)

    #create a data frame dictionary to store your data frames
    DataFrameDict = {elem : pd.DataFrame for elem in UniqueYears}
    #print (DataFrameDict)

    for key in DataFrameDict.keys():
        DataFrameDict[key] = tr[:][tr.year == key]
        #print(DataFrameDict[key])
        #print (DataFrameDict[2014])
    #source = ColumnDataSource(DataFrameDict[2014])

    # output to static HTML file
    year_list = np.array(UniqueYears).tolist()
    #print(year_list)
    for i in year_list:
        source = ColumnDataSource(DataFrameDict[i])
        output_file("lghset4lines.html")
        # create a new plot with a title and axis labels
        p = figure(title="set4" + str(i), x_axis_label='week', y_axis_label='set4')
        # add a line renderer with legend and line thickness
        p.line('week', 'set4', legend="Temp.", line_width=2, source = source)
        # show the results
        show(p)

if __name__ == '__main__':
    print(__version__)

    if 2 != len(sys.argv) :
        print('''Usage:
        $ python lghbokeh.py path/2/XXX.csv
                #''')
    else:
        _csv = sys.argv[1]
        set4plot(_csv)
```

### 数据清洗 data analyze
- 因原始数据不同, 对广鹤数据清洗/分析及可视化的脚本做相应调整 
- because of raw data's difference, change some code.

name|difference原始数据 与dama原始数据不同|.py 相应脚本|相应代码 code
---|---|---|---
lgh|第1列是事件, 第2列才是类型|zq1atl2lines.py|''' _exp.append(line.split(',')[1]) '''
lgh|类型与大妈不同| zq2atlact.py|把自己的字符串放进input 等列表
lgh|广鹤的到秒, 大妈的到分|zq3st2sec.py|'''"%Y-%m-%d %H:%M:%S" ''' 
lgh|中期 weekly 数据|zq6split4weekly.py|在 raw/lgh 内新建 weekly 文件夹,```exp_csv = '../../raw/lgh/weekly/{}-w{:02}.csv'. ```
lgh|名字不同| zq8html.py|"lghset4lines.html"

### 数据分析 data analyze
因为折线图显示出的数据错误, 翻回代码和原始数据, 找到 bug并修复. 

line plot shows data mistake, go back to code and raw data, get bug and fix it. 
- [源数据 bug, 补一行代码, 中间试好多行](https://liguanghe.github.io/2017/09/20/lgh2DebugSET4data0919/)

## 工具 tools 
- Python3
- Jupyter Notebook
- Pandas
    + 科学家最喜欢用的强大数据分析模块
- Bokeh
    + 小众软件, 如何发现这种利器的方法, 以后再书.

## 图书 books
- [数据可视化 到 可视化信息 浅述 - 简书](http://www.jianshu.com/p/49132ffcac8b)
- [shmuelamar/cbox: convert any python function to unix-style command](https://github.com/shmuelamar/cbox)
- [PythonDataScienceHandbook](https://jakevdp.github.io/PythonDataScienceHandbook/index.html)
- [How to Generate FiveThirtyEight Graphs in Python](https://www.dataquest.io/blog/making-538-plots/)
- [比较类](https://antv.alipay.com/vis/doc/chart/classify/compare.html)

## Timelog
- 0901 从0 开始 pandas 想做周的散点图, 队员表示偏离项目.
- 0908 set4 指数 全自动化 atuo set4
- 0913 pandas 做 set4 折线图, 了解 pandas 折线图的 demo, 生成第一张折线图
- 0915 set4 指数 错误数据追查并改正
- 0918 pandas 逐张做出 每年折线图, 在 .ipynb中呈现
- 0923 bokeh 逐张做出 每年折线图, 通过 .py 形式, 并与前面的数据清洗/数据统计串联, 本地即可生成多张折线图. 

## 致谢 Thanks 
- @ZoomQuiet 大妈 立项,招募,引导,像<怎样解题>里的完美老师一样言传身教, 循循善诱, 提供高手思路, 筛选工具. 
- 队友(怼友) @Mxclover 小明 和 @zhangshiying 诗颖 投入的时间和精力,输出的脚本和文档, 每周一次的例会以及当晚怼周会的共同展示. 
- 怼圈 @DeBugUself 各个小伙伴们的关注和倾听
- 开智学堂 py103 课程 提供了我们认识的机会

以上致谢, 强烈地想放在最上面, 但是, 从读者角度出发, 最开始是想明白文章到底在说什么吧.故放在这里压轴咯. 
