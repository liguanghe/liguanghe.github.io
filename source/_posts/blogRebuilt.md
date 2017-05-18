---
title: hexo 博客的神坑及本质原因
time: 2017/05/18 23:27:13
categories: 
- WriterEnvironment
tags:
- hexo
- next
- git
- github
- github pages
---
## hexo 神坑及本质原因

hexo 博客引擎与 jekyll 最大的不同: 

jekyll | hexo
---|---
在 github 网站中生成页面 | 在本地生成后, 将生成页面上传到网站上
master 即可 | 两个分支, 一个设置文件, 一个页面文件


\*\*神坑: 页面文件放在哪个分支(master 还是 gh-pages,一定要是这两个名字), 根据 github pages 的仓库名称来定.
\*\*

> - 个人主页
> 库的名称为yourname.github.io的主页，页面文件应当在master分支下，以HTML文件为主，是没有Markdown文件。
> - 项目主页
> 库名不是yourname.github.io的主页，页面文件应当在gh-pages分支下，文件结构与个人主页基本一致，同样没有Markdown文件。

第一次搭建博客时, 没有弄明白这个问题, 跟着浚宇的博客, 分支是建立了,  博客内容生成在哪个分支是懵的. 

对 git 不熟, 一次没有 commit 就转换分支, 导致两个分支互相污染, 不能使用.  

如果一开始用 jekyll 来搭建博客, 就不会遇到这些问题. 当时觉得 jekyll 要自己布置页面, 设置功能, 难而且费时间, 而 hexo 有很多现成的功能, 页面也漂亮. 实际上, 因为上面这个坑, 花费了大量的时间, 遇到一个大大小小的坑.

比如: 因为一直检测 master,  next 主题下载后, 放在里面, github 不断检测为子模块(submodule) , 要进行相应的设置. 因为之前是不需要这个设置的, 所以肯定是设置哪里不对. 

但是, 为了这个问题, 发邮件给 github, 获得了, 如果里面有. git 文件夹, 就会产生子模块的问题, 大致了解了这是为了引用子项目, 属于 git 高阶技巧. (这个短时间之内用不上))

再比如: 一直是 404 页面, 或者是 master 上的.md 文件. 

如果这个时间,不是用来解决这个, 而是学习 jekyll 的布置方法, 说不定前端页面设计已经学会了. 这就是最初选择什么工具的原因.  阳志平老师还是继续推广 jekyll , 因为它不需本地布置, 从根源上就杜绝了发生这个问题的可能. 

即使如此, 仍做下最后努力, 把博客重建回来, 我需要它漂漂亮亮的.


## 入坑征兆:
如果你使用的是个人主页, 即 yourusername.github.io 作为仓库名. 又没有注意上面那个本质原因, 
你会遇到的坑:

1. github 发邮件给你告知失败.
> The page build failed for the `master` branch with the following error:
> The tag `fancybox` on line 77 in `themes/landscape/README.md` is not a recognized Liquid tag. For more information, see https://help.github.com/articles/page-build-failed-unknown-tag-error/.

因为 github pages 会到 master 里找生成的页面文件来显示, 它会对 hexo 默认的主题有异议.

为了绕过这个, 你会下载一个好用的主题 next , 于是遇到第二个坑:
2. github 发邮件给你告知失败.
> The page build completed successfully, but returned the following warning for the `master` branch:
> You are attempting to use a Jekyll theme, "next", which is not supported by GitHub Pages. Please visit https://pages.github.com/themes/ for a list of supported themes. If you are using the "theme" configuration variable for something other than a Jekyll theme, we recommend you rename this variable throughout your site. For more information, see https://help.github.com/articles/adding-a-jekyll-theme-to-your-github-pages-site/.
> For information on troubleshooting Jekyll see:
> https://help.github.com/articles/troubleshooting-jekyll-builds

