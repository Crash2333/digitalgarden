---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/Kotlin/by/","tags":["kotlin/关键字"],"noteIcon":""}
---


通过使用 by 关键字，我们可以将接口的实现委托给另一个对象，从而避免了代码重复和继承的复杂性。

`Derived` 类可以通过将其所有公有成员都委托给指定对象来实现一个接口 `Base`：

```
interface Base {
    fun print()
}

class BaseImpl(val x: Int) : Base {
    override fun print() { print(x) }
}

class Derived(b: Base) : Base by b

fun main() {
    val b = BaseImpl(10)
    Derived(b).print()
}
```

`Derived` 的超类型列表中的 `by`-子句表示 `b` 将会在 `Derived` 中内部存储， 并且编译器将生成转发给 `b` 的所有 `Base` 的方法。
## 参考资料