---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/MVI/","tags":["Android/架构"],"noteIcon":""}
---


MVI 架构本质就是在 MVVM 架构的基础上进行了行为和数据上的 **约束**，把数据流变成了单向流动，把状态集中管理形成唯一可信数据源。

M：Model
V：View
I：Intent

- **Model**: 与其他MVVM中的Model不同的是，MVI的Model主要指UI状态（State）。当前界面展示的内容无非就是UI状态的一个快照：例如数据加载过程、控件位置等都是一种UI状态
- **View**: 与其他MVX中的View一致，可能是一个Activity、Fragment或者任意UI承载单元。MVI中的View通过订阅State的变化实现界面刷新
- **Intent**: 此Intent不是Activity的Intent，用户的任何操作都被包装成UserIntent后发送给Model进行数据请求



## 单向数据流

![](https://i.imgur.com/vXGHPjc.png)


## 参考资料

[尘埃落地 😛 遍历全网Android-MVI架构，学习总结一波 - 掘金](https://juejin.cn/post/7289662055183155235)
[Google 推荐使用 MVI 架构？卷起来了~ - 掘金](https://juejin.cn/post/7048980213811642382)

