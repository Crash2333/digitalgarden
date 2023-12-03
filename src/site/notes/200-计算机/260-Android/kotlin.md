---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/kotlin/","noteIcon":""}
---

## 关键字
- [[sealed\|sealed]]
- [[lazy\|lazy]]

{ .block-language-dataview}

[[lazy\|lazy]]

### 方法作为参数传递
```
fun setOnClickListener(l: (v: View) -> Unit)
```

#### Java调用kotlin函数，传Function作为参数

java里面没有Unit的概念，我们定义返回Unit类型。
那么java的的写法就是返回`null`，这回直接导致空指针。
此时改成返回int类型的值

```
foo(() -> {
    // Here should be a code you need
    return null;//返回Unit类型
});

foo(() -> {
    // Here should be a code you need
    return 0; //返回int类型
});

```


[[200-计算机/260-Android/谱写 Kotlin 面试指南三部曲 - 基础篇\|谱写 Kotlin 面试指南三部曲 - 基础篇]]
[[200-计算机/260-Android/谱写Kotlin面试指南三部曲-协程篇 - 掘金\|谱写Kotlin面试指南三部曲-协程篇 - 掘金]]
[[200-计算机/260-Android/谱写Kotlin面试指南三部曲-Flow篇 - 掘金\|谱写Kotlin面试指南三部曲-Flow篇 - 掘金]]
## 参考资料
[Kotlin 语言中文站](https://www.kotlincn.net/)
[关于本书 · Kotlin 官方文档 中文版](https://book.kotlincn.net/)