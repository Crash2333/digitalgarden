---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/AndroidStudio异常002/","noteIcon":""}
---

## 控制台打印乱码

### 修改vmoptions配置
1. 点击help
2. 点击Edit Custom VM Options
3. 在`studio64.exe.vmoptions`文件加入`-Dfile.encoding=UTF-8`

### 修改设置项
1. 进入AS的Settings页面
2. 搜索`Encodings`
3. 全部都设置为`UTF-8`编码

### 重启AS