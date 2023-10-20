---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/Interpolator/","noteIcon":""}
---

动画执行速度设置器

#### AccelerateDecelerateInterpolator
先加速再减速，它的动画效果**看起来就像是物体从速度为 0 开始逐渐加速，然后再逐渐减速直到 0 的运动**。

#### LinearInterpolator
匀速

#### AccelerateInterpolator
持续加速。在整个动画过程中，一直在加速，直到动画结束的一瞬间，直接停止。

#### DecelerateInterpolator
持续减速直到 0。动画开始的时候是最高速度，然后在动画过程中逐渐减速，直到动画结束的时候恰好减速到 0。、

#### AnticipateInterpolator
先回拉一下再进行正常动画轨迹。效果看起来有点像投掷物体或跳跃等动作前的蓄力。


#### OvershootInterpolator
动画会超过目标值一些，然后再弹回来。效果看起来有点像你一屁股坐在沙发上后又被弹起来一点的感觉。

#### PathInterpolator
自定义动画完成度 / 时间完成度曲线。
定制的方式是使用一个 `Path` 对象来绘制出你要的动画完成度 / 时间完成度曲线。


### 自定义Interpolator
```
class MyInterpolator : TimeInterpolator {  
    override fun getInterpolation(t: Float): Float {  
		//在这里进行数学函数的运算
		//动画的执行速度由函数的运算结果控制
        var temp = t  
        temp -= 1.0f  
        LogUtils.e("temp:$temp")  
        return  temp * temp * ((1) * temp) + 1.0f  
    }  
}
```

使用[函数图像绘制工具](https://zh.numberempire.com/graphingcalculator.php?functions=1-x%2Cx*x*x%2B1&xmin=-3.384366&xmax=2.475009&ymin=-1.680268&ymax=2.225983&var=x)可以更直观的看到函数的变化曲线，
## 参考资料
