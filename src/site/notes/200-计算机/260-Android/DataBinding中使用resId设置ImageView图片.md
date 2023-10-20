---
dg-publish: true
date: 2023-09-25
tags:
  - DataBinding
---
```
class MainViewModel : ViewModel() {  
    var avatarResId = MutableLiveData(R.mipmap.bg_chinese_autumn_btn_get_normal)  
}


<ImageView  
android:layout_width="30dp"  
android:layout_height="30dp"  
android:layout_margin="4dp"  
app:imageResource="@{item.avatarResId}"/>
```
