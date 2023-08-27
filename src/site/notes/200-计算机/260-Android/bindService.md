---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/bindService/","tags":["Android/Service"],"noteIcon":""}
---


当应用程序中的activity或其它组件需要与服务进行交互，或者应用程序的某些功能需要暴露给其它应用程序时，你应该创建一个bound服务，并通过进程间通信（IPC）来完成。

```
public class BindService extends Service {

	 // 实例化MyBinder得到mybinder对象；
	private final MyBinder binder = new MyBinder();
	
	  /**
     * 返回Binder对象。
     */
	@Override
	public IBinder onBind(Intent intent) {
		// TODO Auto-generated method stub
		return binder;
	}
    
     /**
      * 新建内部类MyBinder，继承自Binder(Binder实现IBinder接口),
      * MyBinder提供方法返回BindService实例。
      */
　　public class MyBinder extends Binder{
        
        public BindService getService(){
            return BindService.this;
        }
    }
     

	@Override
	public boolean onUnbind(Intent intent) {
		// TODO Auto-generated method stub
		return super.onUnbind(intent);
	}
}
```
