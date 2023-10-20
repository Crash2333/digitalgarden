---
dg-publish: true
date: 2023-09-19
tags:
  - Github
  - TODO
---

## 加载圆形头像
```
//加载头像  
Glide.with(context)
	.load(url)
	.transform(CircleCrop())  
    .into(binding.ivAvatar)
```

## 参考资料
[Glide v4 : Fast and efficient image loading for Android](https://bumptech.github.io/glide/)