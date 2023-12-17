---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/JetpackCompose/ComposeBaseViewModel/","tags":["JetpackCompose/ViewModel"],"noteIcon":""}
---



```
/**  
 * 没有定义方法。主要用于接收参数，面向对象中多态的一种实践  
 */
interface UiState
interface UiIntent
```

## IViewModelHandle
```
interface IViewModelHandle<S : UiState, I : UiIntent> {  
    fun handleEvent(event: I, state: S)  
}
```
## ComposeBaseViewModel

```
abstract class ComposeBaseViewModel<S : UiState, I : UiIntent>(viewState: S) :  
    IViewModelHandle<S, I>,  
    ViewModel() {  
  
    private val intentChannel = Channel<I>(Channel.UNLIMITED)  
  
    var viewStates by mutableStateOf(viewState)  
        protected set  
  
    init {  
        handleIntent()  
    }  
  
  
    private fun handleIntent() {  
        viewModelScope.launch(Dispatchers.IO) {  
            intentChannel.consumeAsFlow().collect {  
                handleEvent(it, viewStates)  
            }  
        }    }  
  
    /**  
     * 发送意图  
     */  
    fun sendIntent(viewIntent: I) {  
        viewModelScope.launch(Dispatchers.IO) {  
            intentChannel.send(viewIntent)  
        }  
    }  
  
    /**  
     * 更新意图  
     */  
    fun S.update(content: S.() -> S) {  
        viewStates = content.invoke(this@update)  
    }  
  
}
```

## 参考资料

[JetpackCompose实践-MVI业务开发 | 经验分享 - 掘金](https://juejin.cn/post/7258469240733433917)