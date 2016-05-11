+++
date = "2016-05-11T10:49:46+08:00"
draft = true
title = "Expect 实现 Linux 远程登录"
tags = ["shell", "expect"]
categories = ["shell"]
highlight = true

+++

#### 背景

远程登录时工作中经常遇到的问题，之前的解决办法要么是老老实实手工输入密码，要么是两台机器建立
信任关系，但总感觉很麻烦，特别是机器多了，实在影响效率！  

最好的办法，是不需配置信任关系即可实现自动远程登录。

-----

#### 实现
使用 expect 即可实现，具体实现如下

```
#!/usr/bin/expect

# 设置超时时间为 3 秒
set timeout 3

# 设置要登录的主机 IP 地址
set host 10.10.38.232

# 设置以什么名字的用户登录
set name root
# 设置用户名的登录密码
set password 111222333

#spawn 一个 ssh 登录进程
spawn  ssh $host -l $name

# 等待响应，第一次登录往往会提示是否永久保存 RSA 到本机的 know hosts 列表中；等到回答后，在提示输出密码；之后就直接提示输入密码
expect {
   "(yes/no)?" {
       send "yes\n"
       expect "password:"
       send "$pasword\n"
   }
   "password:" {
       send "$password\n"
   }
}

# 这里使用了 interact 命令，使执行完程序后，用户可以在 $host 终端进行交互操作。
interact
```

-----

#### 参考文献
1. [Unix/Linux 系统自动化管理: 远程登录篇](https://www.ibm.com/developerworks/cn/aix/library/0909_jinjh_unixlogin/)

