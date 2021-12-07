# 简介
**my.getMenuButtonBoundingClientRect** 获取菜单按钮（右上角胶囊按钮）的布局位置信息。坐标信息以屏幕左上角为原点。。

## 使用限制

- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 示例代码

### .js 示例代码
```javascript
// API-DEMO page/API/get-menu-button-bounding-client-rect/get-menu-button-bounding-client-rect.js
Page({
  getMenuButtonBoundingClientRect() {
    const res = my.getMenuButtonBoundingClientRect()
    console.log(res)
    //  bottom: 142.53125
    //  height: 28
    //  left: 279
    //  optionMenuStatus: "None"
    //  right: 393.640625
    //  success: true
    //  top: 51.5
    //  width: 77
  }
});
```

### success 回调函数
Object 类型，属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| width | number | 宽度，单位：px |
| height | number | 高度，单位：px |
| top | number | 上边界坐标，单位：px |
| right | number | 右边界坐标，单位：px |
| bottom | number | 下边界坐标，单位：px |
| left | number | 左边界坐标，单位：px |
