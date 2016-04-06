+++
date = "2016-04-05T15:21:49+08:00"
draft = true
title = "使用 Hugo Github 搭建博客"
categories = ["hugo"]

+++

,使用 Hugo Github 搭建博客,使用 Hugo Github 搭建博客,使用 Hugo Github 搭建博客,使用 Hugo Github 搭建博客,使用 Hugo Github 搭建博客,使用 Hugo Github 搭建博客,使用 Hugo Github 搭建博客,使用 Hugo Github 搭建博客,使用 Hugo Github 搭建博客,使用 Hugo Github 搭建博客,使用 Hugo Github 搭建博客,使用 Hugo Github 搭建博客,使用 Hugo Github 搭建博客,使用 Hugo Github 搭建博客,使用 Hugo Github 搭建博客,使用 Hugo Github 搭建博客,使用 Hugo Github 搭建博客,使用 Hugo Github 搭建博客
#### 环境介绍：
Mac OSX 10.11.1

#### 步骤如下：
在github创建两个仓库 blog.hugo 和 chungwei.github.io

安装Hugo
```shell
brew install hugo
```

使用 Hugo 创建站点
```shell
cd ~/www
hugo new site blog.hugo && cd blog.hugo/
```

本地仓库和远程仓库关联
```shell
git init && git remote add origin https://github.com/chungwei/blog.hugo.git
```

创建页面
```shell
hugo new about.md
```

下载站点主题
```shell
git submodule add https://github.com/dim0627/hugo_theme_beg.git themes/beg
```

启动服务
```shell
hugo server -w --theme=beg --buildDrafts
```

浏览器访问 http://localhost:1313/
![This is an image](/img/BD22C57D-5746-4CBC-AE4B-A62C87D8DD80.png)

下载站点主题
```shell
git submodule add https://github.com/dim0627/hugo_theme_beg.git themes/beg
```

下载站点主题
```shell
git submodule add https://github.com/dim0627/hugo_theme_beg.git themes/beg
```


