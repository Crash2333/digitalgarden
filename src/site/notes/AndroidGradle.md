---
{"dg-publish":true,"permalink":"/AndroidGradle/","tags":["Android/Gradle"],"noteIcon":""}
---


## minSdkVersion：

指定app运行的最低设备sdk版本，如minSdkVersion=19 表示该app最低支持Android 4.4（API 19）设备，低于此版本的设备将不能使用该app。随着Android系统版本的持续更新，之前旧的系统版本占有率越来越低，我们可以根据需要将minSdkVersion值往后调整。

## compileSdkVersion:

和编译时有关。比如我们当前compileSdkVersion=28（Andorid 9.0），Android 10 新增了有关5G的api。我们的app想尽早使用5G相关的api，这时只需要将compileSdkVersion=29（Android 10）,就能在编译阶段编译通过。此外，还需要注意的是，由于这个5G api是新增的，因此需要判断当前系统版本>=29才能使用新api。

## targetSdkVersion
它的作用是兼容旧的api。
>对于同一个API(方法），新版本的系统更改了它的内部实现逻辑，新逻辑可能会影响之前调用此API的App，为了兼容此问题，引入targetSdkVersion。当targetSdkVersion>=xx(某个系统版本）时再生效其新修改的逻辑，否则还是沿用之前的逻辑。换句话说：如果你更改了targetSdkVersion值，说明你已经测试过兼容性问题了。



## 参考资料