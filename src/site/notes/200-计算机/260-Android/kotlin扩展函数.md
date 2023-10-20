---
dg-publish: true
date: 2023-09-27
tags:
  - Android
  - koltin
  - 扩展函数
---
## 使用范围
可以直接定义在`package`下面，这样该`package`下的类中都可以直接使用这个扩展函数（先创建一个类文件，再删除所有类相关的内容，最后定义拓展如下:）
```
package com.demo.demo  
  
import android.content.Context  
import androidx.datastore.preferences.preferencesDataStore  


val Context.dataStore by preferencesDataStore(name = "settings")


```

## 参考资料
[扩展 - Kotlin 语言中文站](https://www.kotlincn.net/docs/reference/extensions.html)