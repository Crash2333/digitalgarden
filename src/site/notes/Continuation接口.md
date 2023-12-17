---
{"dg-publish":true,"permalink":"/Continuation接口/","tags":["kotlin/协程"],"noteIcon":""}
---


## 
```
#Continuation.kt

public interface Continuation<in T> {  
    /**  
     *  协程上下文    
     * The context of the coroutine that corresponds to this continuation.
     * 
     * */    
     public val context: CoroutineContext  
  
    /**  
     * 恢复协程
     * Resumes the execution of the corresponding coroutine 
     * passing a successful or failed result as the return value of the last suspension point.
     * */    
     public fun resumeWith(result: Result<T>)  
}

//创建协程的函数
public fun <T> (suspend () -> T).createCoroutine(  
    completion: Continuation<T>  
): Continuation<Unit> =  
	//看这里createCoroutineUnintercepted
    SafeContinuation(createCoroutineUnintercepted(completion).intercepted(), COROUTINE_SUSPENDED)
    
//启动协程的函数 
public inline fun <T> Continuation<T>.resume(value: T): Unit = resumeWith(Result.success(value))

```

### suspendCoroutineUninterceptedOrReturn
```
#Continuation.kt

psuspend inline fun <T> suspendCoroutine(crossinline block: (Continuation<T>) -> Unit): T {
    contract { callsInPlace(block, InvocationKind.EXACTLY_ONCE) }
    return suspendCoroutineUninterceptedOrReturn { c: Continuation<T> ->
        //传入的c 为父协程的协程体
        //c.intercepted() 为检测拦截器，demo里没有拦截器用自身，也就是c
        val safe = SafeContinuation(c.intercepted())
        //执行函数，也就是子协程体
        block(safe)
        //检测返回值
        safe.getOrThrow()
    }

```

### 
```
#IntrinsicsJvm.kt 

public actual fun <R, T> (suspend R.() -> T).createCoroutineUnintercepted( 
	receiver: R, 
	completion: Continuation<T>
 )

//创建协程的时候会调用该函数
public actual fun <T> (suspend () -> T).createCoroutineUnintercepted( 
	completion: Continuation<T> 
): Continuation<Unit>

```

## 参考资料