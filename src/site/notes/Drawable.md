---
{"dg-publish":true,"permalink":"/Drawable/","tags":["Android/Drawable"],"noteIcon":""}
---


## ShapeDrawable
```
<shape xmlns:android="http://schemas.android.com/apk/res/android"  
    android:shape="line">  
    <corners android:radius="50dp"/>  
    <solid android:color="#ffffff"/>  
    <stroke android:color="#000000"/>  
  
</shape>
```
### 常用属性
#### shape
表示图形的形状，如下四个选项：

1. `rectangle`(矩形)
2. `oval`(椭圆)
3. `line`(横线)
4. `ring`(圆环)

#### corners
表示shape的四个角的角度，只适用于矩形shape

- android:`radius` 为四个角设置相同的角度
- android:`topLeftRadius` 设置左上角角度
- android:`bottomLeftRadius` 设置左下角角度
- android:`bottomRightRadius` 设定右下角的角度

#### solid
表示**纯色填充**
#### gradient
用于表示渐变效果，与 [[Drawable#solid\|solid]]标签互斥(其表示纯色填充)

- android:`angle` 渐变的角度，默认为0,其值必须为45的倍数, **0表示从左向右，90表示从下到上**
- android:`centerX` 渐变中心点的横坐标
- android:`centerY` 渐变中心点纵坐标
- android:`startColor` 渐变的起始色
- android:`centerColor` 渐变的中间点
- android:`endColor` 渐变的结束色
- android:`gradientRadius` 渐变半径,仅当android:type=“radial”时有效
- android:`useLevel` 是否使用等级区分，在 `StateListDrawable` 时有效，默认 **false**
- android:`type` 渐变类型，`linear`(线性渐变)、`radial`(径向渐变)、`sweep`
#### stroke 
  用于设置描边

- android:`width` 描边宽度
- android:`color` 描边颜色
- android:`dashWidth` 描边虚线时的宽度
- android:`dashGap` 描边虚线时的间隔










## LayerDrawable

```
<layer-list xmlns:android="http://schemas.android.com/apk/res/android"  
    android:shape="line">  
    <item android:drawable="@drawable/a1" />  
    
    <item        
	    android:drawable="@drawable/a1"  
        android:top="1dp" />  
  
    <item        
	    android:bottom="2dp"  
        android:drawable="@drawable/a1" />  
  
</layer-list>
```

就是`layer-list`,可以理解为图层列表（类似FrameLayout的叠加效果）。一般常见于需要多个 `Drawable` **叠加** 摆放效果时使用。

#### 实现效果
1. 单边线
2. 双边线
3. 阴影
4. 图片叠加
5. 旋转叠加


## 参考资料
[由浅入深、详解Android中Drawable的那些事](https://juejin.cn/post/7148630011010875422#comment)
[layer-list -- layer-list的基本使用介绍_](https://blog.csdn.net/north1989/article/details/53485729)
