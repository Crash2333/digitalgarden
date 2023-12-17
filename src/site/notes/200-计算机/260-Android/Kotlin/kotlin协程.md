---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/Kotlin/kotlin协程/","tags":["kotlin/协程"],"noteIcon":""}
---

协程就是用闭包伪装起来的线程间回调。

[[Continuation接口\|Continuation接口]]
[[withContext\|withContext]]
[[200-计算机/260-Android/Kotlin/挂起函数\|挂起函数]]

### ViewModel中拉起协程

```
viewModelScope.launch {
}
```


### launch函数的实现
>launch是CoroutineScope类的扩展函数

```
#Builders.common.kt
public fun CoroutineScope.launch(
    context: CoroutineContext = EmptyCoroutineContext,
    start: CoroutineStart = CoroutineStart.DEFAULT,
    block: suspend CoroutineScope.() -> Unit
): Job {
    //构造新的上下文
    val newContext = newCoroutineContext(context)
    //构造completion
    val coroutine = if (start.isLazy)
        LazyStandaloneCoroutine(newContext, block) else
        StandaloneCoroutine(newContext, active = true)
    //开启协程
    coroutine.start(start, coroutine, block)
    return coroutine
}

```


[[CoroutineContext\|CoroutineContext]]
#### newCoroutineContext
```
#CoroutineContext.kt

actual fun CoroutineScope.newCoroutineContext(context: CoroutineContext): CoroutineContext {
    //在Demo 环境里 coroutineContext = EmptyCoroutineContext
    val combined = coroutineContext + context
    //DEBUG = false
    val debug = if (DEBUG) combined + CoroutineId(COROUTINE_ID.incrementAndGet()) else combined
    //没有指定分发器，默认使用的分发器为：Dispatchers.Default
    //若是指定了分发器，就用指定的
    return if (combined !== Dispatchers.Default && combined[ContinuationInterceptor] == null)
        debug + Dispatchers.Default else debug
}

```



```
#BuildersKt

private class LazyStandaloneCoroutine(  
    parentContext: CoroutineContext,  
    block: suspend CoroutineScope.() -> Unit  
) : StandaloneCoroutine(parentContext, active = false) {  
	//创建协程
    private val continuation = block.createCoroutineUnintercepted(this, this)  
  
    override fun onStart() {  
	    //看这里
        continuation.startCoroutineCancellable(this)  
    }  
}
```


### 协程的最终调用
```
#CoroutineStart.kt

public operator fun <T> invoke(block: suspend () -> T, completion: Continuation<T>): Unit =  
    when (this) {  
        DEFAULT -> block.startCoroutineCancellable(completion)  
        ATOMIC -> block.startCoroutine(completion)  
        UNDISPATCHED -> block.startCoroutineUndispatched(completion)  
        LAZY -> Unit // will start lazily  
    }
```

## 创建&调用协程

```
fun <T> launchFish(block: suspend () -> T) { 
	//创建协程，返回值为SafeContinuation(实现了Continuation 接口) 
	//入参为Continuation 类型，参数名为completion，顾名思义就是 
	//协程结束后(正常返回&抛出异常）将会调用它。 
	var coroutine = block.createCoroutine(object : Continuation<T> { 
		override val context: CoroutineContext get() = EmptyCoroutineContext 
		
			//协程结束后调用该函数 
			override fun resumeWith(result: Result<T>) {
				println("result:$result") 
			} 
		}
	)
	//开启协程 
	coroutine.resume(Unit) 
}

```

>定义了函数launchFish，该函数唯一的参数为函数类型参数，被suspend 修饰，而(suspend () -> T)定义一系列扩展函数，createCoroutine 为其中之一，因此block 可以调用createCoroutine。  
createCoroutine 返回类型为SafeContinuation，通过SafeContinuation.resume()开启协程。



```
fun main(array: Array<String>) { 
	launchFish { 
		println("I am coroutine") 
	}
 }

//打印结果
I am coroutine
result:Success(kotlin.Unit)
```


## 参考资料
[一个小故事讲明白进程、线程、Kotlin 协程到底啥关系？ - 掘金](https://juejin.cn/post/7108651566806073380)