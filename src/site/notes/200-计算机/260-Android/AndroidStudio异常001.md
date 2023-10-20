---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/AndroidStudio异常001/","tags":["AndroidStudio/Exception"],"noteIcon":""}
---



```
E:\AndroidProjects\xiongxiongyuyin-android\app\build\intermediates\compile_and_runtime_not_namespaced_r_class_jar\debug\R.jar: 另一个程序正在使用此文件，进程无法访问。
```


## 解决方案

### 方案1
在cmd中执行下面的命令
```
taskkill /im java.exe /f
```

### 方案2

删除下面路径下的所有xml文件
```
%USERPROFILE%\AppData\Roaming\Google\AndroidStudioPreview2020.3\workspace
```

## 参考资料
[Android Studio: R.jar: The process cannot access the file because it is being used by another process - Stack Overflow](https://stackoverflow.com/questions/62082922/android-studio-r-jar-the-process-cannot-access-the-file-because-it-is-being-us)