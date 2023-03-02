---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/View事件分发/","tags":["Android/View"],"noteIcon":""}
---

## dispatchTouchEvent
**MotionEvent**事件分发，返回true表示不下发事件被消费，返回false表示继续下发
## onInterceptTouchEvent
**MotionEvent**事件拦截，返回true表示事件被拦截，返回false表示不处理事件。继续分发。
## onTouchEvent
**MotionEvent**事件消费，返回true表示事件被消费，返回false表示不处理事件。继续分发。


## 参考资料
[安卓自定义View进阶-事件分发机制详解](https://www.gcssloop.com/customview/dispatch-touchevent-source.html)
[安卓自定义View进阶-事件分发机制原理](https://www.gcssloop.com/customview/dispatch-touchevent-theory.html)