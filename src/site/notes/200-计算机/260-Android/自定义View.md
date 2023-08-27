---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/自定义View/","tags":["Android"],"noteIcon":""}
---


## 自定义View流程
| 步骤 | 关键字        | 作用                                       |
| ---- | ------------- | ------------------------------------------ |
| 1    | 构造函数      | View初始化                                 |
| 2    | onMeasure     | 测量View大小                               |
| 3    | onSizeChanged | 确定View大小                               |
| 4    | onLayout      | 确定子View布局(自定义View包含子View时有用) |
| 5    | onDraw        | 实际绘制内容                               |
| 6    | 提供接口      |  控制View或监听View某些状态                                          |

![Imgur](https://imgur.com/XQqZwR0.jpg)


## 测量模式（onMeasure）

|模式|二进制数值|描述|
|---|---|---|
|UNSPECIFIED|00|默认值，父控件没有给子view任何限制，子View可以设置为任意大小。|
|EXACTLY|01|表示父控件已经确切的指定了子View的大小。|
|AT_MOST|10|表示子View具体大小没有尺寸限制，但是存在上限，上限一般为父View大小。|

在实际运用之中只需要记住有三种模式，用 MeasureSpec 的 getSize是获取数值， getMode是获取模式即可。
## View绘制

### 坐标系
>左上角是坐标原点
#### View的坐标系统是相对于父控件而言的
-   getTop(); //获取子View左上角距父View顶部的距离
-   getLeft(); //获取子View左上角距父View左侧的距离
-   getBottom(); //获取子View右下角距父View顶部的距离
-   getRight(); //获取子View右下角距父View左侧的距离

#### View的坐标系统是相对于父控件而言的


## 参考资料
[安卓自定义View进阶-分类与流程](https://www.gcssloop.com/customview/CustomViewProcess.html)