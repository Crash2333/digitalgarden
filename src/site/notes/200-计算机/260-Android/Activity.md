---
{"dg-publish":true,"permalink":"/200/260-android/activity/","tags":["TODO"],"noteIcon":""}
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


## 启动模式
- Standard
- SingleTop
- SingleTask
- SingleInstance

## 启动流程


## 先背生命周期八股文
```
onCreate  
onStart  
onResume  
onPause  
onStop  
onDestroy
```

### 可以干什么？
>onCreate中主要是进行一些初始化的操作
>例如：实例化控件、为控件添加监听、初始化数据、初始化三方库等等


>onStart中通常是启动一些动画


>onResume



>onPause


>onStop


>onDestroy中通常是释放资源，避免内存泄漏


## 再背启动模式
[[standard标准模式\|standard标准模式]]
[[singleTop栈顶复用模式\|singleTop栈顶复用模式]]
[[singleTask\|singleTask]]
[[singleInstance\|singleInstance]]

## 