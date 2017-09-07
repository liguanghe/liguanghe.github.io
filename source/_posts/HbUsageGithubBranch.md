---
title:  Git 入怼之独立分支
date: 2017/9/7 21:35:32
categories: 
- github


tags: 
- git
- branch
- repository
- remote
- orphan
- new way
- wiki
- thinking
- debuguself
- better
- output


---


- 此分支非彼分支, 即不是一个项目中为了完善项目, 从而早晚要合并到主分支的其他分支. 而是永远不会合并到主项目, 仅为方便怼友互看的独立分支. 每个独立分支是一个独立的项目. 
- 此分支特征
    + 新建时基本空白, 不包含主分支的内容
        * git 会自动把之前版本的内容复制到你的新版本, 我们要对抗之.
        * 需要包含: git.ignore 和 README.md, 自己新建. 
    + 难以 merge 到其他分支
        * git 会自动 merge 或关联到其他分支, 我们要对抗之.

## 操作
### 孤子分支(你将在怼圈里建的分支)

- 新建一个孤子分支
```
$ cd repository
$ git checkout --orphan orphan_name
$ git rm -rf .
rm '.gitignore'
$ echo "#Title of Readme" > README.md
$ git add README.md
$ git commit -a -m "Initial Commit"
$ git push --set-upstream origin orphan_name
```

### 纯净本地复本
当前分支

    ༄  git br -a
    * master
      zoejane
      remotes/origin/134_career
      remotes/origin/134_spider
      remotes/origin/DM_tools
      remotes/origin/DUW
      remotes/origin/DU_tools
      remotes/origin/HEAD -> origin/master
      remotes/origin/LearnWebScraping
      remotes/origin/ZQ4mDjango
      remotes/origin/ZQclj
      remotes/origin/ZQgo
      remotes/origin/ZQipynb
      remotes/origin/ZQmma
      remotes/origin/bamboo
      remotes/origin/csapp
      remotes/origin/deepNLP
      remotes/origin/hstaoqian
      remotes/origin/leiyunhe
      remotes/origin/master
      remotes/origin/mxclover
      remotes/origin/spider
      remotes/origin/tl2wc
      remotes/origin/zoejane


本地复本:

    ༄  du -hs *
    3.0M    CSAPP
     17M    DUW
    3.7M    TL2wc
     14M    ZQ4mDjango
     14M    ZQclj
     14M    ZQgo
    1.2M    ZQipynb
    2.0M    ZQmma
     14M    bamboo
     15M    deepNLP
    2.4M    dm_tools
     20M    tools4DU
     18M    zoejane


真正孤儿分支复本:

    ༄  du -hs *
     32M    2013.programming-clojure
    296K    DUWeekly
    180K    clj_ZQ
    812K    dj_ZQ
    140K    go_ZQ
    424K    ipynb_ZQ
    148K    mma_ZQ
    4.0K    requirements.txt
    400K    srv4DU.leo
    776K    st_heroku
    740K    tools4DU

### 本地如何预防孤子分支合并
- 本地新建一个文件夹, git关联以上孤子分支. 
```
$ cd(注意, 这很重要, 不要在du4proto 里面建这个文件夹)
$ mkdir branch_name
༄  cd branch_name
༄  git init
...
༄  git remote add -t branch_name -f origin git@github.com:DebugUself/du4proto.git
༄  git co branch_name
༄  git br -a
* branch_name
  remotes/origin/branch_name
༄  git pl
Already up-to-date.

```

### 万一本地副本被污染的解决方案
意外将其他分支 merge 到孤子分支, 会导致远程仓库的文件过大, 浪费每位成员的网络资源, 因此要语义杜绝. 但意外发生, 解决方案如下:
- 检查本地分支的工作复本是否被污染
```
$ git ll 
```
命令查看仓库分支的版本变化，对比污染和孤子分支的版本历史关系图
- 如果被污染, 重新clone新复本
    - 删除原来的文件夹
    - 新建文件夹, 重复上面'本地如何预防孤子分支合并'中的命令

- 如果已被污染且push到远程仓库，造成远程仓库也被污染了
  - 手动备份需要的文档及代码
  - 然后强行回滚至未被污染的状态
  - 最后正常的push

