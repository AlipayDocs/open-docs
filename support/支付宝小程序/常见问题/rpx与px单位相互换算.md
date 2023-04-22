## acss样式单位换算原理
详情可查看 [acss样式](https://opendocs.alipay.com/mini/framework/acss)。

### rpx根据屏幕宽度自适应
rpx（responsive pixel）可以根据屏幕宽度进行自适应，规定屏幕宽为 750rpx。以 Apple iPhone6 为例，屏幕宽度为 375px，共有 750 个物理像素，则 750rpx = 375px = 750 物理像素，1rpx = 0.5px = 1 物理像素。

| 设备 | rpx 换算 px（屏幕宽度 / 750） | px 换算 rpx（750 / 屏幕宽度） |
| --- | --- | --- |
| iPhone5 | 1rpx = 0.42px | 1px = 2.34rpx |
| iPhone6 | 1rpx = 0.5px | 1px = 2rpx |
| iPhone6 Plus | 1rpx = 0.552px | 1px = 1.81rpx |


### rpx 自动转换成 px 或 rem
通过 acss 设置的样式转成 rem，通过 style 设置的样式转成 px。

## ![](https://gw.alipayobjects.com/zos/sptworksff_prod/de12e9c3-d1f2-4e2e-aa8f-56bc8df566c4.jpg#align=left&display=inline&height=165&margin=%5Bobject%20Object%5D&originHeight=165&originWidth=307&status=done&style=none&width=307) 

## rpx与px互转
借助 `my.getSystemInfoSync().windowWidth` 获取屏幕宽度进行转换，具体代码如下：<br />**注意：**由于安卓上取 screenWidth 屏幕宽度，可能取的是手机的 dpi，所以建议获取窗口宽度（可使用窗口高度）来做。
```
// px 转 rpx，rpx = px * (屏幕宽度 / 750 )
let rpx = px * (750 / my.getSystemInfoSync().windowWidth);

// rpx 转 px，px = rpx * (750 / 屏幕宽度)
let px = rpx * (my.getSystemInfoSync().windowWidth / 750);

```
 
