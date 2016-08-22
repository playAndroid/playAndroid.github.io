---
layout: post
title: git命令使用记录
date: 2016-08-19
categories: 
tags: [记录]
description: git命令学习使用记录
---
####git init
> 初始化git仓库(repository)

####git add 文件名
>将文件添加到暂存区(stage)

#### git add .
>将所有新增以及修改文件添加到暂存区

####git commit -m "本次提交说明"
>将暂存区所有文件提交到仓库当前分支

####git status
>显示仓库状态

####git show
>查看最后一个commit的修改

####git log
>显示提交日志

####git push origin master
>推送最新修改到远程master分支

####git pull
>拉取远程仓库最新修改

####git clone 仓库地址
>克隆一个仓库到本地

####git branch
>列出本地分支

####git checkout xx
>切换到xx分支

####git tag v1.0
>将当前代码标记为v1.0标签

####git checkout v1.0
>切换到v1.0标签时的代码

####git config -global user.name "你的名字"
>更改提交用户名

####git config -global user.email "你的邮箱"
>更改提交时的邮箱



###学习参考资料
[从0开始学习 GitHub 系列汇总](http://stormzhang.com/github/2016/06/19/learn-github-from-zero-summary/)
[Git 命令总结](http://24suixinsuoyu.com/2016/07/27/Git-%E5%91%BD%E4%BB%A4%E6%80%BB%E7%BB%93/)
[版本控制-git系列](http://blog.csdn.net/data_hlk/article/details/50864847)