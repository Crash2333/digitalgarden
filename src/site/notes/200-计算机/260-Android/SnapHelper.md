---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/SnapHelper/","tags":["Android/RecyclerView"],"noteIcon":""}
---

## LinearSnapHelper
>使当前Item居中显示，常用场景是横向的RecyclerView, 类似ViewPager效果，但是又可以快速滑动多个条目。

### LinearSnapHelper获取居中的item
>LinearSnapHelper的作用就是让RecyclerView滚动停止时相应的 Item 停留中间位置。正常情况下，我们还需要知道居中item在Adapter中的position。用来进行一些其他操作。下面的api可以拿到居中item对应的View，再调用getChildAdapterPosition即可拿到position。
```Kotlin
recyclerView.addOnScrollListener(object : RecyclerView.OnScrollListener() {
    override fun onScrolled(recyclerView: RecyclerView, dx: Int, dy: Int) {
        super.onScrolled(recyclerView, dx, dy)
        var targetView = lsHelper.findSnapView(layoutManager)
        targetView?.let {
            val targetPosition = recyclerView.getChildAdapterPosition(it)
            Logcat.e("targetPosition :$targetPosition")
            itemList.forEach { item ->
                item.isSelect = false
            }
            itemList[targetPosition].isSelect = true
            adapter.notifyDataSetChanged()
            val value = itemList[targetPosition].temp
            if (!tempIsSame(value)) {
                listener.onTemperatureChange(value)
            }
        }
    }
})
```

### 用法
```java
LinearLayoutManager manager = new LinearLayoutManager(getContext());
manager.setOrientation(LinearLayoutManager.VERTICAL);
mRecyclerView.setLayoutManager(manager);
LinearSnapHelper snapHelper = new LinearSnapHelper();
snapHelper.attachToRecyclerView(mRecyclerView);
```

## PagerSnapHelper
>使RecyclerView 像ViewPager一样的效果，每次只能滑动一页。


### 用法
```java
LinearLayoutManager linearLayoutManager = new LinearLayoutManager(this);
linearLayoutManager.setOrientation(LinearLayoutManager.HORIZONTAL);
mRecycleview.setLayoutManager(linearLayoutManager);
PagerSnapHelper snapHelper = new PagerSnapHelper();
snapHelper.attachToRecyclerView(mRecycleview);
```



## 参考资料
[RecyclerView + SnapHelper实现炫酷ViewPager效果 - 简书](https://www.jianshu.com/p/f23f6271a074)
[完美解决：RecyclerViwe中使用SnapHelper报错：“An instance of OnFlingListener already set.” - 简书](https://www.jianshu.com/p/7dcc82d593b5)