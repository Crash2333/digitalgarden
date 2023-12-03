---
{"dg-publish":true,"permalink":"/ComposeException003/","tags":["JetpackCompose/Exception","TODO"],"noteIcon":""}
---

## navController传递参数

```
navController.navigate(  
    Screen.WebView.route + "/${URL_TYPE_1}"//不能传复杂参数，URL中有斜杠解析报错  
)
```


## 参考资料
[干货-Jectpack Compose 通过Navigation 传递 Serializable / Parcelable三种实现 - 掘金](https://juejin.cn/post/7088874644408631327)[android - Pass Parcelable argument with compose navigation - Stack Overflow](https://stackoverflow.com/questions/65610003/pass-parcelable-argument-with-compose-navigation)