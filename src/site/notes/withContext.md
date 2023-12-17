---
{"dg-publish":true,"permalink":"/withContext/","tags":["kotlin/协程"],"noteIcon":""}
---

使用`withContext`来**切换线程**用以执行新的协程(子协程)，而原来的协程(父协程)则被**挂起**。
当子协程执行完毕后将会恢复父协程的运行。

## 源码
withContext 被[[200-计算机/260-Android/Kotlin/挂起函数#源码\| suspend]]修饰，而suspend 修饰的函数会默认带一个Continuation类型的形参，这样就能关联起来了：

> [[Continuation接口#suspendCoroutineUninterceptedOrReturn\| suspendCoroutineUninterceptedOrReturn]] 传入的uCount 实参即为父协程的协程体。

将父协程的协程体存储到DispatchedCoroutine里，最后通过DispatchedCoroutine 分发。


```
#Builders.common.kt 

suspend fun <T> withContext( 
	context: CoroutineContext, 
	block: suspend CoroutineScope.() -> T 
): T { 
	return suspendCoroutineUninterceptedOrReturn sc@ { uCont -> 
		val oldContext = uCont.context val newContext = oldContext + context 
		//... //构造分发的协程 
		val coroutine = DispatchedCoroutine(newContext, uCont) 
		//开启协程 
		block.startCoroutineCancellable(coroutine, coroutine) 
		//获取协程结果 
		coroutine.getResult() 
	} 
}

```



```
#DispatchedCoroutine类里

fun getResult(): Any? {
    //先判断是否需要挂起
    if (trySuspend()) return COROUTINE_SUSPENDED
    //如果无需挂起，说明协程已经执行完毕
    //那么需要将返回值返回
    val state = this.state.unboxState()
    if (state is CompletedExceptionally) throw state.cause
    //强转返回值到对应的类型
    return state as T
}

private fun trySuspend(): Boolean {
    //_decision 原子变量，三种值可选
    //private const val UNDECIDED = 0 默认值，未确定是1还是2
    //private const val SUSPENDED = 1 挂起
    //private const val RESUMED = 2   恢复
    _decision.loop { decision ->
        when (decision) {
            //若当前值为默认值，则修改为挂起，并且返回ture，表示需要挂起
            UNDECIDED -> if (this._decision.compareAndSet(UNDECIDED, SUSPENDED)) return true
            //当前已经是恢复状态，无需挂起，返回false
            RESUMED -> return false
            else -> error("Already suspended")
        }
    }
}

```

也就是说当调用了coroutine.getResult() 后，该函数执行的返回值即为 suspendCoroutineUninterceptedOrReturn 的返回值，进而是withContext 的返回值。

此时withContext 的返回值为：COROUTINE_SUSPENDED，它是个枚举值，表示协程执行到该函数需要挂起协程，也即是调用了withContext()函数的协程需要被挂起。

### 小结挂起逻辑：

> 1. withContext()函数记录当前调用它的协程，并开启一个新的协程。
> 2. 开启的新协程在指定的线程执行（提交给线程池或是提交给主线程执行任务）。
> 3. 判断新协程当前的状态，若是挂起则返回挂起状态，若是恢复状态则返回具体的返回值。

### 小结withContext()函数恢复父协程的原理：

> 1. 调用withContext()时传入父协程的协程体。
> 2. 当withContext()的协程体执行完毕后会判断completion。
> 3. completion 即为1的协程体包装类：DispatchedCoroutine。
> 4. completion.resumeWith() 最后执行invokeSuspend()，通过状态机流转执行之前挂起逻辑之后的代码。
> 5. 整个父协程体就执行完毕了


## 参考资料