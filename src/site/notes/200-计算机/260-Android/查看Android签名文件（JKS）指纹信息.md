---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/查看Android签名文件（JKS）指纹信息/","noteIcon":""}
---



今天公司要换apk的包名和签名文件。换了包名相当于是一个新的apk。之前集成第三方SDK注册的配置都不能用了，全部要申请新的。
申请新的配置，需要用到包名和签名文件的SHA1、MD5、SHA256等指纹信息。
公司电脑配置的JAVA版本是18，我使用下面的命令：
```
keytool -list -v -keystore 您的签名文件路径

别名: voiceparty 
创建日期: 2023年9月1日 
条目类型: PrivateKeyEntry 
证书链长度: 1 
证书[1]: 所有者: 
发布者: C=000000, ST=武汉, L=中国,  
序列号: 1 
生效时间: Fri Sep 01 15:07:03 CST 2023, 失效时间: Sat Aug 08 15:07:03 CST 2122 
证书指纹: 
SHA1: C4:C8://这里删除部分值
SHA256: 29:76:E2:5F:AF:1D:4C//这里删除部分值
签名算法名称: SHA256withRSA 
主体公共密钥算法: 2048 位 RSA 密钥 
版本: 1
```
没有看到JKS的MD5值，一时间有点懵逼。
这个命令之前用过很多次，都是没有问题的。我直接谷歌了一下。发现是java8以后版本的keytool不再输出md5指纹信息。这就有点坑了。
解决方案有两个：
1. 修改本地Java版本到1.7，然后再执行keytool命令
2. 使用AndroidStudio的gradle命令输出签名文件信息

## 方案1
修改Java版本没没什么好说的，去官网下载1.7版本的jdk[Java Archive Downloads - Java SE 7](https://www.oracle.com/java/technologies/javase/javase7-archive-downloads.html)。然后安装到指定路径，修改环境变量JAVA_HOME，指向1.7版本jdk的路径。重启电脑让环境变量生效。
让后执行keytool命令

## 方案2

执行gradle自带的`signingReport`Task，即可。
点击项目右侧的Gradle-->app--->Tasks-->android-->signingReport,双击signingReport，执行完毕后，找到release条目下的MD5值。

如果执行失败，可能是开启了gradle的缓存配置。
修改`gradle.properties`里面的配置
```
org.gradle.unsafe.configuration-cache=false //关闭缓存配置
```


## 参考资料
[Android获取SHA1值和MD5值 - Android - 123si 博客](https://www.123si.org/android/article/android-gets-sha1-and-md5-values/)
[android:keytool签名查看md5指纹(java 15) - 刘宏缔的架构森林 - 博客园](https://www.cnblogs.com/architectforest/p/17318174.html)
[android - Unable to download signingReport for SHA1 and SHA-256 - Stack Overflow](https://stackoverflow.com/questions/69732709/unable-to-download-signingreport-for-sha1-and-sha-256)