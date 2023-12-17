---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/JetpackCompose/NavHost/","tags":["JetpackCompose/导航","TODO"],"noteIcon":""}
---

[[ComposeException003 \| navController传递参数]]

```
    NavHost(  
        navController,  
        startDestination = "${Screen.Home.route}/{${NaviConstant.BACK_TO_HOME}}",
        modifier = modifier  
    ) {  
        composable(  
		    "${Screen.Home.route}/{${NaviConstant.BACK_TO_HOME}}",  
		    arguments = listOf(navArgument("${NaviConstant.BACK_TO_HOME}") {  
		        type = NavType.StringType//参数类型  
		        defaultValue = "" //默认值  
		        nullable = false //是否可空  
		    })  
		) { backInfo ->  
		    val fromRouter = backInfo.arguments?.getString("${NaviConstant.BACK_TO_HOME}")  
		    when (fromRouter) {  
		        Screen.Home.route -> {  
		            //重置信息  
		            vm.sendIntent(HomeViewIntent.RoomId(""))  
		            vm.sendIntent(HomeViewIntent.RoomPwd(""))  
		        }  
		    }  
		    LogUtils.i("fromRouter = $fromRouter")  
		    HomeRoute(vm, liveRoomViewModel, mainViewModel)  
		}
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