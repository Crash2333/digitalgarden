---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/Kotlin/is/","tags":["kotlin/关键字"],"noteIcon":""}
---

## is 与 !is 操作符

使用 `is` 操作符或其否定形式 `!is` 在运行时检测对象是否符合给定类型：

```
if (obj is String) {
    print(obj.length)
}

if (obj !is String) { // 与 !(obj is String) 相同
    print("Not a String")
} else {
    print(obj.length)
}
```

## 智能转换

大多数场景都不需要在 Kotlin 中使用[[200-计算机/260-Android/Kotlin/as\|显式转换]]操作符，

智能转换用于 [`when` 表达式](https://book.kotlincn.net/text/control-flow.html#when-%E8%A1%A8%E8%BE%BE%E5%BC%8F) 和 [`while` 循环](https://book.kotlincn.net/text/control-flow.html#while-%E5%BE%AA%E7%8E%AF) 也一样：

```
when (x) {
    is Int -> print(x + 1)
    is String -> print(x.length + 1)
    is IntArray -> print(x.sum())
}
```


## 参考资料