+++
date = "2016-06-14T22:05:52+08:00"
draft = true
title = "Python 升级"
tags = ["python"]
categories = ["python"]
highlight = true

+++

#### 系统基本信息
````
cat /proc/version
````
<img src="/img/linuxver.png" style="width:100%">


````
cat /etc/issue
````
<img src="/img/linuxiss.png" style="width:100%">

#### 备份
安装之前备份旧版本（python2.6.6），因为 `yum` 还会用到该版本
````
which python
mv /usr/bin/python /usr/bin/python2.6.6
````

#### 安装
````
wget https://www.python.org/ftp/python/2.7.11/Python-2.7.11.tgz
tar -zxvf Python-2.7.11.tgz
cd Python-2.7.11
./configure
make
make install
````

#### 创建新版本软链
````
which python2.7
ln -s /usr/local/bin/python2.7 /usr/bin/python
````

#### 更改 yum 配置
这时候假如使用 `yum`，便会报错，因为是 `python` 的版本问题，应进行如下修改
````
vim /usr/bin/yum
// 修改第一行
#!/usr/bin/python
// 为
#!/usr/bin/python2.6.6
````



