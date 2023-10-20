---
dg-publish: true
date: 2023-09-27
tags:
  - Android
---
## 什么事BuildConfig？
BuildConfig是android studio在**打包时自动生成的一个java类**。

## 如何启用BuildConfig？
高版本的**AS**需要在`app`目录下的gradle中添加如下配置，**AS**才会生成BuildConfig类。
```
android {
	buildFeatures {  
	    dataBinding = true //打开dataBinding支持  
	    buildConfig = true //启用buildConfig  
	}
}
```


## BuildConfig在哪里？
BuildConfig类在项目工程的build/generated/source/buildConfig/androidTest或debug或release中，这些目录中的BuildConfig类中有相同的常量字段。

## 参考资料
[Gradle之BuildConfig自定义常量 - 简书](https://www.jianshu.com/p/274c9d95cf76)