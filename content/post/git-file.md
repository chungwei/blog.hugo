+++
date = "2016-05-14T09:10:58+08:00"
draft = true
title = "Git 笔记1 —文件管理篇"
tags = ["git"]
categories = ["git"]
highlight = true

+++

关于`Git`的介绍实在太多，Google 或 百度一下 就有，不再介绍。  

个人接触 `Git` 已经差不多三年，第一次使用`Git`作为版本管理工具时，网上查查资料也能使用，但习惯了`SVN`的客户端，
感觉学习`Git`的曲线很陡，很多命令总是很容易搞混或忘记，后来换工作又切回`SVN`了。直到最近加到新的Team，完全使用`Git`，
经过不断请教和学习，该把成果整理归纳一下，以备今后查询。  

#### 查看仓库状态
使用场景：提交之前，先看一下本次 修改、删除、新增 了哪些文件
````
git status
````

#### 查看变更前后的差异
````
git diff [/path/to/file]  # 可指定只看某文件，删除和新增文件不会显示
````

#### 提交文件
使用场景：提交仓库的变更
````
git add /path/to/file1 [/path/to/file2...]  # 提交到本地暂存区，可同时提交多个文件，新增和修改文件命令相同
git commit -m '提交文件'  # 保存暂存区的变更到当前分支
git push origin branch-name  # 把变更文件推到当前分支对应的远程仓库
````

#### 删除文件
````
git rm /path/to/file
git commit -m '删除文件'
git push origin branch-name
````
