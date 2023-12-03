---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/JetpackCompose/HorizontalPager/","tags":["JetpackCompose/布局组件"],"noteIcon":""}
---

水平分页组件
```
val items = listOf("礼物", "特权", "背包")  
val coroutineScope = rememberCoroutineScope()  
val pagerState = rememberPagerState(  
    pageCount = { items.size },  
)

 HorizontalPager(  
        state = pagerState, modifier = Modifier  
//            .height(216.dp)  
            .fillMaxWidth()  
//            .fillMaxSize()  
    ) { index ->  
        when (index) {  
            0 -> {  
                GiftListNormal(giftList)  
            }  
  
            1 -> {  
                GiftListSpecial(specialGiftList)  
            }  
  
            2 -> {  
                GiftListBackpack(bagList)  
            }  
        }  
  
    }
```


## 参考资料