原因与第一个坑一致, 这次是花式旋转, 也是可以解决的, 比如, 把 next 文件夹中的 .git 删除, 同时删除 config.yml 中那行 “theme: next” 还要删除 landsope 主题文件夹. 才不会生成子模块, 也不会升到上面的邮件了. 

这是一开始可以避免的. 

3. 每一次 deploy, 设置会变成初始的.
因为没有建立分支. 

## 绕坑指南( hexo 博客建立过程)
**务必严格按照以下顺序**
- 安装 hexo : [文档 | Hexo][1]
-  建站: [建站 | Hexo][2]
	- 这里会在本地建一个文件夹, 名称为yourusername.github.io
		- e.g.我的是: liguanghe.github.io
	- 下载 next 主题(hexo 人气最高)
		- $ git clone https://github.com/iissnan/hexo-theme-next themes/next
		- config.yml 里 theme: 后面的 landsope 删掉.
		- next 文件夹里的 .git 要在这时就删掉.(否则建站失败, 后面的都无效)
		- 自带的主题 landsope 也删掉. 
- 新建 github pages: 
	- 新建远程仓库: yourusername.github.io
		- e.g.我的是: liguanghe.github.io
		- 与上面的本地文件夹一致. 
	- 在本地文件夹里设置 git
		- $ git init
	- 关联本地与远程仓库
		- $ git remote add origin http:// … (你的远程仓库链接)
		- $ git push -u origin master
	- 新建 gh-pages 分支
		- 不是空白分支, 注意, 以后源代码都在这个分支.(再次重申, 如果你的远程仓库名是你的用户名的话)
		- $ git checkout -b gh-pages
		- $ git push -u origin gh-pages
- hexo 部署到 github: [部署 | Hexo][3]
	+ 在 config.yml 里添加 theme: next
	- $ npm install hexo-deployer-git --save
	- 修改\_config 关于deploy部分内容,这里共有两段内容代码需要修改

```
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
type: git
repo:  你的远程仓库 url`
(e.g.我的是: https://github.com/liguanghe/liguanghe.github.io  )`
branch: master
# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: http://http://hexo.junyu.pro
root: /
permalink: :year/:month/:day/:title/
permalinkdefaults:
```
- 启动部署
	- $ hexo deploy

## 注意!
- 配置文件永远在 gh-pages 分支, 不需转换分支到 master
- 转换分支前, 先 git add . /git commit  以防分支互相污染, 这将直接导致你回不去.
- 另外, 尝试添加新功能前, 另建分支尝试, 测试可用后再合并到 gh-pages 分支. 


## 参考
[文档 | Hexo][4]
[从零开始新建Hexo博客 | 浚宇的博客][5]
[Hexo常见问题解决方案][6]
[重建Hexo的教训 | 浚宇的博客][7]
[Configuring a publishing source for GitHub Pages - User Documentation][8]

## 关联
建立博客是像黑客一样创作的第一步, 如果你不想走这些坑, 以及省略独自摸索的过程, 可以搜索**开智学堂的像黑客一样创作** 教你搭建 [理想的写作环境：Git+Github+Markdown+Jekyll - 阳志平的网志]
(http://www.yangzhiping.com/tech/writing-space.html)

[1]:	https://hexo.io/zh-cn/docs/index.html
[2]:	https://hexo.io/zh-cn/docs/setup.html
[3]:	https://hexo.io/zh-cn/docs/deployment.html
[4]:	https://hexo.io/zh-cn/docs/index.html
[5]:	http://blog.junyu.io/posts/0002-start-blog-with-hexo.html
[6]:	http://xuanwo.org/2014/08/14/hexo-usual-problem/#Deploy%E4%B9%8B%E5%90%8E%EF%BC%8C%E9%A1%B5%E9%9D%A2%E9%95%BF%E6%97%B6%E9%97%B4404
[7]:	http://blog.junyu.io/posts/0007-a-mistake-rebuilt-hexo-blog.html
[8]:	https://help.github.com/articles/configuring-a-publishing-source-for-github-pages/