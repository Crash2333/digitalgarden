---
dg-publish: true
date: 2023-09-25
tags:
  - koltin
  - Log/TAG
  - Logcat
---
```
/**
 * extension function to provide TAG value
 */
val Any.TAG: String
    get() {
        return if (!javaClass.isAnonymousClass) {
            val name = javaClass.simpleName
            if (name.length <= 23) name else name.substring(0, 23)// first 23 chars
        } else {
            val name = javaClass.name
            if (name.length <= 23) name else name.substring(name.length - 23, name.length)// last 23 chars
        }
    }
```


## 参考资料
[在Kotlin中定义log TAG常量的最佳方式是什么？](https://www.qiniu.com/qfans/qnso-45841067)
[java - What is the best way to define log TAG constant in Kotlin? - Stack Overflow](https://stackoverflow.com/questions/45841067/what-is-the-best-way-to-define-log-tag-constant-in-kotlin/55915831#55915831)
