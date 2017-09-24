## 线性记录
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

ipynb|try|src/md
zq0||readme.md
zq1||
zq2||zq7SET4.py
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





