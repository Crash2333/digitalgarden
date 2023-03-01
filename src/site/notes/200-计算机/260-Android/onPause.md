---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/onPause/","tags":["TODO"],"noteIcon":""}
---

失去焦点，正在停止，此时可做一些存储数据、停止动画等工作，但不能太耗时，因为这会影响到新 Activity 的显示，onPause 必须先执行完，新 Activity 的 onResume 才会执行