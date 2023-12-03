---
{"dg-publish":true,"permalink":"/BottomNavigation/","tags":["TODO","JetpackCompose/导航"],"noteIcon":""}
---



```
data class NavigationItem(  
    val title: String,  
    val iconSelect: Int,  
    val iconUnSelect: Int,  
)
```


```
@Composable  
fun navigationBar(  
    items: List<NavigationItem>,  
    selectedIndex: MutableState<Int>,  
    onItemClick: (Int) -> Unit,  
    modifier: Modifier = Modifier,  
    cornerRadius: Dp = 0.dp,  
) {  
    val gradientBrush =  
        Brush.verticalGradient(colors = listOf(Color(0xFFF0E9FF), Color(0xFFFFFFFF)))  
    Row(  
        modifier = modifier  
            .background(  
                brush = gradientBrush, shape = RoundedCornerShape(  
                    cornerRadius,  
                    cornerRadius,  
                    0.dp,  
                    0.dp,  
                )  
            )  
            .height(84.dp)  
            .fillMaxWidth(),  
        horizontalArrangement = Arrangement.SpaceEvenly,  
        verticalAlignment = Alignment.CenterVertically  
    ) {  
        items.forEachIndexed { index, item ->  
            navigationBarItem(  
                iconSelect = item.iconSelect,  
                iconUnSelect = item.iconUnSelect,  
                label = item.title,  
                selected = index == selectedIndex.value,  
                onClick = { onItemClick(index) },  
                modifier = Modifier.weight(1f)  
            )  
        }  
  
    }
}
```