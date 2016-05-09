+++
date = "2016-05-09T11:03:27+08:00"
draft = true
title = "Pexpect 实现 Linux 远程登录执行命令"
tags = ["python", "pexpect"]
categories = ["python"]
highlight = true

+++

#### 需求
最近接到一个小需求：检测目前在线的机器是否重装过系统。

> <small>由于涉及敏感信息，具体细节不描述，只记录大概思路和代码示例</small>

#### 解决思路
 - 连接、登录远程机器
 - 在远程机器执行命令
 - 获取执行结果
 - 处理执行结果

#### 代码示例
由于对 Shell 不太熟悉，采用了 Python Pexpect 实现，代码示例如下：

```python
import pexpect

def ssh_cmd(ip, passwd, cmd):
    ret = -1
    try:
        ssh = pexpect.spawn('ssh root@%s "%s"' % (ip, cmd))
        ssh.expect('password: ')
        ssh.sendline(passwd)
        r = ssh.read()
        print ssh.before
        ret = 0
    except Exception as ex:
        print 'ip=',ip,',ex=',ex
        ret = -1
    except pexpect.TIMEOUT:
        print 'ip=',ip,',TIMEOUT'
        ret = -2
    
    ssh.close() 
    return ret

cmds='ps -U root -u root -N | wc -l'
pwd='hhjjkkk'
try:
    f = open("./ip_list.txt")
    for line in f:
        ip = line.strip('\n')
        ret = ssh_cmd(ip, pwd, cmds)
        # proc ret
    f.close()
except Exception as ex:
    print ex
    f.close()
```