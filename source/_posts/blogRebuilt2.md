---
title: 用 git 及 github 的正确方式来重建博客
time: 2017/05/21 20:41:19
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
	- `$ brew upgrade git
		`- `$ brew upgrade npm
		`- `$ brew upgrade node.js
		`- `.io $ npm update hexo
		`

- `本地建立同名文件夹 username.github.io ,
	`- `$ hexo init username.github.io
	`- `$ cd username.github.io
	`- `$ npm install
	`
- `$ git remote add origin https://github.com/liguanghe/liguanghe.github.io.git`
- `$ git co gh-pages`
- `$ git pl
	`- `$ git  log
	`- `$ git reset --hard 5esdm(版本号)`
回到 commit version ‘add next’ 即设置 next 之前
- `$ git pu -f origin gh-pages`

## 















