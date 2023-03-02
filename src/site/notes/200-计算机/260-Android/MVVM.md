---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/MVVM/","tags":["Android/架构"],"noteIcon":""}
---

>MVVM是一种代码的分层架构，具体由[[200-计算机/260-Android/DataBinding\|DataBinding]]+[[200-计算机/260-Android/ViewModel\|ViewModel]]+[[200-计算机/260-Android/LiveData\|LiveData]]来组合实现。
>[[200-计算机/260-Android/Activity\|Activity]]或[[200-计算机/260-Android/Fragment\|Fragment]]持有VM的引用，通过[[200-计算机/260-Android/DataBinding\|DataBinding]]和View控件产生关联。

M：Model
V：View
VM：ViewModel

## Model
主要负责数据处理，如本地数据库操作、从web接口获取数据等操作都放在Model层来处理

## View
主要负责UI控件的处理，通常都是指☞[[200-计算机/260-Android/Activity\|Activity]]和[[200-计算机/260-Android/Fragment\|Fragment]]。主要处理动画播放暂停、View事件的监听等

## ViewModel
主要负责页面的**状态管理**和通信

![Imgur](https://imgur.com/5o6KIl5.png)