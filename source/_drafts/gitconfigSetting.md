从 [大妈的配置](https://github.com/zoom-quiet/scm/blob/master/git/.gitconfig)中, 找到自己可以看懂的设置, 放到自己的配置里.

方法: 在 home 文件夹, 找到 .gitconfig 文件, 输入配置即可. 

我 .gitconfig目前是: 
```
[filter "lfs"]
smudge = git-lfs smudge %f
required = true
clean = git-lfs clean %f
[user]
name = liguanghe
email = liguanghe218317@gmail.com
[use]
name = liguanghe
email = liguanghe218317@gmail.com
[alias]
st = status
re = remote
ci = commit -m
co = checkout
br = branch
pu = push
pl = pull


f = fetch
fix = commit --amend

ls = ls-files
lt = ls-tree
cat = cat-file
l = log
l1 = log --pretty=oneline
lgs = log --graph --pretty=oneline --abbrev-commit
ll = log --graph --pretty=format:'%C(yellow)%h%Creset -%C(magenta)%d%Creset %s \n\t%cn %C(cyan)%cr%Creset' --date=relative --abbrev-commit

[color]
diff = auto
status = auto
branch = auto
interactive = auto
ui = true
pager = true

[color "branch"]()
current = yellow reverse
local = yellow
remote = green

[color "diff"]()
meta = yellow bold
frag = magenta bold
old = red bold
new = green bold
commit = yellow
whitespace = normal red

[color "status"]()
added = yellow
changed = green
untracked = cyan
updated = green
nobranch = magenta

# normal, black, red, green, yellow, blue, magenta, cyan, or white

```

大妈其他的内容还看不懂, 列表如下, 待以后用到再说. 
```
[difftool "sourcetree"]
    cmd = opendiff \"$LOCAL\" \"$REMOTE\"
    path = 
[mergetool "sourcetree"]
    cmd = /Applications/SourceTree.app/Contents/Resources/opendiff-w.sh \"$LOCAL\" \"$REMOTE\" -ancestor \"$BASE\" -merge \"$MERGED\"
    trustExitCode = true
[filter "hawser"]
    clean = git hawser clean %f
    smudge = git hawser smudge %f
    required = true
[filter "lfs"]
    clean = git-lfs clean %f
    smudge = git-lfs smudge %f
    required = true
[merge]
conflictstyle = diff3
```

## 延伸问题
- 原来我的 home 也已经在 git 下被管理了, 但是没有推到远程仓库. 因为太大了. 但其中的系统设置是应该推到远程仓库的. 
- 如何有选择的推呢? 如果把他们放进一个特别的文件夹, 系统就找不到这些配置文件啦. 如何优雅的解决?
- 大妈有一个 SCM 的远程仓库, 是如何配置的? 