---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/Exception/ComposeException002/","tags":["JetpackCompose/Exception"],"noteIcon":""}
---

## 禁用点击事件水波纹
通常在`clickable`中处理点击逻辑时，控件会自带一个水波纹的点击效果。
但是产品要求使用别的点击效果，那我们就要想办法禁用了。
## 解决方案
在手势回调中处理点击事件。代码如下：

```
Box(  
    modifier = Modifier  
        //禁用水波纹  
        .pointerInput(Unit) {  
            detectTapGestures(onTap = {  
  
            })  
        }  
        .fillMaxSize()  
)
```


## 参考资料

[android - How to disable ripple effect when clicking in Jetpack Compose - Stack Overflow](https://stackoverflow.com/questions/66703448/how-to-disable-ripple-effect-when-clicking-in-jetpack-compose)