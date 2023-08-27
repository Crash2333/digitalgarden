---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/Service/","tags":["Android/四大组件"],"noteIcon":""}
---

Service是一个应用程序组件，它能够在后台执行一些耗时较长的操作，并且不提供用户界面。
## 生命周期
![Imgur](https://imgur.com/7zo5TK9.png)

## 启动方式
- [[200-计算机/260-Android/startService\|startService]]
- [[200-计算机/260-Android/bindService\|bindService]]

## 使用方法

## Service种类划分
### 前台服务

前台服务是指那些经常会被用户关注的服务，因此内存过低时它不会成为被杀的对象。

前台服务必须提供一个**状态栏通知**，并会置于“正在进行的”（“Ongoing”）组之下。这意味着只有在**服务被终止**或从前台移除之后，此通知才能被解除。

例如，用服务来播放音乐的播放器就应该运行在前台，因为用户会清楚地知晓它的运行情况。 状态栏通知可能会标明当前播放的歌曲，并允许用户启动一个activity来与播放器进行交互。
### 后台服务
就是我们经常使用的服务

### 本地服务
用于应用程序内部，实现一些耗时任务，并不占用应用程序比如Activity所属线程，而是单开线程后台执行。 　　
调用Context.startService()启动，调用Context.stopService()结束。在内部可以调用Service.stopSelf() 或 Service.stopSelfResult()来自己停止。
### 远程服务
用于Android系统内部的应用程序之间，可被其他应用程序复用。
例如车辆设置调用CarService方法，控制车辆功能。
## Service 与 Thread 的区别

服务仅仅是一个组件，即使用户不再与你的应用程序发生交互，它仍然能在后台运行。因此，应该只在需要时才创建一个服务。
如果你需要在**主线程之外**执行一些工作，但仅当用户与你的应用程序**交互时才会用到**，那你应该创建一个新的线程而不是创建服务。
