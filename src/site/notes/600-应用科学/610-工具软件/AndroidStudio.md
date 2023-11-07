---
{"dg-publish":true,"permalink":"/600-应用科学/610-工具软件/AndroidStudio/","noteIcon":""}
---

## 常用插件
- [[PlantUMLParser\|PlantUMLParser]]
- [[RainbowBrackets\|RainbowBrackets]]
- [[MarioProgressBar\|MarioProgressBar]]
- [[JSONToKotlinClass ​\|JSONToKotlinClass ​]]
- [[JsonFormatter\|JsonFormatter]]
- [[Codeium\|Codeium]]
- [[CodeGeeX\|CodeGeeX]]

{ .block-language-dataview}

## 常用设置
[[000-总类/090-Blog/AndroidStudio设置字体大小\|AndroidStudio设置字体大小]]
[[Local History\|Local History]]
#### 自动导包
```
File --> Settings --> Editor --> General --> Auto Import --> 勾选上 optimize imports on the fly 和 add unambiguous imports on the fly 的选项即可
```

#### 显示行号
```
File --> Settings --> Editor --> General --> Appearance --> 勾上 Show line numbers
```

#### 设置光标悬停时提示文档注释
```
File --> Settings --> Editor --> General --> Code Completion --> 然后可以在 Show the documentation popup in 【？】 ms.框框里面填写毫秒数值，我一般写的是500，表示鼠标悬停在代码上面500毫秒就可以看到文档。
```

#### 禁用studio的自动检查更新
```
File --> Settings --> Appearance & Behavior --> System Settings --> Updates--> Automatically check updates for 【？】，中括号里面是对应的更新渠道(包括：Stable Channel、Beta Channel、Dev Channel、Canary Channel)，取消对钩就是禁止更新。
右侧是【check now】，立即检查更新。  `
```

- Stable Channel ： 正式版本通道，只会获取最新的正式版本。(最稳定)
- Beta Channel ： 测试版本通道，只会获取最新的测试版本。
- Dev Channel ： 开发发布通道，只会获取最新的开发版本。
- Canary Channel ： 预览发布通道，只会获取最新的预览版本(问题较多,不建议选择这个)
#### 每次打开studio 会有个提示，查看和关闭的方式
```
点击菜单栏的 Help --> Tips of the Day  --> 可以查看提示窗，点击上面的Show tips on Startup 对勾去掉，以后再打开就不会出现这个提示了。如果要查看提示，就点击菜单栏的 Help --> Tips of the Day
```
## 快捷键
### 工具窗口

| 窗口名称         | Windows快捷键  |
| ---------------- | -------------- |
| 项目             | Alt+1          |
| 版本控制         | Alt+9          |
| 运行（Run）      | Shift+F10      |
| 调试（Debug）    | Shift+F9       |
| logcat           | Alt+6          |
| 返回编辑器       | Esc            |
| 隐藏所有工具窗口 | Ctrl+Shift+F12 |


### 代码补全
| 类型     | Windows快捷键     | 说明                                                                                                                     |
| -------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------ |
| 基本补全 | Ctrl+空格键       | 显示对变量、类型、方法和表达式等的基本建议。如果连续两次调用基本补全，系统将显示更多结果，包括私有成员和非导入静态成员。 |
| 智能补全 | Ctrl+Shift+空格键 | 根据上下文显示相关选项。智能补全功能会考虑预期类型和数据流。如果连续两次调用智能自动补全，系统将显示更多结果，包括链。   |
| **语句补全** | **Ctrl+Shift+Enter**  | 补全当前语句，添加缺失的圆括号、大括号、花括号和格式等。                                                                                                                         |


### 版本控制
| 操作说明     | Windows快捷键 |
| ------------ | ------------- |
| 提交当前修改 | Ctrl+K        |
|              |               |
|从 VCS 更新项目|Ctrl+T|Command+T|
|查看最近变更|Alt+Shift+C|Option+Shift+C|
|打开 VCS 对话框|Alt+`（反引号）|Ctrl+V|

### 重构
| 操作说明 | Windows快捷键 |                  |
| -------- | ------------- | ---------------- |
| 复制     | F5            | F5               |
| 移动     | F6            | F6               |
| 安全删除 | Alt+Delete    | Command+Delete   |
| **重命名**   | **Shift+F6**      | Shift+F6         |
| 更改签名 | Ctrl+F6       | Command+F6       |
| 内嵌     | Ctrl+Alt+N    | Command+Option+N |
| **提取方法** | **Ctrl+Alt+M**    | Command+Option+M |
| 提取变量 | Ctrl+Alt+V    | Command+Option+V |
| 提取字段 | Ctrl+Alt+F    | Command+Option+F |
| 提取常量 | Ctrl+Alt+C    | Command+Option+C |
| 提取参数 | Ctrl+Alt+P    | Command+Option+P |

### 调试
| 操作说明          | Windows快捷键 |                  |
| ----------------- | ------------- | ---------------- |
| **调试（Debug）** | **Shift+F9**      | Ctrl+D           |
| 单步跳过          | F8            | F8               |
| 单步进入          | F7            | F7               |
| 智能单步进入      | Shift+F7      | Shift+F7         |
| 单步退出          | Shift+F8      | Shift+F8         |
| 运行到光标位置    | Alt+F9        | Option+F9        |
| 评估表达式        | Alt+F8        | Option+F8        |
| 继续运行程序      | F9            | Command+Option+R |
| **切换断点**          | **Ctrl+F8**       | Command+F8       |
| **查看断点**          | **Ctrl+Shift+F8** | Command+Shift+F8 |


## 参考资料
[Android Studio常用设置和快捷键](https://github.com/AweiLoveAndroid/The-pit-of-the-Android-Studio/blob/master/readme/Android%20Studio%E5%B8%B8%E7%94%A8%E8%AE%BE%E7%BD%AE%E5%92%8C%E5%BF%AB%E6%8D%B7%E9%94%AE.md)
[键盘快捷键  |  Android Studio  |  Android Developers](https://developer.android.com/studio/intro/keyboard-shortcuts?hl=zh-cn)