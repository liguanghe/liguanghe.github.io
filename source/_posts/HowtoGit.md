---
title: First Step to Git
date: 2017/7/30 09:25:32
categories: 
- github
tags:
- git 
- github
- english
- study
- tutorial
---


## What is Git
I know you get in touch with Git from Github, before it, you should know Git first. 
- A document manage tool
Solve document version problems. You needn't contorl version by named your document, or make a list of it. Git helps you do that, everytime you change the doc and save it, git will git this version of doc a special serial number. This number will help you find any version.
- A floder with git named local repository
`$ cd floder_name`
When you do that, means you use Command Line to tell you computer, come in to a floder, you want to do something in this floder, like add or delete documents. 

`$ git init`
When you do that in you command line, you use git to control this floder, a floder with git has a special name-- repository.
`$ git add .`
After any change you do in repository, you should do that to tell git you made change. 
`$ git cimmit -m 'note of what you have changed'`
Tell git what you have changed, it's a note, git will connect your note to the special version number. 
`$ git log`
Ask git to give you version list. You can see all version number with notes(you just add it.)

## Cloud backup your doc and version by github
Local repository is easy be damaged by phyical problems. Put all doc and version is a safe way.More important, you can cooperiate with fellows for work on line.

The basic function of Github is a cloud backup space based by Git. It's quiet easy to use. 
- build a remote repository
	- clink button on you github: you github profile - repository - new repository 
	- named this repository as you local floder(local repository)
- connect remote repository to local repository
	+ after you build a remote repository in Github, it will give you command, like: git remote add http://github .........git
	+ copy that command and paste it to your terminal
		* notice: you are still in this floder (cd floder\_name)
		* `$ git remote add http://github......git`
	+ check weather you have connect the local to remote
	`$ git remote -v`
	+ push you local version to remote at first time
	`$ git push origin master`
		* master is main branch, we will talk about branch later. 
- if terminal don't say fatal or wrong, you are good. 
	 
## Keep good communiction with remote repository
`$ cd floder`
go in to you repository
`$ git stutas`
check your repository sytutas, have you told all the changes to git? if not, git will tell you to git add . and git commit.
`$ git pl`
get version and data from remote repository, don't worry it will cover your local data, they will be merged. 
do this first, be sure you have the news with other fellows. They may push sth in to the same repository, which you should know.
`$ git add .`
`$ git cimmit -m ''` 
`$ git push`
push you local data to remote.
`$ git stutas`
check it again.

---- 
next tutorial will be: you own branch