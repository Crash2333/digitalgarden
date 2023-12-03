---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/JetpackCompose/Indicator/","tags":["JetpackCompose/布局组件"],"noteIcon":""}
---

## 圆角矩形指示器
>只有选中的tab显示圆角矩形
```
@OptIn(ExperimentalFoundationApi::class)  
@Composable  
fun PagerTabIndicator(  
    tabPositions: List<TabPosition>,  
    pagerState: PagerState,  
    color: Color = Color.Blue,  
    @FloatRange(from = 0.0, to = 1.0) percent: Float = 0.6f,  
    height: Dp = 5.dp,  
) {  
    val currentPage by rememberUpdatedState(newValue = pagerState.currentPage)  
    val fraction by rememberUpdatedState(newValue = pagerState.currentPageOffsetFraction)  
    val currentTab = tabPositions[currentPage]  
    val previousTab = tabPositions.getOrNull(currentPage - 1)  
    val nextTab = tabPositions.getOrNull(currentPage + 1)  
    Canvas(  
        modifier = Modifier.fillMaxSize(),  
        onDraw = {  
  
            val indicatorWidth = currentTab.width.toPx() * percent  
            val indicatorOffset = if (fraction > 0 && nextTab != null) {  
                lerp(currentTab.left, nextTab.left, fraction).toPx()  
            } else if (fraction < 0 && previousTab != null) {  
                lerp(currentTab.left, previousTab.left, -fraction).toPx()  
            } else {  
                currentTab.left.toPx()  
            }  
  
            val canvasHeight = size.height  
            drawRoundRect(  
                color = color,  
                topLeft = Offset(  
                    indicatorOffset + (currentTab.width.toPx() * (1 - percent) / 2),  
                    canvasHeight - height.toPx()  
                ),  
                size = Size(indicatorWidth + indicatorWidth * Math.abs(fraction), height.toPx()),  
                cornerRadius = CornerRadius(50f)  
            )  
        }  
    )  
}
```


## 多选一指示器
>每个tab都有一个指示器，被选中的显示指定颜色
```
@OptIn(ExperimentalFoundationApi::class)  
@Composable  
fun PagerTabIndicator2(  
    tabPositions: List<TabPosition>,  
    pagerState: PagerState,  
    selectedColor: Color = Color.Blue,  
    unselectedColor: Color = Color.Gray,  
    indicatorWidth: Dp = 50.dp,  
    height: Dp = 5.dp,  
    spacing: Dp = 8.dp,  
) {  
    val selectedTabIndex = pagerState.currentPage  
  
    Row(  
        modifier = Modifier  
            .wrapContentWidth(Alignment.CenterHorizontally)  
            .height(height)  
    ) {  
        tabPositions.forEachIndexed { index, tabPosition ->  
            val isSelected = index == selectedTabIndex  
            val color = if (isSelected) selectedColor else unselectedColor  
  
            Box(  
                modifier = Modifier  
                    .width(indicatorWidth)  
                    .height(height)  
                    .background(color)  
            )  
  
            if (index < tabPositions.size - 1) {  
                Spacer(modifier = Modifier.width(spacing))  
            }  
        }  
    }}
```


## 参考资料
[Jetpack Compose TabRow与HorizontalPager 联动 - 掘金](https://juejin.cn/post/7239630585500155961)
[Jetpack Compose实现滑块式标签tab - 掘金](https://juejin.cn/post/7188357337294307389?from=search-suggest)