---
dg-publish: true
date: 2023-03-02
tags: [Android/MVVM]
---
谷歌推出的数据绑定库，既支持单向绑定，也支持双向绑定。一般是和[[200-计算机/260-Android/ViewModel\|ViewModel]]搭配使用。

## 用法
### gradle配置
在 `app` 的 `build.gradle` 文件中，添加以下配置：

```groovy
android {
    defaultConfig {
        buildFeatures{
           // viewBinding 支持，
            viewBinding = true
           // dataBinding 支持
            dataBinding = true
        }
    }
}
```


### 修改布局
1. 在XML布局文件中，鼠标点击根节点`XXXLayout`
2. 使用快捷键`Alt`+`Enter`，`Convert to databinding layout`
使用上面的操作可以将布局文件快速转换为支持databinding的布局文件

### 关联布局
```
DataBindingUtil.bind(view) //关联Dialog
DataBindingUtil.setContentView(this, getLayout()) //关联Activity
```

