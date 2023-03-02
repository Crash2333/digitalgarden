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

## 参考资料
[安卓自定义View进阶-分类与流程](https://www.gcssloop.com/customview/CustomViewProcess.html)