---
layout: post
title: Git之.gitignore文件
date: 2016-11-22
categories: 
tags: [记录]
description: Git之.gitignore文件
---
#####.gitignore忽略文件
 现在使用Android Studio 创建项目时会自动创建.gitignore文件
 
> *.iml

>.gradle

>/local.properties

>/.idea/workspace.xml

>/.idea/libraries

>.DS_Store
>
>/build

>/captures

默认情况下,就是此配置,那么这些配置都是什么意思呢?查阅了一些博客和文章记录在此.

- .gitignore文件对其所在的目录及所在目录的全部子目录均有效

- 文件的每一行保存一个匹配规则

- *.iml     忽略所有iml结尾的文件

- .gradle 忽略文件及子目录所有文件

- local.properties   忽略local.properties文件

- /build   忽略当前目录下的build文件和和目录,自目录的不忽略

- *.[ab]   忽略.a和.b结尾的文件

- !hi.a 除hi.a文件以外

- abc/  只忽略abc目录,但不忽略abc文件

- !abc/ 不忽略abc目录

- abc 忽略abc文件



参考学习文章 : [Git之忽略文件(ignore file)](http://blog.csdn.net/benkaoya/article/details/7932370)
