## 读懂仓库文件夹 README.md 线性记录 兼思考 开发和运行环境
### 嗯哼
- 现象1
    + atl4dama 大妈在 ipynb 中开发完了整个脚本. 其中包括读取文件, 并操作.
    + 我git pl 仓库后, 打开大妈的 .ipynb文件, 直接 shift + enter, 诶? 报错显示文件不存在
- 现象2
    + 直接复制大妈的系列管道命令: ༄ find ../../raw/zoomquiet/weekly/*.csv |
xargs -I{} python zq7SET4.py {} > atl2SET4dama_all.csv
    + 报错说文件夹不存在?
- 命令行拆解管道命令, 逐一实现, 看看问题
- 一并要解决的, 是将文档中大妈散落的操作指南归化到总的 readme 上. 
- 跟上大妈的轨迹
ipynb -> (try) -> src
看的时候是相反的, 先看脚本 README.md, 测试结果可以看 .ipynb

ipynb|try|src/md
zq0||readme.md
zq1||zq1/2/3
zq2||zq4/5/6/7SET4.py
zq3||

- 直接尝试 zq7set4.py
```
liguanghedeMacBook-Pro:_atl2log liguanghe$ python zq7SET4.py
Usage:
        $ find raw/zoomquiet/weekly/ | python zq7SET4.py

liguanghedeMacBook-Pro:_atl2log liguanghe$
```
查看 zq7set4.py, 中写到: 
```
if __name__ == '__main__':
    #print(__version__)
    if 2 != len(sys.argv) :
        print('''Usage:
        $ find raw/zoomquiet/weekly/ | python zq7SET4.py 
                ''')
    else:
        _csv = sys.argv[1]
alt2SET4(_csv)
```

在命令行直接试:
```
_atl2log liguanghe$ find raw/zoomquiet/weekly/ | python zq7SET4.py
find: raw/zoomquiet/weekly/: No such file or directory
Usage:
        $ find raw/zoomquiet/weekly/ | python zq7SET4.py

liguanghedeMacBook-Pro:_atl2log liguanghe$ find: ../../raw/zoomquiet/weekly/ | python zq7SET4.py
-bash: find:: command not found
Usage:
        $ find raw/zoomquiet/weekly/ | python zq7SET4.py
```

逐层级去找 weekly 文件夹:
```
weekly liguanghe$ cat readme.md
# atl4dama.raw.zoomquiet.weekly
~ 大妈的原始数据 按照 周进行切割liguanghedeMacBook-Pro:weekly liguanghe$
```

好吧, 我被大妈骗了.weekly 里没有要处理的文件. 这个要处理的文件显然需要从头, 以源数据开始,管道命令, 最终生成我要的可视化源数据. 删掉中间文件害死人呀. 
```
def alt2SET4(csvf):
    _yyyy, _wn = os.path.splitext(os.path.basename(csvf))[0].split('-')
    df = pd.read_csv(csvf)
#print(df.head())
```
这里还是打开某个 csvf, 可能是: 
```$ python zq7set4.py xxx.csv
```
xxx.csv 在哪里呀? 
也可能是直接连其他脚本的. 

重点是zq1.ipynb, 对应的 src是什么? 
ipynb|try|src/md
zq0||readme.md
zq1||
zq2||zq7SET4.py
zq3||

zq1.ipynb 在这里: [du4proto/src/_atl2log at atl4dama · DebugUself/du4proto](https://github.com/DebugUself/du4proto/tree/atl4dama/src/_atl2log)
这个才是要放到中 readme.md 里的阶段文件. 

不过, 总的 README 不应该是最终功能的实现么? 随时让大家有总体目标的? 可以兼得,可以兼得. 

照做

```
$ _atl2log liguanghe$ cat ../../raw/zoomquiet/1302--report/*.csv
```

获得了所有的. csv内容, 不是这里, 是这篇文档的结尾: 
```
find ../../raw/zoomquiet/1302--report/aTLer_14*.csv |
xargs -I{} python zq1atl2lines.py {} |
python zq2atl2act.py |
python zq3st2sec.py |
python zq4uniq.py | sort -t',' -k1 > atl2dama2014.csv
```
先全部一次性 放到命令行执行, 报错 pip 错误. 
然后逐行添加
```
find ../../raw/zoomquiet/1302--report/aTLer_14*.csv 
```
显示出文件
```
find ../../raw/zoomquiet/1302--report/aTLer_14*.csv |
xargs -I{} python zq1atl2lines.py {} 
```
显示表格
```
find ../../raw/zoomquiet/1302--report/aTLer_14*.csv |
xargs -I{} python zq1atl2lines.py {} |
python zq2atl2act.py |
```
报错: 
```
Traceback (most recent call last):
  File "zq2atl2act.py", line 29, in <module>
    import cbox
ModuleNotFoundError: No module named 'cbox'
Traceback (most recent call last):
  File "zq1atl2lines.py", line 80, in <module>
    cl4base(_csv)
  File "zq1atl2lines.py", line 68, in cl4base
    print(','.join(_exp))
BrokenPipeError: [Errno 32] Broken pipe
...
BrokenPipeError: [Errno 32] Broken pipe
```
我没有 cbox 模块, 这个模块在哪里? 先到 zq2atl2act.py 里面看看.
```pip install cbox
```
可以安装诶, 再试.
```
find ../../raw/zoomquiet/1302--report/aTLer_14*.csv |
xargs -I{} python zq1atl2lines.py {} |
python zq2atl2act.py |
```
显示表格
```
find ../../raw/zoomquiet/1302--report/aTLer_14*.csv |
xargs -I{} python zq1atl2lines.py {} |
python zq2atl2act.py |
python zq3st2sec.py
```
显示表格
```
find ../../raw/zoomquiet/1302--report/aTLer_14*.csv |
xargs -I{} python zq1atl2lines.py {} |
python zq2atl2act.py |
python zq3st2sec.py |
python zq4uniq.py | sort -t',' -k1 > atl2dama2014.csv
```
到这里时, 没有output? 记得大妈说自己本地打出来吧. 
finder里面找到了 atl2dama2014.csv 文件, 接下来是统计这个文件. **注意, git pu 之前要把它删掉, 因为是中间文档** 
问题, 还是没有连接起来? 

先继续统计的部分. 
要经过 pandas? 
这部分的.py文件有没有整理出来? zq7SET4.py?
先管道下试试. 

```
find ../../raw/zoomquiet/1302--report/aTLer_14*.csv |
xargs -I{} python zq1atl2lines.py {} |
python zq2atl2act.py |
python zq3st2sec.py |
python zq4uniq.py | sort -t',' -k1 > atl2dama2014.csv |
python zq7SET4.py
```

显示: 
```
Usage:
        $ find raw/zoomquiet/weekly/ | python zq7SET4.py
```

又回到最初的原点, 但是, 我知道, 要中间生成 weekly 的内容. 
weekly 的内容需要看懂 zq2 里面的weekly

zq2anazlyse.ipynb 中提到的 atl2dama4all.csv 是怎么生成的, 与 atl2dama2014.csv 是什么关系? 

他们不是一个 , 因为直接用 python zq7set4.py 处理这个. csv, 给出的是上面的结果. 

发现 zq5pd0reclean.py 和 zq6split4weekly.py
先继续关联 
```
find ../../raw/zoomquiet/1302--report/aTLer_14*.csv |
xargs -I{} python zq1atl2lines.py {} |
python zq2atl2act.py |
python zq3st2sec.py |
python zq4uniq.py | 
zq5pd0reclean.py
```
显示: 
```
v17.9.10.0909
Usage:
        $ python zq5pd0reclean.py path/2/XXX.csv

Traceback (most recent call last):
  File "/Users/liguanghe/.pyenv/versions/3.6.1/lib/python3.6/site-packages/cbox/concurrency.py", line 53, in _simple_runner
    yield func(item, **kwargs), None
  File "zq4uniq.py", line 34, in uniq4ts
    print(dl)
BrokenPipeError: [Errno 32] Broken pipe
```

```_atl2log liguanghe$ find ../../raw/zoomquiet/1302--report/aTLer_14*.csv |
  xargs -I{} python zq1atl2lines.py {} |
python zq2atl2act.py |
python zq3st2sec.py |
python zq4uniq.py | sort -t',' -k1 > atl2dama2014.csv |
python zq5pd0reclean.py
v17.9.10.0909
Usage:
        $ python zq5pd0reclean.py path/2/XXX.csv
```

把 5 和 6 直接关联上
```
_atl2log liguanghe$ find ../../raw/zoomquiet/1302--report/aTLer_14*.csv | xargs -I{} python zq1atl2lines.py {} | python zq2atl2act.py | python zq3st2sec.py | python zq4uniq.py | python zq5pd0reclean.py | python zq6split4weekly.py
v17.9.10.1001
Usage:
        $ python zq6split4weekly.py path/2/df_wday.csv

Exception ignored in: <_io.TextIOWrapper name='<stdout>' mode='w' encoding='UTF-8'>
BrokenPipeError: [Errno 32] Broken pipe
Traceback (most recent call last):
  File "/Users/liguanghe/.pyenv/versions/3.6.1/lib/python3.6/site-packages/cbox/concurrency.py", line 53, in _simple_runner
    yield func(item, **kwargs), None
  File "zq4uniq.py", line 34, in uniq4ts
    print(dl)
BrokenPipeError: [Errno 32] Broken pipe
```

跳过 atl2dama2014.csv 和 atl2dama4all.csv 的不同, 直接用 5 处理atl2dama2014.csv.
```
_atl2log liguanghe$ python zq5pd0reclean.py atl2dama2014.csv
v17.9.10.0909
       du_start        du_end act_type
0  1.388490e+09  1.388495e+09    livin
1  1.388495e+09  1.388519e+09    sleep
2  1.388519e+09  1.388520e+09    chaos
3  1.388520e+09  1.388532e+09    livin
4  1.388532e+09  1.388547e+09    chaos
       du_start        du_end act_type
0  1.388490e+09  1.388495e+09    livin
1  1.388495e+09  1.388519e+09    sleep
2  1.388519e+09  1.388520e+09    chaos
3  1.388520e+09  1.388532e+09    livin
4  1.388532e+09  1.388547e+09    chaos
       du_start        du_end act_type  wday
0  1.388490e+09  1.388495e+09    livin     2
1  1.388495e+09  1.388519e+09    sleep     2
2  1.388519e+09  1.388520e+09    chaos     2
3  1.388520e+09  1.388532e+09    livin     2
4  1.388532e+09  1.388547e+09    chaos     2
       du_start        du_end act_type  wday  wn4y
0  1.388490e+09  1.388495e+09    livin     2     1
1  1.388495e+09  1.388519e+09    sleep     2     1
2  1.388519e+09  1.388520e+09    chaos     2     1
3  1.388520e+09  1.388532e+09    livin     2     1
4  1.388532e+09  1.388547e+09    chaos     2     1
du_start    5700
du_end      5700
act_type    5700
wday        5700
wn4y        5700
dtype: int64
```


在 \_atl2log 文件夹中找到了 df_isocalendar.csv

```_atl2log liguanghe$ python zq6split4weekly.py df_isocalendar.csv
v17.9.10.1001
```

这里没有在 weekly 的文件夹里生成文件

要这样: 
```
python zq6split4weekly.py df_isocalendar.csv
v17.9.10.1001
    <---W_start
```

出了很多.csv 文件, 
然后
```
༄ find ../../raw/zoomquiet/weekly/*.csv |
xargs -I{} python zq7SET4.py {} > atl2SET4dama_all.csv
```

在 _atl2log 中生成了 atl2SET4dama_all.csv

接下来用这个 .csv 在 ipynb中生成了折线图.

## 进一步的, 想把变成折线图的脚本(.ipynb)也变成像 zq7.py 一样的脚本, 但却有如下报错: 
```
$python lgh8set4plot.py atl2SET4dama_all.csv
Traceback (most recent call last):
  File "lgh8set4plot.py", line 14, in <module>
    import matplotlib.pyplot as plt
  File "/Users/liguanghe/.pyenv/versions/3.6.1/lib/python3.6/site-packages/matplotlib/pyplot.py", line 115, in <module>
    _backend_mod, new_figure_manager, draw_if_interactive, _show = pylab_setup()
  File "/Users/liguanghe/.pyenv/versions/3.6.1/lib/python3.6/site-packages/matplotlib/backends/__init__.py", line 32, in pylab_setup
    globals(),locals(),[backend_name],0)
  File "/Users/liguanghe/.pyenv/versions/3.6.1/lib/python3.6/site-packages/matplotlib/backends/backend_macosx.py", line 19, in <module>
    from matplotlib.backends import _macosx
RuntimeError: Python is not installed as a framework. The Mac OS X backend will not be able to function correctly if Python is not installed as a framework. See the Python documentation for more information on installing Python as a framework on Mac OS X. Please either reinstall Python as a framework, or try one of the other backends. If you are using (Ana)Conda please install python.app and replace the use of 'python' with 'pythonw'. See 'Working with Matplotlib on OSX' in the Matplotlib FAQ for more information.
liguanghedeMacBook-Pro:_atl2log liguanghe$
```
理解为命令行不是框架, 不能显示图形. 

## 下一步行动
- 把_atl2log 的8个脚本集合成一个 .py
- 生成所有现有数据的折线图
- 矫正
- 返回初心--可视化睱想
    + 时间帐单效能分析任务对多人不同数据的原创分析, 试图得到一种通用的效能指标, 从而进一步对比具体阶段工作的产出来印证指标的设计...
    + [du4proto/du_s03e51_zoomquiet_plan.md at master · DebugUself/du4proto](https://github.com/DebugUself/du4proto/blob/master/S03E51/du_s03e51_zoomquiet_plan.md)
```
SET4 的设计也只是出自俺的私人偏见
要通过我们自己的实践, 持续改进/优化/重构,
直到可以将效率和时间帐单通过 SET4 稳定关联起来哪
然后,我们的时间帐单就可以在不改变帐单记录行为的前提下, 
通过一个简洁指标, 把握住每天我们的效能状态了
```








## 心
我要一生与之抗衡的就是这个得意忘形啊, 一有点成就, 就给自己过高的预期和标签, 现实中完不成, 就行为瘫痪,说自己的不是. 求快求多求全的心bug, 要一点一点的完成. 

我看得懂明星的脚本, 看不懂大妈的脚本, 好想哭. 看不懂脚本, 不妨碍看懂他的 readme, 不妨碍协作.

如何与高手一起做项目? 

