---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/Kotlin/sealed/","tags":["kotlin/关键字"],"noteIcon":""}
---

用于声明密封类（sealed class）。密封类是一种特殊的抽象类，用于限制类的继承层级。密封类可以有一些子类，但这些子类必须被声明在密封类的同一个文件中。


以下是密封类的一些常见用途：

1. **表达状态**：密封类可以用于表达有限状态机的不同状态。每个子类可以代表一个特定的状态，而密封类本身可以用作状态的容器。
    
2. **模式匹配**：密封类可以与 `when` 表达式结合使用，用于模式匹配。`when` 表达式允许你使用密封类的子类作为分支条件，这样你可以根据不同的子类来执行相应的逻辑。
    
3. **类型安全**：密封类提供了一种类型安全的方式来表示有限的、可枚举的类型集合。编译器可以在编译时检查 `when` 表达式是否处理了所有可能的子类情况，从而提供更好的编译时安全性。


```
sealed class Result
data class Success(val data: String) : Result()
data class Error(val message: String) : Result()

fun processResult(result: Result) {
    when (result) {
        is Success -> println("Success: ${result.data}")
        is Error -> println("Error: ${result.message}")
    }
}

val successResult = Success("Data received")
val errorResult = Error("Something went wrong")

processResult(successResult) // 输出：Success: Data received
processResult(errorResult) // 输出：Error: Something went wrong
```

## 参考资料

