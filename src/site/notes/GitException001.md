---
{"dg-publish":true,"permalink":"/GitException001/","noteIcon":""}
---

# 无法ping通github域名，但是可以访问网页

今天照常使用[[600-应用科学/610-工具软件/Github\|Github]]备份资料，但是却迟迟`push`不上去。报错如下：
```
$ git push origin master
ssh: connect to host github.com port 22: Connection timed out
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.

```

看了下报错，连接超时。网络问题。于是我又[[ping\|ping]]了一下`github.com`。报文如下：
```
C:\Users\Alex>ping github.com

正在 Ping github.com [20.205.243.166] 具有 32 字节的数据:
请求超时。
请求超时。
请求超时。
请求超时。

20.205.243.166 的 Ping 统计信息:
    数据包: 已发送 = 4，已接收 = 0，丢失 = 4 (100% 丢失)，
```

但是github的网页又可以访问，基本上可以确定是[[DNS污染\|DNS污染]]了。

## 解决方案
### 1.获取域名实际IP
使用[[ipaddress\|ipaddress]]查询实际IP，也可以直接点击下面的链接：
[GitHub.com - GitHub: Let's build from here · GitHub](https://sites.ipaddress.com/github.com/)
[github.global.ssl.fastly.net](https://sites.ipaddress.com/github.global.ssl.fastly.net)

## 2.修改host文件
可以使用[[600-应用科学/610-工具软件/Optimizer\|Optimizer]]修改[[200-计算机/hosts文件\|hosts文件]]
```
140.82.112.3 github.com
151.101.193.194 github.global.ssl.fastly.net
```
![](https://i.imgur.com/PjpWvtE.png)

## 参考资料