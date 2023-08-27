---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/BroadcastReceiver/","tags":["Android/四大组件"],"noteIcon":""}
---

广播是一种广泛运用的在应用程序之间传输信息的机制，主要用来监听系统或者应用发出的广播信息，然后根据广播信息作为相应的逻辑处理，也可以用来传输少量、频率低的数据。

在实现开机启动服务和网络状态改变、电量变化、短信和来电时通过接收系统的广播让应用程序作出相应的处理。

BroadcastReceiver 自身并不实现图形用户界面，但是当它收到某个通知后， BroadcastReceiver 可以通过启动 Service 、启动 Activity 或是NotificationMananger 提醒用户。


## 注册方式
### 静态注册
在AndroidManifest.xml的application里面定义receiver并设置要接收的action。

静态注册的广播接收者是一个常驻在系统中的全局监听器，当你在应用中配置了一个静态的BroadcastReceiver，安装了应用后而无论应用是否**处于运行状态**，广播接收者都是已经**常驻在系统中**了。同时应用里的所有receiver都在清单文件里面，方便查看。　 

要销毁掉静态注册的广播接收者，可以通过调用PackageManager将Receiver禁用。

### 动态注册
在Activity中声明BroadcastReceiver的扩展对象，在onResume中注册，onPause中卸载. 　　　

```

public class MainActivity extends Activity {
	MyBroadcastReceiver receiver;
	@Override
	 protected void onResume() {
		// 动态注册广播 (代码执行到这才会开始监听广播消息，并对广播消息作为相应的处理)
		receiver = new MyBroadcastReceiver();
		IntentFilter intentFilter = new IntentFilter( "android.provider.Telephony.SMS_RECEIVED" );
		registerReceiver( receiver , intentFilter);	
		super.onResume();
	}
	@Override
	protected void onPause() {  
		// 撤销注册 (撤销注册后广播接收者将不会再监听系统的广播消息)
		unregisterReceiver(receiver);
		super.onPause();
	}
}
```

