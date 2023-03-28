---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/MVP/","tags":["Android/架构"],"noteIcon":""}
---

一种代码分层架构，代码解耦之后，方便复用和迭代更新。
在业务没有变动的情况下，我们可以更方便的迭代View，不需要变更数据逻辑和业务逻辑。
## Model
主要负责数据处理

## View
主要负责UI控件的处理，通常都是指☞[Activity](app://obsidian.md/Activity)和[Fragment](app://obsidian.md/Fragment)。主要处理动画播放暂停、View事件的监听等

## Presenter
主要负责处理业务逻辑，同时持有Viwe和Model的引用

![Imgur](https://imgur.com/cy33wSw.jpg)
