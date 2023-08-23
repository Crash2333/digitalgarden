---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/谱写Kotlin面试指南三部曲-Flow篇 - 掘金/","tags":["koltin/面试"],"noteIcon":""}
---

## 转载
> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [juejin.cn](https://juejin.cn/post/7222982459583152188)

> 前言 由于Flow相对来说比较复杂，所以笔者单独整理了一篇；Kotlin Flow流是协程的一个特性，它用作响应式编程框架。Flow流旨在处理异步数据流。它类似于 Kotlin 中的Sequences

#### 前言

由于 _Flow_ 相对来说比较复杂，所以笔者单独整理了一篇；_Kotlin Flow_ 流是协程的一个特性，它用作响应式编程框架。_Flow_ 流旨在处理异步数据流。它类似于 Kotlin 中的 _Sequences_，也具有响应式编程的好处。本文笔者通过思考关于 Flow 的一些问题，来验证是否初步了解掌握 _Kotlin Flow_。

Kotlin 面试指南三部曲系列：

*   [谱写 Kotlin 面试指南三部曲 - 基础篇](https://juejin.cn/post/7213582722329952312 "https://juejin.cn/post/7213582722329952312")
*   [谱写 Kotlin 面试指南三部曲 - 协程篇](https://juejin.cn/post/7220235452292137019 "https://juejin.cn/post/7220235452292137019")

#### 什么是 Kotlin Flow 流？

在 Kotlin 官网中定义中是这么说的：

> 在协程中，与仅返回单个值的挂起函数相反，Flow 可按顺序发出多个值, 它以协程为基础构建，可提供多个值，从概念上来讲，Flow 是可通过异步方式进行计算处理的一组数据序列，所发出值的类型必须相同。

总结一下，我们可以将 _Flow_ 定义为**具有多个异步计算值的协程**。它是可以异步计算的数据流，用于按顺序发送多个值。 发出的数据必须是同一类型，并且也是按顺序发出的，_Flow_ 使用挂起的函数以异步方式消费和生产。

#### 为什么需要 Kotlin Flow?

为了使应用程序响应并提高其性能，异步编程起着非常重要的作用，日常开发中，在协程没有出现的岁月里，可以使用 _RxJava_ 响应式编程框架，它是 _ReactiveX_ 基于 _Java_ 的扩展，直到 Kotlin 的出现和发展。

在 _Kotlin_ 中，相同的功能以 _Kotlin Flow API_ 的形式提供。它不仅具备所需的所有运算符和功能，而且还支持挂起函数，这有助于以顺序方式执行异步任务，也让代码变得更加简洁和高效。

#### 如果我们有 RxJava / 其他响应式实现，为什么要创建 Flow？

在 _Flow_ 中，如果我们想转换数据，用一个 _map_ 操作符即可，这与 _RxJava_ 有些不同，_RxJava_ 具有同步的 _map_ 和异步的 _flatMapSingle_。流程图运算符有一个 _lambda_，它是一个暂停，因此它适用于同步和异步。过滤数据也是如此，_Flow_ 只有一个 _Filter_ 运算符适用于两者。

所以 _Flow_ 能**有效减少了在其它响应式实现中引入的操作符**，更加方便简洁，这也是为什么要使用 Flow 的重要原因。

#### Kotlin Flow 是如何工作的？

平常我们开发都会使用到网络请求吧，当从服务器请求数据并使用异步编程来处理该数据时，_Flow_ 会在后台线程中异步管理该数据，因为某些进程可能会运行更长时间来获取数据。一旦收集器接收并收集了数据，就会使用回收器视图显示数据。

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1b43a5d1ef254655aa097ae00f2411d0~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

我们已经知道，_Flow_ 是一系列值，它使用挂起函数异步生成和使用值。

Flow 流由三个实体组成：

*   生产者: 用于发出添加到流中的数据。
*   中介：它可以修改发送到流中的值
*   消费者 : 从流中接收值

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/19b91677b43c4c728b95690038d586d4~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

#### Flow builders 的几种类型？

我们平时创建一个 Flow 流一般提供了 4 种方式

*   _flowOf_：它用于一组数据的创建 Flow 流
    
    ```
    flowOf(4, 2, 3, 45, 5)
                .collect {
                    print(it)
                }
    ​
    
    
    ```
    
*   _asFlow_：这是一个扩展函数，有助于将当前类型转换为 Flow 流
    
    ```
    (1..5).asFlow()
                .collect {
                    print(it)
                }
    
    
    ```
    
*   _flow_：这就是官方示例程序标准的创建 Flow 流的方式
    
    ```
    flow {
                (0..10).forEach {
                    emit(it)
                }
            }.collect {
                print(it)
            }
    
    
    ```
    
*   _channelFlow_：此构建器使用构建器本身提供的发送元素来创建 Flow 流。
    
    ```
    @OptIn(ExperimentalCoroutinesApi::class)
            channelFlow {
                (0..10).forEach {
                    send(it)
                }
            }.collect {
                print(it)
            }
    
    
    ```
    
    > 需要注意的是 channelFlow 这个 Api 还是实验性的，所以正式项目环境中很少用到
    

#### Kotlin Flow 如何实现并发？

我们都知道，_Flow_ 是异步的，但是收集器 _collect_ 和发射器 _emit_ 是按顺序的方式来工作，怎么说呢？就是当收集器开始收集数据，然后发射器发射出数据，直到没有发射器为止。经常有人说，**它就是用同步的代码做异步的事情**，这个总结挺到位的。当然，为了实现 _Flow_ 并发，我们必须从使用单个协程转变为使用多个协程。

_Flow_ 对此提供了一些特殊的并发运算符，比如说 _buffer()_ , 简单使用一个例子

```
fun main() = runBlocking {
    val time = measureTimeMillis {
        flow {
            for (i in 1..5) {
                delay(100)
                emit(i)
            }
        }
        .buffer()
        .collect { value ->
            delay(300)
            println(value)
        }
    }
    println("Collected in $time ms")
}


```

在上述例子中，所有的 delay 所花费的时间是 2000ms, 当然这是在没有并发操作的情况下，然而通过 _buffer_ 操作符并发地执行 _emit_，再顺序地执行 _collect_ 函数后，所花费的时间在 1700ms 左右，比预期的花费时间更高效。

那我们使用缓存区 buffer 的时候会发生什么呢？如下图所示

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1391dcee1d9d4c7da781784323e7ce71~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

当收集器处理发出的数据时, 下一个发射器开始其过程。它不会等待收集器完成它对先前发出的数据的处理并返回控制权。这是通过在单独的协程中运行收集器和发射器来实现的，这与在单个协程中运行的异步顺序方法不同。在内部它使用通道 _Channel_ 将数据发送给接收者。

#### Kotlin Flow 如何进行并行调用？

那有小伙伴说了，如果我有很多个长任务想要同时执行呢，也就是并行，Flow 能不能做到呢？答案肯定是 YES 的，为了并行运行长任务，我们需要使用 Flow 提供的组合操作符 _zip_，它通过指定的函数将两个流集合的排放组合在一起，并根据此函数的结果为每个组合排放单个项目。

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/00887f5ca05f4c3c8e1e7484fc546f52~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

让我们通过示例代码来理解弹珠图：

```
val flowOne = flowOf(1, 2, 3)
val flowTwo = flowOf("A", "B", "C")
​
flowOne.zip(flowTwo) { intValue, stringValue ->
    "$intValue$stringValue"
}.collect {
    println(it)
}


```

输出结果如下：

```
1A
2B
3C


```

可以看到通过 _zip_ 压缩将两个流执行完之后再一起输出结果，不够清晰？那我们再举一个 Android 中的真实用例：当我们想要并行运行两个网络请求任务并希望在两个任务完成时将两个任务的结果放在一个回调中。

假设我们有两个长时间允许的网络请求任务

*   长时间运行的任务请求一：
    
    ```
    private fun doLongRunningTaskOne(): Flow<String> {
        return flow {
            //开始请求接口。。。。
            delay(5000)
            emit("One")
        }
    }
    ​
    
    
    ```
    
*   长时间运行的任务请求二:
    
    ```
    private fun doLongRunningTaskTwo(): Flow<String> {
        return flow {
            //请求另一个接口。。。
            delay(5000)
            emit("Two")
        }
    }
    
    
    ```
    
*   现在，使用 _zip_ 操作符处理
    
    ```
    fun startLongRunningTask() {
        viewModelScope.launch {
            doLongRunningTaskOne()
                .zip(doLongRunningTaskTwo()) { resultOne, resultTwo ->
                    return@zip resultOne + resultTwo
                }
                .flowOn(Dispatchers.Default)
                .catch { e ->
                    //异常处理
                }
                .collect {
                    //获取结果
                    println(it)
                }
        }
    }
    
    
    ```
    
*   结果输出如下:
    
    ```
    OneTwo
    
    
    ```
    
    在这里，由于我们使用了 _zip_ 运算符，它并行运行两个任务，并在两个任务完成时在一个回调中给出两个任务的结果。
    
    通过使用 _zip_ 运算符压缩两个流集合，两个任务并行运行。当两者都完成时，我们就会得到结果。这样我们就一次得到了两个流集合的结果。
    
    _Kotlin Flow_ 的 _zip_ 运算符的优点：
    
*   并行运行任务。
    
*   当所有任务完成时，在单个回调中返回任务结果。
    

这样我们就可以在 Kotlin 中使用 _Flow_ 的 _Zip_ 操作符来并行运行任务。

#### Kotlin Flow 中的异常处理？

我们都知道了 Flow 是在协程的基础进行构建的，它可以在有或没有异常的情况下完成，如果有异常的话它会直接完成 _Complete_；在 _Flow_ 中，我们一般都使用其提供的 _catch_ 操作符来进行异常的处理。

还是以往的套路，先来举个例子，看下面的代码，告诉我，它会发生异常导致崩溃么? 答案是肯定的

```
(1..5).asFlow().map {
            //当值为3得时候抛出异常
            check(it != 3) {
                "Value $it"
            }
            it * it
        }.onCompletion {
            Log.d(TAG, "onCompletion")
        }.collect {
            Log.d(TAG, "$it")
        }


```

输出结果如下：

```
1
4
onCompletion
Exception in thread "main" java.lang.IllegalStateException: Value 3


```

是的，它崩溃了，中止了发射数据，Flow 进入了 _onCompletion_ 状态

此时我们再加上 _catch_ 操作符，它将把异常的句柄信息交给我们，并不会发生崩溃

```
(1..5).asFlow().map {
            check(it != 3) {
                "Value $it"
            }
            it * it
        }.onCompletion {
            Log.d(TAG, "onCompletion")
        }.catch { e ->
            Log.e(TAG, "Caught is $e")
        }.collect {
            Log.d(TAG, "$it")
        }


```

结果将是：

```
1
4
onCompletion
Caught java.lang.IllegalStateException: Value 3


```

它记录了异常信息，可以看到，无论加不加 _catch_ 操作符，_Flow_ 发射数据都会中止，并且直接进入 _OnComplete_ 状态，这和协程的异常处理基本是一致的，原来如此，差点忘了，Flow 是以协程的基础构建，属于包含关系。

如此，我们知道了 _Flow_ 是如何处理异常的，**我们可以将 _catch_ 应用于单个流并在出现任何错误时发出数据**

#### 如果我有一个长时间任务有异常的任务，Flow 怎么进行重试？

和 _Rxjava_ 一样，在进行任务重试的时候，Kotlin Flow 提供了相应的操作符, 它们分别是

*   _retrywhen_
*   _retry_

在大多数情况下，这两个操作符可以互换使用，它们本身并没有什么太大的区别，下面我们分别来看看吧

##### retrywhen

先用力的撇一眼 _Kotlin Flow_ 源码中 _retryWhen_ 的定义

```
fun <T> Flow<T>.retryWhen(predicate: suspend FlowCollector<T>.(cause: Throwable, attempt: Long) -> Boolean): Flow<T>


```

我们先开始使用这个操作符

```
.retryWhen { cause, attempt ->

}


```

可以看到它返回了两个参数，它们分别是

*   **cause**：_Throwable_ 所有错误和异常的基类。
*   **attempt**：_attempt_ 是代表当前尝试的次数，它**从零开始**。

这样以来，当我们在任务中出现了异常，我们将收到当前异常和尝试次数，这个时候就需要我们根据需求条件进行判断是否进行重试了，只有满足了一定的条件才可以重试，如此我们可以这么做

```
.retryWhen { cause, attempt ->
    if (cause is IOException && attempt < 3) {
        delay(2000)
        return@retryWhen true
    } else {
        return@retryWhen false
    }
}


```

##### retry

还是老规矩，我们再用力瞥一眼 _retry_ 的源码定义

```
fun <T> Flow<T>.retry(
    retries: Long = Long.MAX_VALUE,
    predicate: suspend (cause: Throwable) -> Boolean = { true }
): Flow<T> {
    require(retries > 0) { "Expected positive amount of retries, but had $retries" }
    return retryWhen { cause, attempt -> attempt < retries && predicate(cause) }
}


```

只用关心一点，它实际上是在 _retryWhen_ 的基础上调用，这也是为什么这两个操作符可以互相替换

_retry_ 函数是默认参数的，如果不设置次数，它将使用 _Long.MAX_VALUE_, 这样以来它将会不断重试，直到任务完成为止。所以我们可以这么写:

```
.retry(retries = 3) { cause ->
    if (cause is IOException) {
        delay(2000)
        return@retry true
    } else {
        return@retry false
    }
}


```

#### 说说 Cold Flow 冷流 和 Hot Flow 热流？

说起 _Flow_ 可以分为冷流和热流，结合官网和网络上的一些解释，其实分别可以概括成一句话

*   冷流就是**不消费，不生产，多次消费，多次生产，一对一关系**
    
*   热流就是**只要创建，有无消费，都生产，一对多关系**
    
    你说什么，不是特别清晰，那笔者用一个表来展示冷流和热流的区别吧
    

<table><thead><tr><th>冷流</th><th>热流</th></tr></thead><tbody><tr><td>它仅在有收集器的时候才有数据</td><td>即使没有收集器，它也会发出数据</td></tr><tr><td>它不存储数据</td><td>它可以存储数据</td></tr><tr><td>它不能有多个收集器</td><td>它允许有多个收集器</td></tr></tbody></table>

在 _Cold Flow_ 中，在多个收集器的情况下，完整的流程将从每个收集器的开始而开始，执行任务并将值发送到它们相应的收集器。这就像一对一的映射。1 个收集器的 1 个生产流量。这意味着冷流不能有多个收集器，因为它将为每个收集器创建一个新流。

在 _Hot Flow_ 中，在多个收集器的情况下，流将继续发出值，收集器从它们开始收集的地方获取值。这就像 1 对 N 映射，N 个收集器对应 1 个生产流量，这意味着一个热流可以有多个收集器。

如此我们写些伪代码来辅助说明下吧：

*   冷流示例

假设我们有一个 _Cold Flow_，它以 1 秒的间隔发出 1 到 5

```
fun getNumbersColdFlow():ColdFlow<Int> {
    return someColdFlow {
        (1..5).forEach {
            delay(1000)
            emit(it)
        }
    }
}


```

我们创建两个收集器进行收集:

```
val numbersColdFlow = getNumbersColdFlow()

numbersColdFlow
    .collect {
        println("1st Collector: $it")
    }

delay(2500)

numbersColdFlow
    .collect {
        println("2nd Collector: $it")
    }


```

那么输出将是：

```
1st Collector: 1
1st Collector: 2
1st Collector: 3
1st Collector: 4
1st Collector: 5

2nd Collector: 1
2nd Collector: 2
2nd Collector: 3
2nd Collector: 4
2nd Collector: 5


```

我们这两个收集器从一开始就会得到所有的值，会从头到尾全部一点不落的拿到

*   热流示例

假设我们有一个 _Hot Flow_，它同样以 1 秒的间隔发出 1 到 5

```
fun getNumbersHotFlow(): HotFlow<Int> {
    return someHotflow {
        (1..5).forEach {
            delay(1000)
            emit(it)
        }
    }
}


```

现在我们继续创建两个收集器进行收集：

```
val numbersHotFlow = getNumbersHotFlow()

numbersHotFlow
    .collect {
        println("1st Collector: $it")
    }

delay(2500)

numbersHotFlow
    .collect {
        println("2nd Collector: $it")
    }


```

输出将是

```
1st Collector: 1
1st Collector: 2
1st Collector: 3
1st Collector: 4
1st Collector: 5

2nd Collector: 3
2nd Collector: 4
2nd Collector: 5


```

可以看到，第一个收集器将会接收到所有的值，由于第二个收集器将会 2500 毫秒之后开始收集，所以它只会收集那些 2500 毫秒之后的值。

#### StateFlow 和 SharedFlow 之间的区别？

我们已经知道什么是冷流和热流了，而 _StateFlow_ 和 _SharedFlow_ 都属于热流，下面笔者列出一张表来说明 _StateFlow_ 和 _SharedFlow_ 之间的区别

<table><thead><tr><th>StateFlow</th><th>SharedFlow</th></tr></thead><tbody><tr><td>热流</td><td>热流</td></tr><tr><td>需要一个初始值并在收集器开始收集时立即发出它</td><td>不需要初始值，因此默认情况下不发出任何值</td></tr><tr><td>写法：val stateFlow = MutableStateFlow(0)</td><td>写法: val sharedFlow = MutableSharedFlow()</td></tr><tr><td>仅发出最后一个已知值</td><td>可以配置为使用重播运算符发出许多以前的值</td></tr><tr><td>它有 value 属性，可以查看当前值，保留了一个值的历史记录，我们可以直接获取而无需收集</td><td>它没有 value 属性</td></tr><tr><td>它不会发出连续的重复值。只有当它与前一项不同时，它才会发出值</td><td>它发出所有值并且不关心与前一项的区别，它还发出连续的重复值</td></tr><tr><td>类似于 LiveData，除了 Android 组件的生命周期感知。我们应该使用带有 StateFlow 的 repeatOnLifecycle 范围来为其添加生命周期感知，然后它就会变得与 LiveData 完全一样</td><td>和 LiveData 不同</td></tr></tbody></table>

我们分别举个相应的例子看看：

*   StateFlow 示例
    
    假设我们去记录小明的一次数学考试成绩, 一开始的成绩是个鸭蛋，代码如下：
    
    ```
    val gradeStateFlow = MutableStateFlow(0)
    
    
    ```
    
    这个时候老师再去收集这个成绩
    
    ```
    gradeStateFlow.collect {
        println(it)
    }
    
    
    ```
    
    一旦开始收集了，那么我们就会得到，原来小明考了个鸭蛋，回去应该得挨骂了
    
    ```
    0
    
    
    ```
    
    这是因为小明的初始分数就是 0，它会立即发出
    
    后来老师发现原来自己算错分了，小明的分数原来是 10 分，所以就继续设置这个值, 但又不小心输了两遍进去
    
    ```
    gradeStateFlow.value = 10
    gradeStateFlow.value = 10
    
    
    ```
    
    此时最后只会得到一个值，那就是 10 分，因为它不会发出**连续的重复值**
    
    ```
    10
    
    
    ```
    
    小明回到家了，妈妈问他成绩怎么样，小明怕被打没有告诉她，所以妈妈就亲自打电话问了老师，这个时候，我们就创建了一个新的收集器，用来发送小明的最终成绩
    
    ```
    gradeStateFlow.collect {
        println(it)
    }
    
    
    ```
    
    这个时候妈妈已经知道了小明最终只考了 10 分，免不了一顿责骂
    
    ```
    10
    
    
    ```
    
    因为 _StateFlow_ 存储最后一个值并在新的收集器中开始收集时会立即发出它
    
*   SharedFlow 示例
    

第二天，小明的妈妈让小明去买些水果回来，于是乎，小明来到了楼下的水果店，开始选些水果并放入自己的购物篮中

```
 ```kotlin
 val fruitSharedFlow = MutableSharedFlow<String>()
 fruitSharedFlow.collect {
     println(it)
 }
 ```


```

这个时候是不会得到任何东西的，小明还没开始购买水果呢，这个时候他拿了 1 斤苹果，1 斤香蕉和 1 斤葡萄，后面发现葡萄不够又拿了 1 斤

```
```kotlin
fruitSharedFlow.emit("1斤苹果")
fruitSharedFlow.emit("1斤香蕉")
fruitSharedFlow.emit("1斤葡萄")
fruitSharedFlow.emit("1斤葡萄")
```


```

最终得到的结果就是

```
1斤苹果
1斤香蕉
1斤葡萄
1斤葡萄


```

可以看到我们可以得到连续的重复值，现在小明买完回到家，将购物篮的水果都交给了妈妈，这时候小明再看购物篮的时候，里面已经空空如也了, 他不会得到任何结果，因为 _SharedFlow_ 不存储最后一个值

```
fruitSharedFlow.collect {
    println(it)
}


```

现在通过两个现实中的例子我们就可以理解下面几点

*   _StateFlow_ 是 _SharedFlow_ 的一种，_StateFlow_ 是 _SharedFlow_ 的特化
    
*   _StateFlow_ 本质是一个具有固定 replay = 1 的 _SharedFlow_，并增加了一些内容。这意味着新收集器在开始收集后将立即获得当前状态初始值。怎么说呢，我们还是用一段伪代码看看吧
    
    ```
    StateFlow = SharedFlow
                .withInitialValue(initialValue)
                .replay(count=1)
                .distinctUntilChanged()
    
    
    ```
    
    实际开发中，我们是可以使用 _SharedFlow_ 获取 _StateFlow_ 行为
    
    ```
    val sharedFlow = MutableSharedFlow<Int>(
        replay = 1,
        onBufferOverflow = BufferOverflow.DROP_OLDEST
    )
    sharedFlow.emit(0) // initial value
    val stateFlow = sharedFlow.distinctUntilChanged()
    
    
    ```
    
    事实上，这是让我们可以自定义属于我们的 _StateFlow_，比如说需要存储最后的两个值，我们就可以根据我们的用例执行 _replay = 2_
    

#### 什么时候需要用 StateFlow/SharedFlow?

##### 使用 StateFlow 的情况

还是使用实际的例子来说明，我们有一个用例，就是通过网络从后台用户信息接口获取用户列表并将其显示再 UI 中

现在我们的 _ViewModel_ 中有一个 _StateFlow_

```
val usersStateFlow = MutableStateFlow<UiState<List<User>>>(UiState.Loading)


```

在 _Activity_ 中创建收集器

```
usersStateFlow.collect {
​
}


```

现在，只要我们进入到 _Activity_ 中，就会开始订阅收集，将收集以下内容：

usersStateFlow：作为 _StateFlow_ 加载状态采用初始值并立即发出

当我们的 _viewModel_ 从网络中获取数据时，它将数据设置到 usersStateFlow。

```
usersStateFlow.value = UiState.Success(usersFromNetwork)


```

我们的 _Activity_ 中的收集器将获取用户的数据并将其显示在 UI 中

试想一下，如果方向改变了呢，_ViewModel_ 将被保留，但我们在 Activity 中的收集器将重新订阅收集，由于 _StateFlow_ 保留最后一个值，我们可以直接获取之前从网络设置的用户列表，这个时候优势在于我不需要在**重新请求网络接口了**

这个时候，我们尝试使用 _SharedFlow_ 代替 _StateFlow_ 看看

```
val usersSharedFlow = MutableSharedFlow<UiState<List<User>>>()
usersSharedFlow.collect {
​
}


```

现在，只要我们打开 Activity，Activity 就会订阅收集。由于使用了 _SharedFlow_，因此不会在此处收集任何内容。

当我们的 _ViewModel_ 从网络中获取数据时。它将数据设置为 _usersSharedFlow_。

```
usersSharedFlow.emit(UiState.Success(usersFromNetwork))


```

此时由于方向改变，_ViewModel_ 将被保留，我们在 _Activity_ 中的收集器将重新订阅收集。由于使用不存储任何数据的 _SharedFlow_，因此不会在此处收集任何内容。我们将不得不进行新的网络请求。

所以在这种情况下我们应该使用 _StateFlow_ 而不是 _SharedFlow_，为了避免不必要的频繁网络请求调用

##### 使用 SharedFlow 的情况

假设我们现在执行一项任务，如果该任务失败就必须显示 _SnackBar_ 提示

在我们的 _ViewModel_ 中创建一个 _SharedFlow_

```
val showSnackbarSharedFlow = MutableSharedFlow<Boolean>()


```

同样的，我们的 Activity 中有一个收集器

```
showSnackbarSharedFlow.collect {
​
}


```

现在，只要我们打开 Activity，Activity 就会订阅收集。由于使用了 SharedFlow，因此不会在此处收集任何内容

然后，当我们的 _viewModel_ 启动任务并失败的时候，它会将 _showSnackbarSharedFlow_s 设置为 true，表示我们需要显示 _Snackbar_

```
showSnackbarSharedFlow.emit(true)


```

如果方向改变，_ViewModel_ 将被保留，我们在 Activity 中的收集器将重新订阅收集。此处不会收集任何内容，因为 _SharedFlow_ 不保留最后一个值。那很好。我们不应该在方向改变时再次显示 _Snackbar_。

此时我们尝试使用 _StateFlow_ 代替 _SharedFlow_，但是如果方向改变了，_ViewModel_ 将被保留，我们在 Activity 中的收集器将重新订阅收集，因为 _StateFlow_ 保留最后一个值。它将再次显示 Snackbar，那这样就不好，我们不应该在方向改变时再次显示 _Snackbar_

所以，在这种情况下，我们应该使用 _SharedFlow_ 而不是 _StateFlow_。

> 具体什么时候使用 StateFlow，什么时候 ShardFlow, 还请大家结合自身项目和需求的特点，选择合适的即可

#### 参考资料

*   [Kotlin Flow 面试笔记](https://link.juejin.cn?target=https%3A%2F%2Fpradyotprksh4.medium.com%2Fkotlin-flow-65920759c8c2 "https://pradyotprksh4.medium.com/kotlin-flow-65920759c8c2")
*   [Kotlin 协程之一文看懂 StateFlow 和 SharedFlow](https://juejin.cn/post/7169843775240405022#heading-13 "https://juejin.cn/post/7169843775240405022#heading-13")
*   [Kotlin Flow 学习终极指南](https://link.juejin.cn?target=https%3A%2F%2Fwww.simplilearn.com%2Ftutorials%2Fkotlin-tutorial%2Fan-ultimate-guide-to-kotlin-flows "https://www.simplilearn.com/tutorials/kotlin-tutorial/an-ultimate-guide-to-kotlin-flows")