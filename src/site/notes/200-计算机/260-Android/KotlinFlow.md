---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/KotlinFlow/","tags":["koltin","Android"],"noteIcon":""}
---


- [[200-计算机/260-Android/Kotlin/StateFlow\|StateFlow]]
- [[200-计算机/260-Android/Kotlin/SharedFlow\|SharedFlow]]

{ .block-language-dataview}
## SharedFlow
### 应用场景
1. 需要重放历史数据
2. 可以配置缓存
3. 需要重复发射/接收相同的值
## StateFlow
### 应用场景
>StateFlow 和LiveData很像，都是只维护一个值，旧的值过来就会将新值覆盖。  
适用于通知状态变化的场景，如下载进度。适用于只关注最新的值的变化。  
如果你熟悉LiveData，就可以理解为StateFlow基本可以做到替换LiveData功能。

## 参考资料
[这一次，让Kotlin Flow 操作符真正好用起来 - 掘金](https://juejin.cn/post/7226933611265605669)
[Kotlin Flow上手指南（一）基础使用 - 掘金](https://juejin.cn/post/7034379406730592269#heading-1)