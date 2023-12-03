---
{"dg-publish":true,"permalink":"/TabRow/","tags":["JetpackCompose/布局组件"],"noteIcon":""}
---


用于创建标签式导航栏。
`TabRow`通常与`Tab`一起使用，可以在水平方向上显示多个标签，并允许用户通过点击标签来切换内容。

```
TabRow(
	selectedTabIndex = pagerState.currentPage,  
    modifier = Modifier  
        .background(Color(ColorUtils.getColor(R.color.black_transparency_90)))  
        .height(20.dp)  
        .width(192.dp),  
    //指示器样式,自定义指示器
    indicator = { tabPositions ->  
        PagerTabIndicator(  
            tabPositions = tabPositions,  
            pagerState = pagerState,  
            percent = 0.3f,  
            color = Color.Transparent,  
            height = 2.dp  
        )  
    },  
    containerColor = Color.Transparent,  
    divider = {  
        //处理分割线  
        Divider(thickness = 1.dp, color = Color.Transparent)  
    }) {  
    items.forEachIndexed { index, _ ->  
        Tab(modifier = Modifier.height(20.dp),  
            selected = index == pagerState.currentPage,  
            onClick = {  
                coroutineScope.launch {  
                    pagerState.animateScrollToPage(index)  
                }  
            }) {  
            Text(text = items[index], fontSize = 12.sp, color = Color.White)  
        }  
  
    }
}
```


## 参考资料