## 关联
- [Git - git-checkout Documentation](https://git-scm.com/docs/git-checkout/1.7.3.1)
- [Create an orphan branch in a repo.](https://gist.github.com/seanbuscay/5877413)
- [如何建立一個沒有 Parent 的獨立 Git branch | ihower { blogging }](https://ihower.tw/blog/archives/5691)


## 心
没明白就是没明白. 大妈觉得明明白白的, 我就是不明白. 

私下问竹子, 竹姐一句话:新建文件夹即可. 豁然开朗. 

这就是思维误区. 之前认知写作课给 github 做 bp, 理解分支是独立的时间线, 就应该在一个文件夹里, 好像是这个文件夹的平行宇宙. 但是, 大妈在怼仓库里建立的分支, 或者说, 让这个分支所起的作用, 是完全不同于一般意义样的分支的. 竹子一句话, 新建文件夹, 实际上是说, 它们在同一个宇宙里, 不能重叠的. 我自己以为懂了, 但实际上, 却一直没懂. 

遇到 git 的问题, 我的第一反应还是再看一遍廖雪峰的 git 教程. 因为 git 自己的教程我比较难看懂. 但大妈说, 看别人写的教程, 再好也是别人嚼过的甘蔗渣. 而这也恰恰**是我引发这次血案的本质原因**. 大妈说的孤鸿分支, 以及在本仓库中各个分支, 廖雪峰的教程里根本没提到过. 廖雪峰介绍了一般的分支, 即一个项目里面的分支起到解决 bug 和多线程的问题, 最终是要合并的. 而在玻璃花园里, 各个分支相互独立, 是不同的项目, **没什么可能合并**. 并且, 要对抗 git 想要合并的属性. 

这是怼圈特别的设置, 当然也是对 git 的进阶利用. 但在我个人的思维定式下, 就是无法理解. 
即使大妈已经给出来 git 命令, 我也试着操作, 还提出了问题, 大妈也让我自己怼明白, 但我就是没有怼. 随后22天之后, 引发了血案之宏大 merge.

这件事放在新人刚来的前一刻是很有启发的. 因为随后大量的项目会进来, 这个反 git 一般常识(当然, 这也是 git 的高阶用法)的设置, 很有可能成为多人犯的大坑. 

**同时, 这件事也让我见识到了自己构建知识树的重要性. 别人的内容永远是别人实操得来的自我领悟, 可以借鉴却不应成为核心知识, 把这当做核心知识, 很可能以偏概全, 自我设置壁垒, 从而犯下视而不见或无法理解更精深内容的可能.**

**建立自己的知识树, 大妈和阳老师都说的很明白, 去看官方文档啊, 从源头做起啊.** 

而且我这样说大妈就会明白, 实际上我没弄懂的并非版本, 版本仓库, 协同, 因为我自己写了这块的教程(见上文), 实际上也已经明白, 我的问题就出在, 还是认为分支就是要合并的那种用法. 

所以这个问题的解决方案就是, 在操作指南的基础上, 前面加上一段话: 

git 仓库的分支功能, 原意是为了完善项目, 记录对于一个项目的各种可能, 确定这个功能后即可合并到主分支( master). 但在怼圈, 每个分支是一个独立的项目, 是为了方便大家看到他人的项目. 这些项目不会合并, 我们也要尽可能的防止合并( git 及 github 喜欢合并) . 并且, git 本身会将主分支的内容复制一份放在你的新分支里, 从一个版本给接下来的所有版本, 而这也是你独立项目所不需要的, 举例来说, master 里的文件都是大家的计划, 而你的分支里是你的项目文件, 你的分支并不需要哪些计划. 所以, 你需要建立一个孤鸿分支. 

好, 接下来这件事的实际次序是: 

1. 在 master 的基础上建立一个孤子分支. 
2. 在 本地 新建一个文件夹, 关联这个孤子分支.

这样做的好处是:
1. 新建的分支不继承原本主分支的内容
2. 新建的文件夹很难 merge 到主干

必须这样做, 不要抱着侥幸心理. 
比如我会在莫名其妙 merge 之后(再说一遍, 这是 git 的属性), 把多出来的文件删掉, 但是问题来了, git 不仅仅包括文件, 还包括记录这些文件所有版本的变动, 这些看不见的内容也很庞大, 而这是你看不到所以不会删掉的内容, 然而他们却真实存在, 占用远程仓库的空间, 也占用你同伴们的空间. (现在这个血案越写越明白了). 

好了, 完成大妈在26天前就已经给出的任务: 
- 嗯哼明白 从孤子分支创建到本地净分支仓库复制流程
- 并增补wiki, 从小白角度说个明白,
- 以及将文档->安装到合理的索引树中

->交付 wiki: 见上文.