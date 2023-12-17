---
{"dg-publish":true,"permalink":"/CoroutineContext/","tags":["kotlin/协程"],"noteIcon":""}
---

**CoroutineContext 里存放着协程的分发器。**


## 协程分发器

**Dispatchers.Main**

> UI 线程，在Android里为主线程

**Dispatchers.IO**

> IO 线程，主要执行IO 操作

**Dispatchers.Default**

> 主要执行CPU密集型操作，比如一些计算型任务

**Dispatchers.Unconfined**

> 不特意指定使用的线程

  

作者：小鱼人爱编程  
链接：https://juejin.cn/post/7113706345190129700  
来源：稀土掘金  
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。


## 参考资料