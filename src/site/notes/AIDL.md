---
{"dg-publish":true,"permalink":"/AIDL/","noteIcon":""}
---

AIDL 全称Android 接口定义语言（Android Interface Definition Language），是一种用于定义客户端和服务端之间的通信接口的语言，它可以让不同进程之间通过IPC（进程间通信）进行数据交互。


我们可以根据不同的场景和需求，选择合适的IPC的方式。一般来说：

- 如果需要实现跨应用的数据共享，可以使用ContentProvider。
    
- 如果需要实现跨应用的功能调用，可以使用AIDL。
    
- 如果需要实现跨应用的消息传递，可以使用Messenger。
    
- 如果需要实现跨网络的数据交换，可以使用Socket。

## 定义AIDL 接口
>创建ICalculator.aidl文件


```
interface ICalculator {
  int add(int a, int b);
  int subtract(int a, int b);
  int multiply(int a, int b);
  int divide(int a, int b);
}

```

>创建完成后rebuild整个工程，生成AIDL接口
### 第 2 步，创建 Service 工程，实现AIDL接口

在「服务端」应用中，创建一个Service类，实现AIDL接口，并在onBind方法中返回一个IBinder对象。

```
public class CalculatorService extends Service {

  private final Calculator.Stub mBinder = new Calculator.Stub() {
    @Override 
    public int add(int a, int b) throws RemoteException {
      return a + b;
    }

    @Override
    public int subtract(int a, int b) throws RemoteException {
      return a - b;
    }

    @Override
    public int multiply(int a, int b) throws RemoteException {
      return a * b;
    }

    @Override
    public int divide(int a, int b) throws RemoteException {
      if (b == 0) {
        throw new IllegalArgumentException("Divisor cannot be zero");
      }
      return a / b;
    }
  };

  @Override
  public IBinder onBind(Intent intent) {
    return mBinder;
  }
}

```

在「服务端」应用中，注册Service，并设置android:enabled和android:exported属性为true，以便其他应用可以访问它。


### 第 3 步，创建客户端工程，调用AIDL接口

```
private ICalculator mCalculator;

private ServiceConnection mConnection = new ServiceConnection() {
    @Override
    public void onServiceConnected(ComponentName name, IBinder service) {
	    //类型强转
        mCalculator = ICalculator.Stub.asInterface(service);
        
        // 计算 3*6
        calculate('*',3,6);
    }

    @Override
    public void onServiceDisconnected(ComponentName name) {
        mCalculator = null;
    }
};

//在Activity中调用该方法
private void bindToServer() {
    Intent intent = new Intent();
    intent.setAction("com.wj.CALCULATOR_SERVICE");
    intent.setComponent(new ComponentName("com.xx.service", "com.xx.service.CalculatorService"));
    boolean connected = bindService(intent, mConnection, BIND_AUTO_CREATE);
    Log.e(TAG, "onCreate: " + connected);
}

```


## 参考资料

[【视频文稿】车载Android应用开发与分析 - AIDL实践与封装（上） - 掘金](https://juejin.cn/post/7221328463692120119?searchId=202312151424567A0D27A10A7BA789D074)

