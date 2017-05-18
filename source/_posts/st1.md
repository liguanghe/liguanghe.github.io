
---
title:  Sublime Text / it’s all text / firefox
date: 2017/5/2 18:35:32
categories: 
- WriterEnvironment
tags: 
- firefox
- Sublime Text
- Ulysses

---
## 文本编辑器

- 从使用文本编辑器 Ulysses  + TextWangler( LPTHW 遗留至今），变成Ulysses  + Sublime Text
	- Q: 下载了 Sublime Text 为什么不用？
	- A：不知道研究大概需要多久，今天看大妈的展示：[openmindclub.qiniucdn.com/res/tr/tr\_MDP2py4w\_1\_w1cli\_rebuild.html]()(http://openmindclub.qiniucdn.com/res/tr/tr\_MDP2py4w\_1\_w1cli\_rebuild.html)，好像将命令行与代码编辑器合在一起了，看是不是这个 APP 搞定的。
	- Q: Ulysses 的好处？
	- A: 默认 .md 格式，
		- 显示三级目录，
		- 上传 icloud 云，
		- 字数统计，
		- 多种格式导出和预览，
		- 连接本地文件夹，
		- 随时修改随时自动保存，无需 command + s，
		- 随时在文件夹新建……这个编辑器已经成为我与网络对话的页面。自动延续编码。
	- Q: Ulysses 的坏处？
	- A: 其 markdown 语言符号与 github 略有不同。显示代码不那么方便。--- 容易连起来。不能显示表格。url 和 img 的格式也不对。编代码不能用它。
	- Q: 有什么编辑器可以兼顾 Ulysses 的好处，同时没有它的坏处？
	- A: 探索 Sublime text 看能否解决。
- Sublime Text 好像是个大坑，强大好用的同时，貌似教程都成本书了。
	- Q: 你对它的初步印象？
	- A: 要配置很多。三部分内容需要慢慢补足：基本功能、快捷键和插件。
	- Q: Sublime Text 可以取代 Ulysses 么？
	- A: 尝试中
		+ 显示三级目录: project - Add floder to project ; sidebar: command + k/b
		+ 上传云 变为都在 github 上对应的仓库.
	- Q: 安装 Sublime Text 的步骤？
	- A: 见官网. 补充，CML 下 command + shift + p 之后再输入 install……
	- Q: 插入链接?
	- A:  copy as markdown 插件（chrome 和 firefox 都有）。
	- Q: 插入图片？
	- A: 用iPic 图床，保存的图片格式即是 markdown 格式，command + v 即可。也可以用 command + option + k

## 浏览器
- 从使用一个浏览器：chrome 变成两个：chrome + firefox
	- Q: 什么时候用 chrome？什么时候用 firefox？
	- A: 目前，文本上传网页，使用 firefox，浏览和查询还是使用 chrome。
	- Q: 只想使用 chrome 浏览器的原因？
	- A: chrome 的插件 cVim 提供大量翻页等快捷键， adblock 屏蔽广告，copy as markdown 批量转化 url 为 md 格式，盘古之白添加空格，feeder 快速添加 RSS。如果添加 firefox 浏览器，这些插件是否也需添加？适用，没有的话是否需要替代品，需要时间配置。故，暂时只用 firefox 查阅 github 网页。firefox 有 vimfx ，与 cVim 的用法差不多，也有广告拦截插件。总共耗时10分钟。

	- Q: 如何下载 firefox？
	- A: 官网点击下载后，dmg文件打不开。更改方式：
$ brew install cask/firefox
下的很慢，两次都 incomplete。
更改方式：在玩转苹果下载破解版，成功安装。




## 插件
- it is all text
	- Q: 要不要用？
	- A：用。大妈在用，  已经查过 chrome 没有如此好用的插件。
	- Q: 尝试的时候有哪些发现？
	- A: 正在尝试。
	- Q: 图片链接格式？
	- A:稍后尝试。
	- Q: 能绑定两个编辑器么？
	- A: 不可以，只能绑定一个，我绑了Sublime Text，绕过 Ulysses 的设置。
	- Q: 安装这个插件会不会遇到坑？
	- A：会的。
		- 第一个坑就是，firefox 和 chrome 不一样，插件不会完全显示在右上角，这个插件就显示做拓展里，导致我不知道已经下载了。
		- 第二个坑，因为它不在右上角，也不像 chrome 点击使用。而是默认在右下角有一个小小的 edit。这个也可以设置位置，凭爱好。
		- 第三个坑，关联编辑器，大家都没写，好像很简单的样子。我用了 47 分钟。方法也确实简单，但是没人写呀。官方介绍和官方 Github 上都没有。方法如下：
			 - firefox - 附加组件管理器 - 拓展 - it's all text - 首选项 - 作者 - 框内的 text（Mac 内置编辑器名）改成 Sublime Text 即可：/Applications/Sublime Text.app
			 - 顺便，在这里改存储文件夹。这个文件夹我也想找个仓库放进去。方便管理。
	- Q: 还有哪些设置？
	- A: 都在首选项里，可以设置 hot key（快捷键），无需鼠标点击 edit。
	- Q: it's all text 的文件夹可否 git? 随时修改后，原本的对话框内容也变更。目前的方式是：点开 issue，找到文本，点击修改，点击 edit 跳转到 st, 回到浏览器，保存提交对话框。



## 快速调用 APP
- Manico
- delete terminal from dock，
- add firefox 
- add Sublime Text
- set shortcut

## 行为习惯
- 每天早上看 issue: 开 Chrome（option + c）-\> 开 firefox（opthin + x）
- 先看 issue 中的: 表明 assignee 的

