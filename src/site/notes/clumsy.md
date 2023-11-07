---
{"dg-publish":true,"permalink":"/clumsy/","tags":["Android/Debug","弱网模拟"],"noteIcon":""}
---


一个弱网测试软件，绿色版(需管理员权限)，支持Win7/Win8/Win8.1/Win10，可以模拟网络的丢包，延迟，重复，乱序，损坏（数据包）等情况。可以做到针对性得模拟用户在弱网条件（如2G网络或是连上了一个信号很差的Wi-Fi等）下的使用体验，做到软件对网络恶劣条件下的debug。

![](https://i.imgur.com/q0VcpNl.jpg)


## 用法
一般需要搭配[[AGB\|AGB]]使用。
1. 手机关闭WiFi和移动网络
2. 打开Android手机的开发者模式和USB调试开关
3. USB连接电脑
4. 使用[[AGB\|AGB]]，让手机使用电脑的网络
5. clumsy来控制指定IP的延时、丢包的配置

![](https://i.imgur.com/VweIPtO.png)



![](https://i.imgur.com/nxbIJRW.png)





## 参考资料
[Clumsy——弱网测试工具（介绍和简单上手） - Gulut's Blog](https://gulut.github.io/gulut-blog/post1/2020/09/20/2020-09-20-clumsy-a-bad-net-test-tool/)
[jagt/clumsy: clumsy makes your network condition on Windows significantly worse, but in a controlled and interactive manner.](https://github.com/jagt/clumsy)

