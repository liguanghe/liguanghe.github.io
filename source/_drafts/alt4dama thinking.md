alt4dama 思路

从 0 接触项目. 盲目的目标中熟悉 pandas  到 清晰的目标 使用 bokeh. 

盲目目标 仍然想用 pandas 实现散点图的想法. 一周尝试后, 尝试工具的各种代码. 小组成员说没有用. 
开始靠近项目. 做 set4 可视化, 之前已经有大妈和小明关于这个图的数据分析, 单独考虑图片生成, 比数据生成和图片生成放在一起 容易多了. 

可视化倒退要的数据 一开始的理解是必须要.csv, 随后对整个数据分析的工具上手后, 发现了他们的内在联系, 一个 list也是可以的. 

0913 代码:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

tr = pd.read_csv('/Users/liguanghe/du4proto/src/_atl2log/atl2SET4dama_all.csv')
#print(tr)
#添加表头
tr.columns = ['year','week','set4']
#tr.head()
ax = tr.plot.line(x='week',y='set4')
ax
plt.show()
```

 tr.columns 被 Names = ... 取代

0918 代码: 

