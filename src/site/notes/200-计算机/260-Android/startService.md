---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/startService/","tags":["Android/Service"],"noteIcon":""}
---

一个started服务必须自行管理生命周期。也就是说，系统不会终止或销毁这类服务，除非必须恢复系统内存并且服务返回后一直维持运行。 因此，服务必须通过调用stopSelf()自行终止，或者其它组件可通过调用stopService()来终止它。