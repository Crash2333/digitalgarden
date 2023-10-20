---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/PropertyAnimation/","noteIcon":""}
---

## 属性动画
### 1. setDuration(int duration) 设置动画时长
 #TODO 示例代码

### 2. setInterpolator(Interpolator interpolator) 设置 Interpolator
[[200-计算机/260-Android/Interpolator\|Interpolator]]
 #TODO 示例代码

### 3. 设置监听器
#### 3.1 ViewPropertyAnimator.setListener() / ObjectAnimator.addListener()
这两个方法的名称不一样，可以设置的监听器数量也不一样，但它们的参数类型都是 `AnimatorListener`，所以本质上其实都是一样的。 `AnimatorListener` 共有 4 个回调方法：

##### 3.1.1 onAnimationStart(Animator animation)

当动画开始执行时，这个方法被调用。

##### 3.1.2 onAnimationEnd(Animator animation)

当动画结束时，这个方法被调用。

##### 3.1.3 onAnimationCancel(Animator animation)

当动画被通过 `cancel()` 方法取消时，这个方法被调用。

需要说明一下的是，就算动画被取消，`onAnimationEnd()` 也会被调用。所以当动画被取消时，如果设置了 `AnimatorListener`，那么 `onAnimationCancel()` 和 `onAnimationEnd()` 都会被调用。`onAnimationCancel()` 会先于 `onAnimationEnd()` 被调用。

##### 3.1.4 onAnimationRepeat(Animator animation)
当动画通过 `setRepeatMode()` / `setRepeatCount()` 或 `repeat()` 方法重复执行时，这个方法被调用。

由于 `ViewPropertyAnimator` 不支持重复，所以这个方法对 `ViewPropertyAnimator` 相当于无效。

#### 3.2 ViewPropertyAnimator.setUpdateListener() / ObjectAnimator.addUpdateListener()

和上面 3.1 的两个方法一样，这两个方法虽然名称和可设置的监听器数量不一样，但本质其实都一样的，它们的参数都是 `AnimatorUpdateListener`。它只有一个回调方法：`onAnimationUpdate(ValueAnimator animation)`。

##### 3.2.1 onAnimationUpdate(ValueAnimator animation)

当动画的属性更新时（不严谨的说，即每过 10 毫秒，动画的完成度更新时），这个方法被调用。

方法的参数是一个 `ValueAnimator`，`ValueAnimator` 是 `ObjectAnimator` 的父类，也是 `ViewPropertyAnimator` 的内部实现，所以这个参数其实就是 `ViewPropertyAnimator` 内部的那个 `ValueAnimator`，或者对于 `ObjectAnimator` 来说就是它自己本身。

`ValueAnimator` 有很多方法可以用，它可以查看当前的动画完成度、当前的属性值等等。不过 `ValueAnimator` 是下一期才讲的内容，所以这期就不多说了。
