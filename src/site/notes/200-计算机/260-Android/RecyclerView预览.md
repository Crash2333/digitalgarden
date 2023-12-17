---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/RecyclerView预览/","tags":["Android/RecyclerView"],"noteIcon":""}
---


```
<androidx.recyclerview.widget.RecyclerView  
    android:id="@+id/rv_select"  
    android:layout_width="match_parent"  
    android:layout_height="26dp"  
    android:orientation="horizontal"  
    app:layoutManager="androidx.recyclerview.widget.LinearLayoutManager"  
    tools:itemCount="5"  
    tools:listitem="@layout/item_island_buy_select" />
```

- itemCount：预览的item数量
- listitem：预览的item样式布局
- orientation：列表的排列方向
- layoutManager：预览时使用的布局管理器
## 参考资料