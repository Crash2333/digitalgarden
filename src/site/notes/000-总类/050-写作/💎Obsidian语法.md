---
{"dg-publish":true,"permalink":"/000-总类/050-写作/💎Obsidian语法/","tags":["Obsidian/Syntax"],"noteIcon":""}
---


## 超链接
Obsidian 支持多种「超链接语法」[^1]，这些功能也是「现代笔记管理」的必备技能。几种常见的语法如下（都是基于双向链接进行拓展）：
>- [[000-总类/050-写作/💎Obsidian语法#双向链接 \|双向链接]]：`[[NoteName]]`
>- [[💎Obsidian话题引用 \|话题引用]]：`[[NoteName #header]]`
>- [[000-总类/050-写作/💎Obsidian语法#别名引用\|别名引用]] ：`[[NoteName |Alias]]`
>- [[Obsidian嵌入引用#^e4a652\|嵌入引用]]：`！[[NoteName]]`
>- [[000-总类/050-写作/💎Obsidian块引用\|块引用]]：`[[NoteName ^]]`
## 标签
```
tags: [maintag/subtag]
```
`maintag`是主标签，`subtag`是子标签。


## 别名引用
```
[[NoteName |Alias]]
```
给[[000-总类/050-写作/💎Obsidian语法#双向链接\|双向链接]]起个别名，使表达更加准确

## 双向链接
「双向链接」指的是在笔记 A 中通过输入 `[[笔记 B]]` 后，使得笔记 A 和笔记 B 建立了链接关系


## 嵌入视频
Obsidian是支持使用iframe标签嵌入视频的
- B站的iframe分享链接开头没有https，需要手动补齐
- B站的iframe标签没有设置视频宽高，需要手动设置
`width="900" height="500" `

```html
<iframe src="https://player.bilibili.com/player.html?aid=12386776&bvid=BV1Hx411i74i&cid=20399296&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>
```

<iframe src="https://player.bilibili.com/player.html?aid=12386776&bvid=BV1Hx411i74i&cid=20399296&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true" width="900" height="500" > </iframe>


## 参考资料
- [标签的使用 - Obsidian 中文帮助](https://publish.obsidian.md/help-zh/%E4%BD%BF%E7%94%A8%E6%8C%87%E5%8D%97/%E6%A0%87%E7%AD%BE%E7%9A%84%E4%BD%BF%E7%94%A8)

[^1]:在Obsidian中，对双向链接使用技巧的统称。本质上还是双向链接