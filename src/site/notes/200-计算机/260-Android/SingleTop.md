---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/SingleTop/","tags":["Android/Activity/启动模式"],"noteIcon":""}
---

## 栈顶复用
如果新 Activity 已经位于任务栈的栈顶，那么此 Activity 不会被重新创建，同时会回调 **onNewIntent** 方法，如果新 Activity 实例已经存在但不在栈顶，那么 Activity 依然会被重新创建。
## 用途
