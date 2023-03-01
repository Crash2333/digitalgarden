---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/SingleTask/","tags":["Android/Activity/启动模式"],"noteIcon":""}
---

## 栈内复用
只要 Activity 在一个任务栈中存在，那么多次启动此 Activity 都**不会重新创建**实例，并回调 **onNewIntent** 方法，此模式启动 Activity，系统首先会寻找是否 Activity 存在想要的任务栈。
如果不存在，就会重新创建一个任务栈，然后把创建好 Activity 的实例放到栈中。
如果存在，则将该实例之上的Activity全部清除（具有 clearTop 功能）