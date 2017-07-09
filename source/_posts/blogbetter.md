---
title:  博客优化
date: 2017/3/22 18:35:32
categories: 
- WriterEnvironment

---

## Add comments function
### disqus
[disqus 官网][1]
填写博客网站后，会给你一个short name 

### 在blog修改
站点配置文件和主题配置文件 添加disqus：short name
[hexo-next 主题下添加][2]

## Attention
- npm install     in  file

## Add visit times info
[http://theme-next.iissnan.com/getting-started.html][3]
[https://notes.wanghao.work/2015-10-21-%E4%B8%BANexT%E4%B8%BB%E9%A2%98%E6%B7%BB%E5%8A%A0%E6%96%87%E7%AB%A0%E9%98%85%E8%AF%BB%E9%87%8F%E7%BB%9F%E8%AE%A1%E5%8A%9F%E8%83%BD.html#%E9%85%8D%E7%BD%AELeanCloud][4]
[https://leancloud.cn/dashboard/data.html?appid=9GEqF7BQvsUPba1qXT9WOrNM-gzGzoHsz#/Counter][5]

themes - next - config.yml - leancloud - enable: true - id - key

## 只在创作页面发布打赏功能，晚点添加

## 内容分享
jia this 
themes - next - config.yml - jiathis（去掉#）
[http://theme-next.iissnan.com/third-party-services.html][6]

## 互动
我想到的三个方式：
- 填写你的邮箱，更新发到你的邮箱。
[如何添加邮箱订阅功能][7]
[15种增加订阅的方法][8]
[hexo添加订阅功能][9]
- 关注我的公众号，更新推送。
这里，每次更新公众号都需要管理员微信扫二维码才能登录，目前还没有想到自动的办法。
- 点击 RSS 关注，如果你有RSS阅读器的话。
RSS 就相当于一个列表，你关注的人列表，有新消息也会发送给你。是早于Facebook、Twitter和微信微博的存在。
后续会添加这个在页面。

## 独立博客属于？
建一个独立博客，多少接触到了一些软件知识，这些知识属于什么呢？是前端开发么？如果想更改布局或者优化，想对此多了解一些。

后续会研究这个内容。

## 添加域名
- 到godaddy.com 买域名
- 在仓库 setting 改 custom domain
- 在godaddy.com 域名管理页面添加 liguanghe.github.io
- 在godaddy.com 域名管理添加 A ( @ point to : github 的官方 Ip address: 192… ) ,
	- [https://help.github.com/articles/setting-up-an-apex-domain/]()(https://help.github.com/articles/setting-up-an-apex-domain/)
- 等待大概一天, 部署成功

## 嵌入视频
- 方法1：
``` <iframe 
    height=438 width=680 
    src="https://v.qq.com/x/page/m05035g7hf3.html" 
    frameborder=0 allowfullscreen>
</iframe>
```
## 设置后无反应
$ hexo clean

[1]:	https://disqus.com/profile/signup/intent/
[2]:	https://github.com/iissnan/hexo-theme-next/wiki/%E8%AE%BE%E7%BD%AE%E5%A4%9A%E8%AF%B4-DISQUS
[3]:	http://theme-next.iissnan.com/getting-started.html
[4]:	https://notes.wanghao.work/2015-10-21-%E4%B8%BANexT%E4%B8%BB%E9%A2%98%E6%B7%BB%E5%8A%A0%E6%96%87%E7%AB%A0%E9%98%85%E8%AF%BB%E9%87%8F%E7%BB%9F%E8%AE%A1%E5%8A%9F%E8%83%BD.html#%E9%85%8D%E7%BD%AELeanCloud
[5]:	https://leancloud.cn/dashboard/data.html?appid=9GEqF7BQvsUPba1qXT9WOrNM-gzGzoHsz#/Counter
[6]:	http://theme-next.iissnan.com/third-party-services.html
[7]:	http://www.race604.com/add-email-subscribe/
[8]:	https://blog.benchmarkemail.com/cn/15-ways-grow-email-list-2017/
[9]:	http://whatbeg.com/2017/03/23/addemailsubscribe.html
