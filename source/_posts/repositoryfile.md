---
title:  版本仓库文件存放指南
date: 2017/5/06 18:35:32
categories: 
- github


tags: 
- git
- wiki
- repository
- effiction

---

## 概述
- 仓库里应该放哪些文件格式,是做项目和协同重要的部分.

## 意义  
- 放什么文件反映对当前项目的理解
	- 你是否知道在做什么?
	- 你的项目需要哪些文件?
	- 你的项目不需要哪些文件?
- 版本仓库是保险库, 恢复项目环境
	+ 远程
	+ 何时何地, 有电脑和网络就可以工作
	+ 你的同事 clone 仓库后,是否可以立刻工作?

## 目标
- 文件是否值得放入的:简洁的公式/判定指标

## 操作
### 明确项目中的有用文件
- 描述自己的项目应该出现哪些格式的文件
- 源代码
- 其他生成代码的应用程序
- 源数据文件
- 项目文件/项目文档

### 明确项目中会产生的无用文件
- 格式
	- 自动生成的文件要格外注意
	- github 总结的 python 常见忽略文件[Some common .gitignore configurations][1]
- 可被容易再次生成的文件不需要放
	+ eg: .py
	+ eg: 缩略图
- 图片
	+ 课程中的 demo 网站中的图片
		+ 静态的, 美化用, 对工程无用.
		+ 照片太大, 占用流量和内存

### 忽略这些文件, 不上传到版本库
- .gitignore 文件用法
	+ 尝试创建分支时, 保留.gitignore
	+ 尝试了解.gitignore 里面的文件及格式是什么
	+ 根据自己项目的需要, 添加要忽略的文件名进 .gitignore
		* .gitignore 只忽略在其被添加以后的文件.
		* 之前的文件还是要删除的.
	+ 可使用GitHub 提供各编程语言的[模板][2]
		* [python模板][3]

基本上使用这个模板，再根据自己的实际情况增加一些特殊情况，比如 Ulysses 的特殊文件，比如某些wiki 项目根据 Markdwon 自动生成的一些 HTML 文件，比如一些无用的 图片/ 数据库文件等等 就可以啦。
### 上传前检查
- 查看文件夹里的内容
	+ 提交前 git diff HEAD 查看修改
		* 编辑文件完成后
		* git pull 更新本地仓库
		* git add . 添加暂存区
		* git diff/git diff HEAD 检查差别
		* git commit 提交信息,再次检查修改的文件.
- 确定都是要上传版本库的
	+ 如果不是, 删除之.
- 上传
	+ git push 推送
- 尽量避免上传后才发现需要删除

## 故事

## 小结
- 明确项目应该有的文件
- 明确不该有的文件
- 用. gitignore 工具忽略之


## 参考

- [版本仓库中应该放什么文件?在线收听\_Zoom.Quiet\_荔枝FM][4]
- [2.2 我们应该在仓库中存放什么文件 - 《版本控制之道——使用CVS》 - 免费试读 - book.csdn.net][5]     
- [Git-gitignore][6]
- [Ignoring files][7]
- [Some common .gitignore configurations][8]
- [忽略特殊文件 - 廖雪峰的官方网站][9]



[1]:	https://gist.github.com/octocat/9257657
[2]:	https://github.com/github/gitignore
[3]:	https://github.com/github/gitignore/blob/master/Python.gitignore
[4]:	https://www.lizhi.fm/3475110/2599671308701033478
[5]:	http://zqscm.qiniucdn.com/data/20080104214134/index.html
[6]:	https://git-scm.com/docs/gitignore
[7]:	https://help.github.com/articles/ignoring-files/
[8]:	https://gist.github.com/octocat/9257657
[9]:	http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013758404317281e54b6f5375640abbb11e67be4cd49e0000