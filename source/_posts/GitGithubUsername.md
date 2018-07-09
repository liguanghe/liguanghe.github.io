---
title:  Changing Github Username
date: 2017/5/11 18:35:32
categories: 
- github


tags: 
- git


---
更改用户名
[Changing your GitHub username - User Documentation][1]

哪些变了, 哪些没变
[What happens when I change my username? - User Documentation][2]

变更远程连接
[Changing a remote's URL - User Documentation]()(https://help.github.com/articles/changing-a-remote-s-url/)

## What happens when I change my username?

When you change your GitHub username, most references to your repositories under the old username automatically change to the new username. 
改用户名后, 你仓库的大部分说明自动变成新的用户名.

However, some links to your profile won't automatically redirect. 
但是, 一些你页面的链接不能自动重定向.

Commits made with your username@users.noreply.github.com address will no longer be associated with your account.
用 你的 username@users.noreply.github.com 地址提交, 将不再和你的账户联合.

## Repository references
仓库简要

After you change your username, GitHub will automatically redirect references to your repositories.
更改用户名后, 自动重定向到你的仓库

• Web links to your existing repositories will continue to work. This can take a few minutes to complete after you initiate the change.
网络链接到你已经存在的仓库, 将继续工作. 在你变更后需要一些时间.

• Command line pushes from your local repository clones to the old remote tracking URLs will continue to work.
你从旧的远程仓库克隆到本地的仓库, 命令行还可以继续推送.

However, after changing your username, your old username will become available for anyone else to claim. 
任何人可以链接你的旧用户名.

If the new owner of your old username creates a repository with the same name as your repository, that will override the redirect entry and your redirect will stop working.
如果新的拥有者用你的旧用户名创建仓库, 将优先重定向入口,你的重定向将不能工作.

 Because of this possibility, we recommend you update all existing remote repository URLs after changing your username.
防患于未然, 建议你**升级所有已经存在的远程仓库 urls.**

GitHub cannot set up redirects for:
将不为以下建议重定向:
• @mentions using your old username
提及你旧用户名的@
• Links to Gists with your old username
就要户名的链接要点
## Links to your previous profile page
预先页面链接
After changing your username, links to your previous profile page, such as https://github.com/previoususername, will return a 404 error. 
github 主页 将显示错误

We recommend **updating any links to your GitHub account from elsewhere, such as your LinkedIn or Twitter profile.**
建议升级放在其他地方的主页链接

## Your Git commits

If your previous Git commits were correctly attributed to your account and displayed in your contributions graph, and they were made with an email address that is not your username@users.noreply.github.com address, they will continue to be correctly attributed to your new username.
预先 git 提交 正确的属于你的账户, 在你的贡献表展示, 被一个邮件地址生成, 但有不是你的 username@users.noreply.github.com 地址, 他们将继续属于你的新用户名.

However, if your previous commits were made with your username@users.noreply.github.com address (because you chose to keep your email address private or set it as your Git email address) those commits will no longer be associated with your account or displayed on your contributions graph after changing your username.
但是, 如果你预先 推送属于这个地址, (因为你选择让你的地址是有, 或者用你 git email address), 哪些推送将不能属于你的账户. 

Further reading
• "Changing a remote's URL"
• "Why are my commits linked to the wrong user?"
• 
Article versions
• GitHub.com
• GitHub Enterprise 2.9 
• GitHub Enterprise 2.8 
• GitHub Enterprise 2.7 


© 2017 GitHub Inc. All rights reserved. 
• Terms of Service
• Privacy
• Security
• Support

## github pages
- link will change to new automatically
- repository name will not change automatically
- you should change it
- then you can use the newname to open link

## branch
- change old branch name to new one
[branch - git: renaming branches remotely? - Stack Overflow][4]

## 行动
1. change username
2.  update remote url
3. update links at other web(like blog)
4. 告诉一休/大妈等关键人物

[1]:	https://help.github.com/articles/changing-your-github-username/
[2]:	https://help.github.com/articles/what-happens-when-i-change-my-username/
[4]:	http://stackoverflow.com/questions/4753888/git-renaming-branches-remotely