---
{"dg-publish":true,"permalink":"/CodeiumException001/","noteIcon":""}
---

# Failed to download language server

今天在新版的[[600-应用科学/610-工具软件/AndroidStudio\|AndroidStudio]]中安装插件[[600-应用科学/610-工具软件/Codeium\|Codeium]]，装好之后遇到报错如下：
```
Failed to download language server
```


## 解决方案

### 1.使用[[Listary\|Listary]]找到codeium插件的存放目录
![](https://i.imgur.com/YWq3Hb1.png)

### 2.下载server文件
我们可以在[language-server的github仓库](https://github.com/Exafunction/codeium/releases)中找到需要使用的server。
例如我使用的插件版本是`1.6.11`，电脑是Windows64位的。
那么我只需要下载`language_server_windows_x64.exe`即可
![](https://i.imgur.com/ASnipmj.png)

### 3.server文件放入指定路径
![](https://i.imgur.com/yEat7WZ.png)


![](https://i.imgur.com/xXDFXOh.png)


### 重启AS
## 参考资料
[Codeium在IDEA里的3个坑：无法log in，downloading language server和中文乱码-CSDN博客](https://blog.csdn.net/zhtisi/article/details/130790718)
