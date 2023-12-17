---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/Kotlin/when表达式/","tags":["kotlin/表达式"],"noteIcon":""}
---

`when` 将它的参数与所有的分支条件顺序比较，直到某个分支满足条件。
```
when (x) {
    1 -> print("x == 1")
    2 -> print("x == 2")
    else -> {
        print("x is neither 1 nor 2")
    }
}
```

作为表达式时，可以直接返回一个值
```
fun Request.getBody() =
    when (val response = executeRequest()) {
        is Success -> response.body
        is HttpError -> throw HttpException(response.status)
    }
```


## 参考资料