---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/JetpackCompose/Image/","tags":["JetpackCompose/基础组件"],"noteIcon":""}
---

图片组件

```
Image(  
    modifier = Modifier.fillMaxSize(),  
    painter = painterResource(id = R.mipmap.bg_live_room),  
    contentDescription = null,  
    contentScale = ContentScale.FillBounds,  
)
```


| 裁切类型 | 描述 |
| ---------------- | ---------------------------------------- |
| `FillBounds` | 将图像拉伸以填充可用空间，可能导致图像失真。 | 
| `FillWidth` | 将图像宽度拉伸以填充可用空间，高度保持原样，可能导致图像失真。 | 
| `FillHeight` | 将图像高度拉伸以填充可用空间，宽度保持原样，可能导致图像失真。 |
| `Inside` | 将图像缩放以适应可用空间，保持纵横比，可能会在边缘添加空白。 | 
| `Crop` | 将图像缩放以填充可用空间，保持纵横比，并且可能会裁剪超出可用空间的部分。 |
| `FillBoundsVertically` | 将图像高度拉伸以填充可用空间，宽度保持原样，可能导致图像失真。类似于`FillHeight`，但不会裁切图像。 |
| `FillBoundsHorizontally` | 将图像宽度拉伸以填充可用空间，高度保持原样，可能导致图像失真。类似于`FillWidth`，但不会裁切图像。 |
## 参考资料