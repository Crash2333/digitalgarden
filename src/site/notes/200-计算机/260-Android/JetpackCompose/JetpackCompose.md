---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/JetpackCompose/JetpackCompose/","tags":["Android/Compose"],"noteIcon":""}
---

## 待完善卡片
- [[200-计算机/260-Android/JetpackCompose/NavHostController\|NavHostController]]
- [[200-计算机/260-Android/JetpackCompose/NavHost\|NavHost]]
- [[200-计算机/260-Android/JetpackCompose/Compose权限\|Compose权限]]
- [[200-计算机/260-Android/JetpackCompose/Compose跑马灯\|Compose跑马灯]]
- [[200-计算机/260-Android/JetpackCompose/BottomNavigation\|BottomNavigation]]
- [[200-计算机/260-Android/Exception/ComposeException003\|ComposeException003]]

{ .block-language-dataview}

[[可组合函数\|可组合函数]]

[[200-计算机/260-Android/JetpackCompose/remember函数\|remember函数]]


[使用 Compose 进行导航  |  Jetpack Compose  |  Android Developers](https://developer.android.com/jetpack/compose/navigation?hl=zh-cn)

[[200-计算机/260-Android/JetpackCompose/CompositionLocalProvider\|CompositionLocalProvider]]
## 接口
[[200-计算机/260-Android/JetpackCompose/Modifier\|Modifier]]
## 组件
### 基础组件


- [[200-计算机/260-Android/JetpackCompose/TextField\|TextField]]
- [[200-计算机/260-Android/JetpackCompose/StickyHeader\|StickyHeader]]
- [[200-计算机/260-Android/JetpackCompose/Image\|Image]]

{ .block-language-dataview}
### 布局组件

- [[200-计算机/260-Android/JetpackCompose/TabRow\|TabRow]]
- [[200-计算机/260-Android/JetpackCompose/Row\|Row]]
- [[200-计算机/260-Android/JetpackCompose/Indicator\|Indicator]]
- [[200-计算机/260-Android/JetpackCompose/HorizontalPager\|HorizontalPager]]
- [[200-计算机/260-Android/JetpackCompose/Box\|Box]]
- [[200-计算机/260-Android/JetpackCompose/Column\|Column]]

{ .block-language-dataview}


### 列表
[[200-计算机/260-Android/JetpackCompose/LazyColumn\|LazyColumn]]

- [[200-计算机/260-Android/JetpackCompose/LazyColumn\|LazyColumn]]

{ .block-language-dataview}
## 导航

- [[200-计算机/260-Android/JetpackCompose/NavHostController\|NavHostController]]
- [[200-计算机/260-Android/JetpackCompose/NavHost\|NavHost]]
- [[200-计算机/260-Android/JetpackCompose/BottomNavigation\|BottomNavigation]]

{ .block-language-dataview}

## 手势

- [[200-计算机/260-Android/JetpackCompose/Scrollable\|Scrollable]]

{ .block-language-dataview}

## 动画

## MVI
[[200-计算机/260-Android/JetpackCompose/ComposeBaseViewModel\|ComposeBaseViewModel]]

## 三方库
- [[200-计算机/260-Android/JetpackCompose/Matisse\|Matisse]]

{ .block-language-dataview}

## Effect API
>在很多讲解关于程序设计最佳实践的文章或者书籍里，都会推荐一个编码原则：**尽可能使用 val、不可变对象及纯函数来设计程序**。这个原则在 Jetpack Compose 中也同样需要遵守，因为一个合格的可组合函数就应该属于**纯函数**，幂等且没有副作用。


>何谓纯函数？假如一个函数使用相同的入参参数重复执行时，总是能获得相同的运行结果，且运行结果不会影响任何外部状态，也不用担心重复执行会对外部造成改变，那么这个函数就称为纯函数。纯函数不具备副作用，具有引用透明性。副作用就是指修改了某处的某些东西，比如：
>- 引用或修改了外部变量的值
>- 执行了 IO 操作，比如读写了 SharedPreferences
>- 执行了 UI 操作，比如修改了一个按钮的可操作状态

- [[200-计算机/260-Android/JetpackCompose/LaunchedEffect\|LaunchedEffect]]

{ .block-language-dataview}
## 参考资料
[迁移基于 View 的现有应用  |  Jetpack Compose  |  Android Developers](https://developer.android.com/jetpack/compose/migrate?hl=zh-cn)
[迁移策略  |  Jetpack Compose  |  Android Developers](https://developer.android.com/jetpack/compose/migrate/strategy?hl=zh-cn)
[迁移到 Jetpack Compose](https://developer.android.com/codelabs/jetpack-compose-migration?hl=zh-cn#0)
[Compose + Fragment是一个不错的选择 - 掘金](https://juejin.cn/post/7179590175515738168#comment)

[Compose 与 Kotlin 的兼容性对应关系  |  Android 开发者  |  Android Developers](https://developer.android.com/jetpack/androidx/releases/compose-kotlin?hl=zh-cn)

[两年 Compose 项目实践总结，常见错误一览 - 掘金](https://juejin.cn/post/7139864943918055432)
[JetpackCompose的响应式布局实践 | 实验分享 - 掘金](https://juejin.cn/post/7307838693145903138)


[android/compose-samples: Official Jetpack Compose samples.](https://github.com/android/compose-samples)