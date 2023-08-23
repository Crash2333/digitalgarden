---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/Java/String、StringBuffer、StringBuilder 的区别？/","noteIcon":""}
---


## 可变性
- `String` 是不可变的（后面会详细分析原因）。
- `StringBuilder` 与 `StringBuffer`是可变的(`append`方法修改字符串)

## 线程安全性
- `String` 中的对象是不可变的，也就可以理解为常量，线程安全。
- `StringBuffer` 对方法加了同步锁或者对调用的方法加了同步锁，所以是线程安全的。
- `StringBuilder` 并没有对方法进行加同步锁，所以是**非线程安全的**


