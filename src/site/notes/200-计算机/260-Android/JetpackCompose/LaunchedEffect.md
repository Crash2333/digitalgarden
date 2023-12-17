---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/JetpackCompose/LaunchedEffect/","tags":["JetpackCompose/EffectAPI"],"noteIcon":""}
---

LaunchedEffect 用于在可组合函数中安全地调用协程。
当 LaunchedEffect 进入组合时，它会通过 CoroutineScope.launch 启动一个协程，并将开发者声明的代码块作为参数传递给该协程进行执行。
当 LaunchedEffect 退出组合时，启动的协程也会被取消，从而保证了安全性。同时 LaunchedEffect 也支持和多个 key 进行绑定，当 key 发生变化时就会取消现有协程并重新启动


## 参考资料
[Compose 中的附带效应 - 掘金](https://juejin.cn/post/7244788137410953271?searchId=20231208102047E7DD3AB70320D076F2EF)
[学不动也要学，Jetpack Compose 写一个 IM APP（二） - 掘金](https://juejin.cn/post/7028397244894330917?searchId=20231208102047E7DD3AB70320D076F2EF#heading-5)