---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/JetpackCompose/CompositionLocalProvider/","tags":["JetpackCompose/优化"],"noteIcon":""}
---



`CompositionLocalProvider` 是 Jetpack Compose 中的一个重要概念，它提供了一种在组合树中共享数据的方式。下面是一些 `CompositionLocalProvider` 的优点：

1. **局部性**: `CompositionLocalProvider` 允许您在组合树的特定子树中共享数据，而不需要显式地将数据传递给每个子组件。这使得在组合树中访问和使用共享数据变得更加方便和简洁。
    
2. **类型安全**: 您可以使用 `compositionLocalOf` 来创建特定类型的局部值，并通过 `CompositionLocalProvider` 将其提供给子组件。这种类型安全的方式确保了在组合树中正确使用和获取共享数据，避免了类型错误和运行时异常。
    
3. **动态更新**: 当通过 `CompositionLocalProvider` 提供的局部值发生更改时，使用该值的组件会自动重新计算并重新渲染。这样，您可以轻松地在应用程序中共享和更新状态，并确保 UI 及时反映最新的数据。
    
4. **封装和解耦**: 使用 `CompositionLocalProvider` 可以将共享数据的创建和提供逻辑封装在一个地方，从而将其与组件的实现和用途解耦。这提供了更好的代码组织和可维护性，并使您的代码更具可测试性。

## 代码
```
private val LocalViewModel = compositionLocalOf<HomeViewModel> { error("No init!") }  
private val LocalViewState = compositionLocalOf<HomeViewState> { error("No init!") }  
private val LocalNavController = compositionLocalOf<NavHostController> { error("No init!") }


@Composable  
fun ThisApp(  
    navController: NavHostController,  
    vm: HomeViewModel = viewModel(),  
    onBackPressedDispatcher: OnBackPressedDispatcher,   
) {  
    CompositionLocalProvider(  
        LocalViewModel provides vm, 
        LocalViewState provides vm.viewStates,  
        LocalNavController provides navController,  
    ) {  
        homeView(navController)  
    }  
}
```

## 参考资料