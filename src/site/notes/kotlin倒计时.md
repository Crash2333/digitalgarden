---
dg-publish: true
date: 2023-09-26
tags:
  - koltin
  - Android
---
```
var TotalTime : Long = 2*60*60*1000 //总时长 2小时
    var countDownTimer=object : CountDownTimer(TotalTime,1000){//1000ms运行一次onTick里面的方法
        override fun onFinish() {
            Log.d(TAG,"==倒计时结束")
        }

        override fun onTick(millisUntilFinished: Long) {
            var hour=millisUntilFinished/1000/60/60
            var minute=millisUntilFinished/1000/60%60
            var second=millisUntilFinished/1000%60
            Log.d(TAG,"==倒计时"+hour+"小时"+minute+"分"+second+"秒")
        }
    }.start()
```
## 参考资料
[kotlin——倒计时（CountDownTimer和flow形式）_kotlin 倒计时-CSDN博客](https://blog.csdn.net/wy313622821/article/details/105454665)