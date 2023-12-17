---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/获取第三方库的的离线jar或aar/","noteIcon":""}
---


一般来说，当一个三方库比较稳定不需要频繁更新的时候。作者这会提供一个**jar**或者**aar**文件，放在放在maven、jeatpack之类的远程仓库。再提供一个依赖的地址，供开发者使用。

## 离线环境
当开发者处于特殊的环境，需要离线开发时。是无法通过依赖拉取**jar**或者**aar**文件使用的。此时开发者如果需要使用三方库，只能先下载好**jar**或者**aar**文件。然后导入到离线的开发环境进行使用。

### 获取离线的aar
以[EasyFloat](https://github.com/princekin-f/EasyFloat)这个库为例，作者提供如下了集成的方法。

-   **在项目的根目录的`build.gradle`添加：**

```
allprojects {
    repositories {
        ...
	maven { url 'https://jitpack.io' }
    }
}
```

-   **在应用模块的`build.gradle`添加：**

```
dependencies {
    implementation 'com.github.princekin-f:EasyFloat:2.0.4'
}
```

在AndroidStudio中新建一个Demo项目，根据第三方库作者提供的方式。在Demo中集成 EasyFloat。集成成功之后，双击Ctrl使用[[Listary\|Listary]]全局的搜索关键字**EasyFloat**。效果如下：
![Imgur](https://i.imgur.com/5FuMSMw.png)


从图中可以看出EasyFloat这个库对应的aar文件所在的路径后续将aar文件导入离线环境的项目中使用即可

## 参考资料