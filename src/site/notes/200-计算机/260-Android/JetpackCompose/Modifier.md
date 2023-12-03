---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/JetpackCompose/Modifier/","noteIcon":""}
---

在Jetpack Compose中，UI组件是通过函数来构建的，而`Modifier`则用于给这些函数传递参数，用于修改或调整UI组件的外观和行为。

`Modifier`是一个不可变的修饰符对象，可以通过链式调用方法来应用多个修饰符。每个方法都会返回一个新的`Modifier`对象，所以可以方便地进行组合和连续的修饰。



```
Modifier
    .padding(top = 6.dp) // 设置外边距Margin
    .clip(RoundedCornerShape(6.dp)) // 裁切圆角
    .padding(top = 6.dp) // 设置内边距，使用时注意调用顺序。第二次调用padding才是设置内边距
    .fillMaxWidth() // 填充最大宽度
    .fillMaxHeight() // 填充最大高度
    .fillMaxSize()//沾满屏幕
    .height(50.dp) // 设置高度
    .width(100.dp) // 设置宽度
    .background(Color.Blue) // 设置背景颜色
    .align(Alignment.Center) // 对齐方式
    .alpha(0.8f) // 设置透明度
    .border(2.dp, Color.Red) // 设置边框宽度和颜色
    .clickable { /* 点击事件处理 */ } // 添加点击事件
    .padding(start = 16.dp, end = 16.dp) // 设置起始边距
    .offset(y = 10.dp) // 设置偏移量
    .weight(1f) // 设置权重
    .rotate(45f) // 旋转
    .scale(1.2f) // 缩放
    .shadow(4.dp, shape = CircleShape) // 添加阴影
```


## 参考资料