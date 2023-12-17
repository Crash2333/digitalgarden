---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/JetpackCompose/Column/","tags":["JetpackCompose/布局组件"],"noteIcon":""}
---

Column 是一个布局组件，它能够将里面的子项按照从上到下的顺序垂直排列。

```
Column(  
	modifier,
	horizontalArrangement,//子控件在水平方向上的排列方式（对齐方式）
	verticalAlignment, //子控件在垂直方向上的排列方式（对齐方式）
)
```

| 对齐方式 | 描述 |
| ----------------------------- | ------------------------------------------------ |
| `start` | 左对齐（默认） |
| `end` | 右对齐 |
| `centerHorizontally` | 水平居中对齐 |
| `top` | 上对齐 |
| `bottom` | 下对齐 | 
| `centerVertically` | 垂直居中对齐 |
| `baseline` | 基线对齐（与文本相关，适用于包含文本的情况） |
| `center` | 水平和垂直居中对齐 | 
| `start/end/bottom/top/center` | 根据内容自动选择对齐方式，优先级为：start > end > bottom > top > center |

![](https://i.imgur.com/WqLTfri.png)



## 参考资料