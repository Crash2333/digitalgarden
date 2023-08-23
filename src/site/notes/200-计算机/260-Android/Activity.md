---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/Activity/","tags":["Android/四大组件"],"noteIcon":""}
---


Android四大组件之一。本质上就是一个交互界面。
## 生命周期
1. [[200-计算机/260-Android/onCreate\|onCreate]]
2. [[200-计算机/260-Android/onStart\|onStart]]
4. [[200-计算机/260-Android/onResume\|onResume]]
5. [[200-计算机/260-Android/onPause\|onPause]]
6. [[200-计算机/260-Android/onStop\|onStop]]
7. [[200-计算机/260-Android/onDestroy\|onDestroy]]
8. [[200-计算机/260-Android/onRestart\|onRestart]]

![](https://imgur.com/R4QX7qB)
![Imgur](https://imgur.com/R4QX7qB.png)

## 启动模式
- [[200-计算机/260-Android/Standard\|Standard]]
- [[200-计算机/260-Android/SingleTop\|SingleTop]]
- [[200-计算机/260-Android/SingleTask\|SingleTask]]
- [[200-计算机/260-Android/SingleInstance\|SingleInstance]]


### 配置方法

```
<activity
	．．．．．．
    android:launchMode="standard">
     ．．．．．．．
</activity>
```

## 启动流程



## 其它
### 横竖屏切换
横竖屏切换的生命周期：

> onPause() --> onSaveInstanceState() --> onStop() --> onDestory() --> onCreate() --> onStart() --> onRestoreInstanceState() --> onResume()

可以通过在AndroidManifest文件的Activity中指定如下属性来避免横竖屏切换：

```
android:configChanges = "orientation| screenSize"
```