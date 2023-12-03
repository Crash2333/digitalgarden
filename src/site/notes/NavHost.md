---
{"dg-publish":true,"permalink":"/NavHost/","tags":["JetpackCompose/导航","TODO"],"noteIcon":""}
---

[[ComposeException003 \| navController传递参数]]

```
    NavHost(  
        navController,  
        startDestination = Screen.Home.route,  
        modifier = modifier  
    ) {  
        composable(Screen.Home.route) { HomeScreen() }  
        composable(Screen.Dynamic.route) { DynamicScreen() }
        composable(Screen.Search.route) { SearchScreen() }
        composable("${Screen.WebView.route}/{${NaviConstant.URL_TYPE}}",  
            arguments = listOf(navArgument(NaviConstant.URL_TYPE) {  
                type = NavType.StringType//参数类型  
                defaultValue = UrlManager.web_url_user_agreement //默认值  
                nullable = false //是否可空  
            })) { backInfo ->  
            val url = when (backInfo.arguments?.getString(NaviConstant.URL_TYPE)) {  
                URL_TYPE_1 -> UrlManager.web_url_user_agreement  
                URL_TYPE_2 -> UrlManager.web_url_privacy_agreement  
                URL_TYPE_3 -> UrlManager.web_url_help_and_feedback  
                else -> {  
                    UrlManager.web_url_user_agreement  
                }  
            }  
            LogUtils.i("backInfo = ${backInfo.arguments.toString()}")  
            LogUtils.i("url = $url")  
            WebScreen(url, vm)  
        }
    }
```

111
```
sealed class Screen(val route: String, @StringRes val resourceId: Int) {  
  
    object Home : Screen(StringUtils.getString(R.string.navi_home), R.string.navi_home_title)
    
    object Dynamic :  Screen(StringUtils.getString(R.string.navi_dynamic), R.string.navi_dynamic_title)
    
    object Search : Screen(StringUtils.getString(R.string.navi_search), R.string.navi_search_title)
      
	object WebView : Screen(StringUtils.getString(R.string.navi_web_view), R.string.navi_web_view_title)
}
```

## 参考资料