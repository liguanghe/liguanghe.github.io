---
title: Git One branch to Multiple Repositories
date: 2017/10/15 09:46:32
categories: 
- github


tags: 
- git
- remote
- branch 
- cooperation
- project
- Repository
- lghDL


---



~如有更好的方法, 欢迎推荐

## 需求
- 在怼圈半年, 完全熟悉了这里的模式, 希望将我的一切项目都在怼圈的分支中进行. 
- 1. 同时, 参加了开智的课程 py104 课程和 dl102
    - (1) py104 的结业项目,我设定为: 自动化生成我的时间报告. 这属于atl4dama 的引申支线任务. 
    - (2) dl102 的日常任务
- 2. 以及, 当我想求职的时候, 想让某些特定的人看到我的所有项目成果.

## 隐私及知识产权
1(1). 怼圈是基于 开智 python 课程引申出的社群, 怼友都是开智群友, 很多在 py104 担任教练或复训. atl4dama 也是大妈带着的一个项目, 将这部分公开给 py104的群友, 也是很好的示范作用. 

1(2). 我个人的深度学习分支, 以及怼圈内其他几位参加课程的同学, 如能在这里透明的完成项目, 互相抱团, 加速完成任务, 也是开智课程, 互相也都有兴趣

## 思路

- 基于孤子分支以及分支的独立文件夹, 在其上添加推送到另外一个私有仓库的功能. 同时也在 git官方文档/google/stack 时, 得到可以添加多个 remote 仓库. 其他方法尚未尝试, 欢迎推荐.

- 连接怼圈仓库与开智课程仓库
    - 开智课程仓库有固定的格式, 课程负责人希望的协作方式是 fork. 因为有100多人, 用直接开分支的方法, 入门门槛高(不过这应该也是有可能在 py105 实现的吧, 独立分支的 wiki 都写出来了).
    - DebugUself/du4proto at lghDL ←→ liguanghe/DeepLearning101-002 at lghDL -> (forked)AIHackers/DeepLearning101-002
    - 实现怼圈及开智课程成员均可以看到这个项目的进展. 

## 实现
- 在两个仓库中建立同名孤子分支
    + 先将远程仓库 clone 到本地以新建孤子分支lghDL, 之后不用这个本地文件夹. [HbUsageGithubBranch · DebugUself/du4proto Wiki](https://github.com/DebugUself/du4proto/wiki/HbUsageGithubBranch)
- 在本地建立与孤子分支同名的文件夹. 
- 为本地文件夹添加两个远程仓库 [Git - Working with Remotes](https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes)
    + git remote add name(注意, 这里另起名字, 不是 origin)/gihtub ...
- 将本地文件夹分别 git pull 和 git push 到两个远程仓库的同名分支. 
    + git pl origin lghDL
    + git pu origin lghDL

```
$ git remote show origin
* remote origin
  Fetch URL: git@github.com:DebugUself/du4proto.git
  Push  URL: git@github.com:DebugUself/du4proto.git
  HEAD branch: master
  Remote branch:
    lghDL tracked
  Local branch configured for 'git pull':
    lghDL merges with remote lghDL
  Local ref configured for 'git push':
    lghDL pushes to lghDL (local out of date)
```

    + git pl dl(name) lghDL
    + git pu dl(name) lghDL 

```
$ git remote show dl
* remote dl
  Fetch URL: git@github.com:liguanghe/DeepLearning101-002.git
  Push  URL: git@github.com:liguanghe/DeepLearning101-002.git
  HEAD branch: master
  Remote branches:
    lghDL  tracked
    master tracked
  Local ref configured for 'git push':
    lghDL pushes to lghDL (local out of date)
```

+ 新仓库的不相关历史 [rebase - Git refusing to merge unrelated histories - Stack Overflow](https://stackoverflow.com/questions/37937984/git-refusing-to-merge-unrelated-histories)

```
$ git pu dl
To https://github.com/liguanghe/DeepLearning101-002.git
 ! [rejected]        lghDL -> lghDL (non-fast-forward)
error: failed to push some refs to 'https://github.com/liguanghe/DeepLearning101-002.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
liguanghedeMacBook-Pro:lghDL liguanghe$ git pl dl lghDL
From https://github.com/liguanghe/DeepLearning101-002
 * branch            lghDL      -> FETCH_HEAD
fatal: refusing to merge unrelated histories
```


```
$ git pl dl lghDL  --allow-unrelated-histories
From https://github.com/liguanghe/DeepLearning101-002
 * branch            lghDL      -> FETCH_HEAD
Already up-to-date!
Merge made by the 'recursive' strategy.

```
再试就可以了
```
$ git pl dl lghDL
From https://github.com/liguanghe/DeepLearning101-002
 * branch            lghDL      -> FETCH_HEAD
Already up-to-date.
liguanghedeMacBook-Pro:lghDL liguanghe$ git remote show dl
* remote dl
  Fetch URL: https://github.com/liguanghe/DeepLearning101-002.git
  Push  URL: https://github.com/liguanghe/DeepLearning101-002.git
  HEAD branch: master
  Remote branches:
    lghDL  tracked
    master tracked
  Local ref configured for 'git push':
    lghDL pushes to lghDL (up to date)
```

## 每次拉送
- ```$ git pl/pu``` 默认是从 origin 的仓库中
- ```$ git pl dl(name) lghdl(branchname)``` 即可从对应仓库中拉送 
- 这里应该可以优化, 同时拉送, 不需逐个进行, 继续探索中. 

## 参考
- [HbUsageGithubBranch · DebugUself/du4proto Wiki](https://github.com/DebugUself/du4proto/wiki/HbUsageGithubBranch)
- [Git - Working with Remotes](https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes)
- [github - Git - Pushing code to two remotes - Stack Overflow](https://stackoverflow.com/questions/14290113/git-pushing-code-to-two-remotes)
- [What is "origin" in Git? - Stack Overflow](https://stackoverflow.com/questions/9529497/what-is-origin-in-git)
- [Adding a remote - User Documentation](https://help.github.com/articles/adding-a-remote/)
- [rebase - Git refusing to merge unrelated histories - Stack Overflow](https://stackoverflow.com/questions/37937984/git-refusing-to-merge-unrelated-histories)


## 下一步
- 大妈反馈用 config 更容易实现, 进一步探索中
- 分支中的子文件夹如何到多个远程仓库.

## 用时
1013 lgh 180 min