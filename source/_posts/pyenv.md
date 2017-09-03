
---
title:  Mac OSx Python 环境配置(操作指南)
date: 2017/9/2 15:35:32
categories: 
- python


tags: 
- python
- pyenv
- wiki
- thinking
- environment


---

## why
- 用 pyenv 管理 python 版本, 而不是用 anaconda. 理由: [Python环境出坑记](http://blog.junyu.io/posts/0707-python-env-config.html)
- pyenv/shell 等原理: [Python环境出坑记](http://blog.junyu.io/posts/0707-python-env-config.html)

> 浚宇说[python环境出坑记]: 一个命令的执行过程，`输入命令 -> shell 读入命令 -> 查找文件 -> 定位文件中的环境变量 -> 浏览环境变量对应的路径下的文件 -> 在文件里寻找命令和执行方法 -> 找到了，按照要求执行 -> 找不到，输出找不到`，
直接照搬，python 输入后没有找到我想要的效果，可以跟着这个引导看哪个环节出错了.
所以，我这篇博客不是手把手的教程，更像一个入口，把可能用到的知识都串联了一遍，供大家参考。我当初探索最痛苦的是“不知道自己不知道”，现在界定了问题的知识边界，按理来说探索起来更方便。
为什么不写手把手的教程呢，因为环境问题的任何一个环节都可能出错，无法穷尽。授人以鱼不如授人以渔，这里的知识边界能够帮助大家探路和减小探索的困难程度，但是这个探索的过程，还得自己来做。


## 卸载 anaconda 及 清理环境
- 见[Python环境出坑记](http://blog.junyu.io/posts/0707-python-env-config.html)中 ### bye anaconda
- 将 .bash_profile 文件中的内容删除. 
### 安装 pyenv
结合: [pyenv/pyenv: Simple Python version management](https://github.com/pyenv/pyenv#installation) 和 [Aoi-planetDUer | DebugUself with DAMA ;-)](http://du.zoomquiet.io/2017-08/aoi-planet/#wow1) 中关于 pyenv 安装的部分. 
- 选择安装在哪个文件夹
    + 大妈安装的位置不同(我没懂)
    + 官方文档推荐 HOME, 也就是自己安装在电脑总目录. 我是这么做的. 
- git clone/brew 两种方法均可. 
- 设置(新建或改写其中内容) .bash_profile 文件, 内容仅三行:
```
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
```
    - 方法1: echo (官方文档)
    - 方法2: 直接改写. 
- 关联 PATH
    +  方法1: $ source .bash_profile (大妈使用)
    +  方法2: $ exec "$SHELL" (官方文档, 我用不好使)
## 运行 pyenv 
```
$ pyenv --versions
$ pyenv install 3.6.1
$ pyenv install 2.7
$ pyenv versions
* system (set by /Users/liguanghe/.pyenv/version)
  2.7
  3.6.1
$ python --version
Python 2.7.10
$ pyenv 3.6.1
pyenv: no such command `3.6.1'
$ pyenv global 3.6.1
$ python --version
Python 3.6.1
```

- 在 jupyter notebooke 中检验, 如不是, 重新安装 jupyter notebook.
```
$ pip install jupyter notebook
```

## 关联
- [pyenv/pyenv: Simple Python version management](https://github.com/pyenv/pyenv#installation) 
- [Aoi-planetDUer | DebugUself with DAMA ;-)](http://du.zoomquiet.io/2017-08/aoi-planet/#wow1) 
- [Python环境出坑记](http://blog.junyu.io/posts/0707-python-env-config.html)
- [广鹤参照以上三文档布置环境的线性记录: NotePyenvPython.md](https://github.com/liguanghe/liguanghe.github.io/blob/gh-pages/source/_posts/NotePyenvPython.md),如果你遇到坑, 可以到里面看看, 或许可找到跨坑点. 

## 未回答的大妈之问
- pyenv 依赖什么?私人用部属在哪儿合理?

## 致谢
- 感谢浚宇 @Wangjunyu  提供珍贵文档, 建议投稿怼周刊
- 感谢大妈 @ZoomQuiet  提供珍贵文档, 我已订阅博客, 接下来尝试投稿. 

## 心
在所有的程序安装或运行时, 我常常遇到的问题就是:
- 在什么时候用?
- 在哪里用?
- 格式是什么? 怎么知道我找对了?
以上其实是程序员的内隐知识, 他们见多了, 知道文本是什么样子的, 该用在什么地方, 所以会不知不觉的简略. 检验自己教程是否合格的标准, 就是回答上面三个问题. 


## timelog
- 2017-09002 李广鹤lgh 发布 wiki 5 min
- 2017-08-31 李广鹤lgh 教程 30 min
- 2017-08-30 李广鹤lgd 操作及线性记录 330 min
(大妈布置 pyenv 时间, 30 min, 我用了10倍的时间...)
