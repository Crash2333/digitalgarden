---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/RecyclerView的item居中显示/","tags":["RecyclerView/ItemDecoration"],"noteIcon":""}
---


## 调用
```
//注意这里传的参数都是dp，宽度要和xml中的保持一致
recyclerView.addItemDecoration(GridSpaceDecoration(8, prizeAdapter.list.size, ConvertUtils.dp2px(296f), ConvertUtils.dp2px(68f)))


```

## Decoration

```
class GridSpaceDecoration : RecyclerView.ItemDecoration {  
  
    //间距  
    private var mSpace = 0  
  
    //列表item的总个数  
    private var mTotalCount = 0  
  
    //recyclerView的宽度  
    private var mTotalWidth = 0  
  
    //每个item的宽度  
    private var mItemWidth = 0  
  
    constructor(mSpace: Int, mTotalCount: Int, mTotalWidth: Int, mItemWidth: Int) : super() {  
        this.mSpace = mSpace  
        this.mTotalCount = mTotalCount  
        this.mTotalWidth = mTotalWidth  
        this.mItemWidth = mItemWidth  
    }  
  
  
    override fun getItemOffsets(  
        outRect: Rect, view: View, parent: RecyclerView, state: RecyclerView.State  
    ) {  
        super.getItemOffsets(outRect, view, parent, state)  
        val layoutManager = parent.layoutManager as GridLayoutManager  
        //获取每行的个数  
        val spanCount: Int = layoutManager.spanCount  
        //获取当前位置  
        val position = parent.getChildAdapterPosition(view)  
        //当前列  
        val column = position % spanCount  
        //计算垂直方向上的间距，当不是首行时  
        if (position >= spanCount) {  
            //添加垂直方向上的间距  
            outRect.top = mSpace  
        }  
  
        //获取左边距  
        val leftMargin = getLeftMargin(position, spanCount)  
        outRect.left = column * mSpace / spanCount + leftMargin  
        outRect.right = mSpace - (column + 1) * mSpace / spanCount  
  
    }  
  
    override fun onDraw(c: Canvas, parent: RecyclerView, state: RecyclerView.State) {  
        super.onDraw(c, parent, state)  
  
    }  
  
    /**  
     * 根据位置，判断在第几行，0，1，2，3  
     */    private fun getRow(position: Int, spanCount: Int): Int {  
        return position / spanCount  
    }  
  
    /**  
     * 返回第N行会有多少个元素  
     */  
    private fun getRowCount(row: Int, spanCount: Int): Int {  
        return if ((row + 1) * spanCount <= mTotalCount) {  
            spanCount  
        } else {  
            mTotalCount - row * spanCount  
        }  
    }  
  
    /**  
     * 获取左侧的边距  
     */  
    private fun getLeftMargin(position: Int, spanCount: Int): Int {  
        //判断是第几行  
        val row = getRow(position, spanCount)  
        //该行有多少个元素  
        val rowCount = getRowCount(row, spanCount)  
        //如果该行元素都满了  
        return if (rowCount == spanCount) {  
            0  
        } else {  
            (mTotalWidth - (rowCount * mItemWidth + (rowCount - 1) * mSpace)) / 2  
        }  
    }  
  
}
```

## 参考资料
[RecyclerView + ItemDecoration 实现item布局居中 - 简书](https://www.jianshu.com/p/4aa37b69134d)