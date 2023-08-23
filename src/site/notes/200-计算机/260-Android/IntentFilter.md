---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/IntentFilter/","noteIcon":""}
---

android的3个核心组件——Activity、services、广播接收器——是通过intent传递消息的。intent消息用于在运行时绑定不同的组件。

在 Android 的 AndroidManifest.xml 配置文件中可以通过 intent-filter 节点为一个 Activity 指定其 Intent Filter，以便告诉系统该 Activity 可以响应什么类型的 Intent。


### Action

　　一个 Intent Filter 可以包含多个 Action，Action 列表用于标示 Activity 所能接受的“动作”，它是一个用户自定义的字符串。

```
<intent-filter > 
 <action android:name="android.intent.action.MAIN" /> 
 <action android:name="com.scu.amazing7Action" /> 
……
 </intent-filter>
```


### URL

　　在 intent-filter 节点中，通过 data节点匹配外部数据，也就是通过 URI 携带外部数据给目标组件。

```
<data android:mimeType="mimeType" 
	android:scheme="scheme" 
	 android:host="host"
	 android:port="port" 
	 android:path="path"/>
```

注意：只有data的所有的属性都匹配成功时 URI 数据匹配才会成功

### Category

　　为组件定义一个 类别列表，当 Intent 中包含这个类别列表的所有项目时才会匹配成功。

```
<intent-filter . . . >
   <action android:name="code android.intent.action.MAIN" />
   <category android:name="code　android.intent.category.LAUNCHER" />
</intent-filter>
```