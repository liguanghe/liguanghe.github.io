
---
title:  源数据 bug, 补一行代码, 中间试好多行
date: 2017/9/20 11:35:32
categories: 
- python


tags: 
- python
- bug
- data
- thinking
- story
- record
- pandas
- readme
- data


---


## bug
- (时间账单项目)做折线图时发现异常. set4 应该在0-2 之间, 在10-20区间的都是异常, 尝试找出这两个数据(另开 .ipynb 文档检测数据异常)
    ```
    看atl2SET4dama_all.csv 
    2015,01,17.927306943389056
    2014,01,21.787416651210933
    ```


## 思路
- 将最迟的数据(单周数据)放在最迟的算法里, 发现是什么问题. 
- 回推 
    - 原始数据 - 数据清洗 - 数据统计
    - 13-2.report -> atl2dama4all.csv -> df_isocalendar.csv -> weekly(2014-w01.csv) -> atl2SET4dama_all.csv
- 不用看回尝试 .ipynb, 而是应该直接 copy .py 脚本, 在自己的.ipynb 格式里拆解,逐一计算中间数据,排查是数据还是算法的问题. 
- 理解每个过程数据的意义. 

## 解决
- 因数据有错, 所以改进算法. 
- 有结束时间小于开始时间的记录错误
- 要筛除这类数据, 不去使用.
- 添加一行代码: 
```
x=df4LOTa_drop_top1sleep[df4LOTa_drop_top1sleep.du_time > 0]
TBT = x.du_time.sum()
```

## changelog

- 将2014w01 周数据放入 zq7 逐个过程数字算出: [lgh2DebugSET4data0919.ipynb](https://github.com/DebugUself/du4proto/blob/atl4dama/ipynb/lgh2DebugSET4data0919.ipynb)

- 2014w01 set4 数据异常排查:  TBT = -31241700.0, **异常**, TBC = 68(属于正常范围), 导致 TBI = -15.952665441176471   
对比 2014w02 TBT=225060 TBC=77 TBI=0.1  
- 2015w1 TBT = -31330680.0 TBC = 56 TBI = -19.426264880952377

- TBT 是基于什么, 为什么在2014年会异常
- 是 TBT 这个变量本身的设置问题, 还是2014年的数据在这个变量里不适合? (edited)


### TBT? 
大妈在zq2analyze.ipynb 中说, 这是中断时长
```
+ 以及每天的: `中断指数` (**TBI** ~ Totle Broken Index) 为加权
    * TBT ~ 中断总时长
    * TBC ~ 中断次数
    * 设每天有效工作时间为8小时
    * (TBT/TBC)/(8*60*60) -> 平均中断时长 占有效工作时间比例 -> TBI 
    * 即,每天平均中断时长占有效工作时间的比例, 记为: `xx.xTBI`
```
结合代码
```
df4LOTa_drop_top1sleep = df4LOTa.drop(_top1sleeps, axis=0)
```
这是去掉 睡眠 数据的表格
```
TBT = df4LOTa_drop_top1sleep.du_time.sum()
```
意思应该是: 除了第一睡眠数据和输出时间之外的其他时长的总和

TBC 应该是 除了第一睡眠数据和输出时间之外的其他数据的次数
TBI 应该是 其他时间/其他次数/8小时(工作时长)

TBT 不应该是负数, 说明有一条不在20%的数据是记录错误
排查方法见上文, dutime<0

添加解决: dutime>0

这里要注意的是:遇到源数据有问题, 也不应该删掉源数据, 而是用代码来从根本上排除错误的源数据.

## 心
- 项目下一阶段的人, 也可能随时需要发现上一阶段结果出了问题, 此时再学习对应脚本, 用 .ipynb 拆解代码逐个了解, 是很好的办法. 
- 尽可能的多了解之前的代码 
- 数据的问题不难, 运用以前上学时的简单数学和过往办公软件的经验, 再加上 pandas的简单操作, 可以解决很多问题. 


