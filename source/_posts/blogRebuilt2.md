---
title: 用 git 及 github 的正确方式来重建博客
time: 2017/05/26 8:41:19
categories: 
- WriterEnvironment
tags:
- hexo
- next
- git
- github
- github pages
---
## 重建本地仓库, 与远程连接.
遇到的问题:
![]()(http://ww4.sinaimg.cn/large/006tNc79gy1fft9uyau2bj312q0vcwmf.jpg)

此次重建不顺利, 重新设置的过程, 一次设置了比较多的内容, 导致出现这个的时候, 我都不知道哪里出了问题. 

本地仓库和远程仓库都删掉, 从 0 开始再重建一个博客. 这样做了几次, 愚蠢.

严格遵守: 每一步骤的作用 - 新建分支 - 每一步改动 - commit(记录) - 测试无误 - 合并 
尝试用 git 及 github 的正确方式来重建博客. 

- 在本地升级全部环境
	- \`$ brew upgrade git
		`-`$ brew upgrade npm
		`-`$ brew upgrade node.js
		`-`.io $ npm update hexo
		\`

- \`本地建立同名文件夹 username.github.io ,
	`-`$ hexo init username.github.io
	`-`$ cd username.github.io
	`-`$ npm install
	\`
- `$ git remote add origin https://github.com/liguanghe/liguanghe.github.io.git`
- `$ git co gh-pages`
- `$ git pl`
- 这里会出现can’t merge unrelated- history
- \`$ git  log
	`-`$ git reset --hard 5esdm(版本号)\`
回到 commit version ‘add next’ 即设置 next 之前
- `$ git pu -f origin gh-pages`

## 探索 git 的新功能, 用测试仓库.
新建一个仓库, 并与本地连接. 探索 git 的功能
测试 git merge
git merge new-branch
$ git st
$ git co gh-pages
$ git co -b test
$ echo branch \> branch
$ git add .
$ git ci ‘try to merge’
$ git co gh-pages
$ git merge test

$ git merge --no-ff -m 'ls' test
Merge made by the 'recursive' strategy.
 branch | 1 +
 ls     | 1 +
 2 files changed, 2 insertions(+)
 create mode 100644 branch
 create mode 100644 ls

$ ls
gh-pages 里出现了 branch
$ git co master
master 中没有 branch(新建的文件)

成功. 
## git 添加新功能
用 git 的方法, 新建分支rss - 添加功能 - 测试 - 合并到 gh-pages 分支 - 删除rss

$ git co -b rss
$ npm …
$ hexo  …
$ hexo s 
$ git st
$ git add .
$ git ci “npm and hexo …’
$ git st
$ git co gh-pages
$ git st
$ hexo s
$ git merge rss
解决冲突. 
$ git merge rss
$ git br -d rss


### RSS
添加 rss 的方法, 我在用官方文档推荐的 hexo-migrator-rss 插件. 遇到建立 rss 报错 ‘not a feed’的问题. 用 hexo-generator-feed 插件可以建立 rss.

* ["not a feed" when: hexo migrate rss http://liguanghe.github.io · Issue #11 · hexojs/hexo-migrator-rss]()(https://github.com/hexojs/hexo-migrator-rss/issues/11#issuecomment-303743420)
* [hexojs/hexo-generator-feed: Feed generator for Hexo.]()(https://github.com/hexojs/hexo-generator-feed)


## 关联
[git - How can I remove a commit on GitHub? - Stack Overflow]()(http://stackoverflow.com/questions/448919/how-can-i-remove-a-commit-on-github)

[rebase - Git refusing to merge unrelated histories - Stack Overflow]()(http://stackoverflow.com/questions/37937984/git-refusing-to-merge-unrelated-histories)















