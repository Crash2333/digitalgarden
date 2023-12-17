---
{"dg-publish":true,"permalink":"/ANR/","tags":["Android/性能优化"],"noteIcon":""}
---


## ANR产生机制

网上通俗的一段面试答题

> ANR——应用无响应，Activity是5秒，BroadCastReceiver是10秒，Service是20秒。

这句话说的很笼统，要想深入分析定位ANR，需要知道更多知识点，一般来说，ANR按产生机制，分为4类：

### 输入事件超时(5s)

**InputEvent Timeout**

- InputDispatcher发送key事件给 对应的进程的 Focused Window ，对应的window不存在、处于暂停态、或通道(input channel)占满、通道未注册、通道异常、或5s内没有处理完一个事件，就会发生ANR ​ 
- InputDispatcher发送MotionEvent事件有个例外之处：当对应Touched Window的 input waitQueue中有超过0.5s的事件，inputDispatcher会暂停该事件，并等待5s，如果仍旧没有收到window的‘finish’事件，则触发ANR ​ 
- 下一个事件到达，发现有一个超时事件才会触发ANR`

### 广播类型超时（前台15s，后台60s）

**BroadcastReceiver Timeout**
- 静态注册的广播和有序广播会ANR，动态注册的非有序广播并不会ANR ​ 
- 广播发送时，会判断该进程是否存在，不存在则创建，创建进程的耗时也算在超时时间里 ​ 
- 只有当进程存在前台显示的Activity才会弹出ANR对话框，否则会直接杀掉当前进程 ​ 
- 当onReceive执行超过阈值（前台15s，后台60s），将产生ANR ​ 
- 如何发送前台广播：Intent.addFlags(Intent.FLAG_RECEIVER_FOREGROUND)`

### 服务超时（前台20s，后台200s）

**Service Timeout**

- Service的以下方法都会触发ANR：onCreate(),onStartCommand(), onStart(), onBind(), onRebind(), onTaskRemoved(), onUnbind(), onDestroy(). ​ 
- 前台Service超时时间为20s，后台Service超时时间为200s ​ 
- 如何区分前台、后台执行————当前APP处于用户态，此时执行的Service则为前台执行。 ​ 
- 用户态：有前台activity、有前台广播在执行、有foreground service执行`

### ContentProvider 类型

- ContentProvider创建发布超时并不会ANR ​ 
- 使用ContentProviderclient来访问ContentProverder可以自主选择触发ANR，超时时间自己定 client.setDetectNotResponding(PROVIDER_ANR_TIMEOUT);`

## 导致ANR的原因

很多开发者认为，那就是耗时操作导致ANR，全部是app应用层的问题。实际上，线上环境大部分ANR由系统原因导致。

### 应用层导致ANR（耗时操作）
- 函数阻塞：如死循环、主线程IO、处理大数据 ​ 
- 锁出错：主线程等待子线程的锁 ​ 
- 内存紧张：系统分配给一个应用的内存是有上限的，长期处于内存紧张，会导致频繁内存交换，进而导致应用的一些操作超时`

### 系统导致ANR
- CPU被抢占：一般来说，前台在玩游戏，可能会导致你的后台广播被抢占CPU ​ 
- 系统服务无法及时响应：比如获取系统联系人等，系统的服务都是Binder机制，服务能力也是有限的，有可能系统服务长时间不响应导致ANR ​ 
- 其他应用占用的大量内存`


## 分析日志

发生ANR的时候，系统会产生一份anr日志文件（手机的/data/anr 目录下，文件名称可能各厂商不一样，业内大多称呼为trace文件），内含如下几项重要信息。

| 枚举值 | 含义 |
| ------------------- | ------------------------------------------------------------ | 
| `NEW` | 初始状态，线程被创建但尚未启动执行。还没有调用start | 
| `RUNNABLE` | 可运行状态，线程正在 Java 虚拟机中执行或准备执行。 |
| **BLOCKED** | 阻塞状态，线程被阻塞等待监视器锁定。 |
| **WAITING** | 等待状态，线程无限期地等待其他线程采取特定操作。 |
| **TIMED_WAITING** | 计时等待状态，线程等待其他线程采取特定操作，但最多等待一段时间。 |
| `TERMINATED` | 终止状态，线程已完成执行或提前终止。 |


-----

| Java Thread State | C++ Thread State | 含义 |
| ----------------- | ---------------- | ------------------------------ |
| `TERMINATED` | `ZOMBIE` | 线程死亡，终止运行 |
| `RUNNABLE` | `RUNNING/RUNNABLE` | 线程可运行或正在运行 |
| **TIMED_WAITING** | `TIMED_WAIT` | 执行了带有超时参数的等待操作 |
| **BLOCKED** | `MONITOR` | 线程阻塞，等待获取对象锁 |
| **WAITING** | `WAIT` | 执行了无超时参数的等待操作 |
| `NEW` | `INITIALIZING` | 新建，正在初始化，为其分配资源 |
| `NEW` | `STARTING` | 新建，正在启动 |
| `RUNNABLE` | `NATIVE` | 正在执行 JNI 本地函数 |
| **WAITING** | `VMWAIT` | 正在等待 VM 资源 |
| `RUNNABLE` | `SUSPENDED` | 线程暂停，通常是由于 GC 或调试暂停 |
| | `UNKNOWN` | 未知状态 |

