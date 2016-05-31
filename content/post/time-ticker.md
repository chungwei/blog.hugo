+++
date = "2016-05-31T15:32:34+08:00"
draft = true
title = "Golang 实现定时器"
tags = ["golang", "ticker"]
categories = ["golang"]
highlight = true
+++

#### 背景  
定时任务的实现方式有多种，常用的是使用 `crontab`。最近的一个项目需要有执行定时（每5分钟）任务的需求，要求
不能使用 `crontab`，于是在程序中使用 `golang` 实现了。

#### crontab 实现
假设使用 `crontab`，会是这样的：  
```java
*/5 * * * * sh /path/to/script.sh 
```  
> <small>配置释义：分 时 日 月 周 命令</small>

#### golang 实现  
```java
import (
    "fmt"
    "time"
)
func main() {
    ticker := time.NewTicker(time.Second * time.Duration(300))

    for curTime := range ticker.C {
        fmt.Println(curTime)
        // doSth.
    }
}
```
