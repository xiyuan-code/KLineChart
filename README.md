# KLineChart

Android仿火币K线图实现（包含MA,BOLL,MACD,KDJ,RSI,WR指标）

本项目是在 [tifezh的KChartView](https://github.com/tifezh/KChartView) 基础上进行修改的，新增了KDJ和WR指标，对UI展示进行了修改。

![](https://github.com/fujianlian/KLineChart/tree/master/img/1.png) 
 
![](https://github.com/fujianlian/KLineChart/tree/master/img/2.png) 

![](https://github.com/fujianlian/KLineChart/tree/master/img/3.png) 

## 配置使用

```xml
<com.github.fujianlian.klinechart.KLineChartView
    android:id="@+id/kLineChartView"
    android:layout_width="match_parent"
    android:layout_height="match_parent" />
```

主图和附图初始化
```java
// KLineChartView
private void initView() {
    ...
    // 依次添加副图子视图
    addChildDraw(mMACDDraw);
    addChildDraw(mKDJDraw);
    addChildDraw(mRSIDraw);
    addChildDraw(mWRDraw);
    // 设置成交量视图
    setVolDraw(mVolumeDraw);
    // 设置主视图
    setMainDraw(mMainDraw);
}
```
BaseKLineChartView
```java
// 主图显示隐藏调用
public void changeMainDrawType(Status status) {
    if (mainDraw != null && mainDraw.getStatus() != status) {
        mainDraw.setStatus(status);
        invalidate();
    }
}

// 主视图当前子视图
public enum Status {
    MA, BOLL, NONE
}

// 设置子视图，position依据初始化添加先后顺序下标
public void setChildDraw(int position) {
        if (mChildDrawPosition != position) {
            if (!isShowChild) {
                isShowChild = true;
                initRect();
            }
            mChildDraw = mChildDraws.get(position);
            mChildDrawPosition = position;
            isWR = position == 5;
            invalidate();
        }
    }

// 子视图隐藏
public void hideChildDraw() {
        mChildDrawPosition = -1;
        isShowChild = false;
        mChildDraw = null;
        initRect();
        invalidate();
    }
```

## 具体使用参照KLineChartDemo