>main线程处于 BLOCK、WAITING、TIMEWAITING状态，那基本上是函数阻塞导致ANR；
>如果main线程无异常，则应该排查CPU负载和内存环境。

## 堆栈消息
>堆栈信息是最重要的一个信息，展示了ANR发生的进程当前所有线程的状态。

```
suspend all histogram:  Sum: 2.834s 99% C.I. 5.738us-7145.919us Avg: 607.155us Max: 41543us
DALVIK THREADS (248):
"main" prio=5 tid=1 Native
  | group="main" sCount=1 dsCount=0 flags=1 obj=0x74b17080 self=0x7bb7a14c00
  | sysTid=2080 nice=-2 cgrp=default sched=0/0 handle=0x7c3e82b548
  | state=S schedstat=( 757205342094 583547320723 2145008 ) utm=52002 stm=23718 core=5 HZ=100
  | stack=0x7fdc995000-0x7fdc997000 stackSize=8MB
  | held mutexes=
  kernel: __switch_to+0xb0/0xbc
  kernel: SyS_epoll_wait+0x288/0x364
  kernel: SyS_epoll_pwait+0xb0/0x124
  kernel: cpu_switch_to+0x38c/0x2258
  native: #00 pc 000000000007cd8c  /system/lib64/libc.so (__epoll_pwait+8)
  native: #01 pc 0000000000014d48  /system/lib64/libutils.so (android::Looper::pollInner(int)+148)
  native: #02 pc 0000000000014c18  /system/lib64/libutils.so (android::Looper::pollOnce(int, int*, int*, void**)+60)
  native: #03 pc 0000000000127474  /system/lib64/libandroid_runtime.so (android::android_os_MessageQueue_nativePollOnce(_JNIEnv*, _jobject*, long, int)+44)
  at android.os.MessageQueue.nativePollOnce(Native method)
  at android.os.MessageQueue.next(MessageQueue.java:330)
  at android.os.Looper.loop(Looper.java:169)
  at com.android.server.SystemServer.run(SystemServer.java:508)
  at com.android.server.SystemServer.main(SystemServer.java:340)
  at java.lang.reflect.Method.invoke(Native method)
  at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:536)
  at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:856)
   
  ........省略N行.....
   
  "OkHttp ConnectionPool" daemon prio=5 tid=251 TimedWaiting
  | group="main" sCount=1 dsCount=0 flags=1 obj=0x13daea90 self=0x7bad32b400
  | sysTid=29998 nice=0 cgrp=default sched=0/0 handle=0x7b7d2614f0
  | state=S schedstat=( 951407 137448 11 ) utm=0 stm=0 core=3 HZ=100
  | stack=0x7b7d15e000-0x7b7d160000 stackSize=1041KB
  | held mutexes=
  at java.lang.Object.wait(Native method)
  - waiting on <0x05e5732e> (a com.android.okhttp.ConnectionPool)
  at com.android.okhttp.ConnectionPool$1.run(ConnectionPool.java:103)
  - locked <0x05e5732e> (a com.android.okhttp.ConnectionPool)
  at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1167)
  at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:641)
  at java.lang.Thread.run(Thread.java:764)

```


###  CPU 负载
```
Load: 2.62 / 2.55 / 2.25
CPU usage from 0ms to 1987ms later (2020-03-10 08:31:55.169 to 2020-03-10 08:32:17.156):
  41% 2080/system_server: 28% user + 12% kernel / faults: 76445 minor 180 major
  26% 9378/com.xiaomi.store: 20% user + 6.8% kernel / faults: 68408 minor 68 major
........省略N行.....
66% TOTAL: 20% user + 15% kernel + 28% iowait + 0.7% irq + 0.7% softirq

```

如上所示：

- 第一行：1、5、15 分钟内正在使用和等待使用CPU 的活动进程的平均数
    
- 第二行：表明负载信息抓取在ANR发生之后的0~1987ms。同时也指明了ANR的时间点：2020-03-10 08:31:55.169
    
- 中间部分：各个进程占用的CPU的详细情况
    
- 最后一行：各个进程合计占用的CPU信息。
    
#### 名词解释：
- user:用户态,kernel:内核态 ​
- faults:内存缺页，minor——轻微的，major——重度，需要从磁盘拿数据 ​ 
- iowait:IO使用（等待）占比 ​ 
- irq:硬中断，softirq:软中断`

**注意：**
- iowait占比很高，意味着有很大可能，是io耗时导致ANR，具体进一步查看有没有进程faults major比较多。
    
- 单进程CPU的负载并不是以100%为上限，而是有几个核，就有百分之几百，如4核上限为400%。

### 内存信息
```
Total number of allocations 476778　　进程创建到现在一共创建了多少对象
​
Total bytes allocated 52MB　进程创建到现在一共申请了多少内存
​
Total bytes freed 52MB　　　进程创建到现在一共释放了多少内存
​
Free memory 777KB　　　 不扩展堆的情况下可用的内存
​
Free memory until GC 777KB　　GC前的可用内存
​
Free memory until OOME 383MB　　OOM之前的可用内存
​
Total memory 当前总内存（已用+可用）
​
Max memory 384MB  进程最多能申请的内存

```


## 参考资料
[干货：ANR日志分析全面解析 - 掘金](https://juejin.cn/post/6971327652468621326?searchId=20231215160006A217666B93B6B195310C#heading-15)