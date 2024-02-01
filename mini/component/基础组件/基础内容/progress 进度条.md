# 简介

当页面在请求数据过程中，会出现信息读取的进度过程。

# 使用限制
**Native 渲染引擎**：暂不支持。可以通过 `my.canIUse('progress')` 判断是否支持。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark/97c38fce-1453-4d80-b1e0-c35812f56167/2018/jpeg/6df7d4cf-70e6-438f-b8c4-ef613de4005e.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=1906&originWidth=1540&status=done&style=none&width=127)

# 使用

## 在线示例

[小程序在线示例](https://opendocs.alipay.com/openbox/mini/opendocs/basic-component?view=preview&defaultPage=pages/progress/index&defaultOpenedFiles=pages/progress/index&theme=light)

## 属性说明

| 属性          | 类型    | 描述       |
| ------------ | ------- | ---------------- |
| percent      | Float   | 百分比（0~100）。 |
| show-info    | Boolean | 在右侧显示百分比值。默认值：`show-info="{{false}}"` |
| stroke-width | Number  | 线的粗细，单位是 `px`。默认值：6 |
| active-color | Color   | 已选择的进度条颜色。默认值：`#09BB07` |
| background-color | Color   | 未选择的进度条颜色。 |
| active       | Boolean | 是否添加从 0% 开始加载的入场动画。默认值：`active="{{false}}"` |
