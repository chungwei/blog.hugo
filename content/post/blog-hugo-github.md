+++
date = "2016-04-25T13:43:49+08:00"
draft = true
title = "使用 Hugo Github 搭建博客"
tags = ["github", "hugo"]
categories = ["tutorial"]
highlight = true

+++

<br>

本文主要介绍如何使用`Hugo`在`Github`搭建免费的个人博客，关于`Hugo`
可在其[官网](https://gohugo.io)上进一步了解。  

#### 环境介绍
* Mac OSX 10.11.1  
* 项目根路径 ~/www/

---

#### 搭建步骤
1. 在`Github`创建两个仓库，比如`blog.hugo`和`chungwei.github.io`  

1. 安装`Hugo`
```shell
brew install hugo
```

1. 使用`Hugo`创建站点
```shell
cd ~/www
hugo new site blog.hugo
cd blog.hugo/
```

1. 本地仓库和远程仓库关联
```
git init
git remote add origin https://github.com/your-name/blog.hugo.git
```

1. 创建页面
```shell
hugo new about.md
```

1. 下载站点主题
```shell
git submodule add https://github.com/dim0627/hugo_theme_beg.git themes/beg
```

1. 启动服务
```shell
hugo server -w --theme=beg --buildDrafts
```

1. 浏览器访问 http://localhost:1313/  
看到如下图页面，说明本地搭建博客已经没问题了。接下来就是如何挂到 `Github`上。
<img src="/img/demo.png" style="width:100%">

1. 提交`blog.hugo` 到远程仓库
```shell
git add -A
git commit -m 'commit demo'
git push origin master
```
1. 生成站点页面  
执行完命令，目录下会多一个 `public` 目录，要发布到 `Github` 的博客页面就在该目录中
```shell
rm -rf public
hugo --buildDrafts -t beg
```

1. 检出博客页面远程仓库
```shell
cd ~/www
git clone https://github.com/your-name/chungwei.github.io.git
cd chungwei.github.io/
```

1. 复制本地博客页面到该仓库
```shell
cp -R ~/www/blog.hugo/public/* .
```

1. 提交 `chungwei.github.io` 到远程仓库
```shell
git add -A
git commit -m 'ci demo'
git push origin master
```
1. 浏览器访问 http://chungwei.github.io/  
看到 `步骤8`页面，说明博客搭建成功。

    >
*<small>可能存在这样的情况：  
访问 `http://chungwei.github.io 出现404`，但访问 `http://chungwei.github.io/about`
是正常的，原因是仓库`chungwei.github.io缺少README.md`，创建该文件即可解决
</small>*

---

#### 安装插件

1. **评论功能**  
国外的有 [disqus](https://disqus.com/)，国内的有 [多说](http://duoshuo.com/)，
因为多说支持国内第三方账号登录，下面简单说一下如何配置：
 - 注册多说账号，按照引导一步步往下走即可；
 - 完成后，提示将一段 js 代码引入页面；
 - 将 js 代码放在 `layout/partials/duoshuo.html` 中；
 - 在 `config.toml` 的 `[params]` 节点下加入配置项 `duoshuoShortname = "your-blog-name"`，
   注意：`your-blog-name` 是在注册多说账号时填的名称；
 - 在页面中引用 `layout/partials/duoshuo.html`

        ```shell
{{ if .Site.Params.duoshuoShortname }}
    {{ partial "duoshuo.html" . }}
{{ end }}
```

1. **代码高亮**  
在文件头部设置变量 `highlight = true` 即可。

    > *<small>之前尝试在 `config.toml` 文件中设置，都不生效</small>*

---

#### 参考资料

1. [Hugo官网文档](https://gohugo.io/overview/quickstart/)
1. [使用Hugo搭建静态站点](http://tonybai.com/2015/09/23/intro-of-gohugo/)