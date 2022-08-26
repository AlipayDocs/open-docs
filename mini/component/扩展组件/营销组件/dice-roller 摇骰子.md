# 简介

用户点击按钮或者摇动手机进行摇骰子，根据出现的点数进行相应抽奖，可以摇动多次。

更多详细信息请参见 [代码市场](https://openhome.alipay.com/platform/mas.htm#/templateDetail/comps/6)。

## 扫码体验

![|157x194](https://gw.alipayobjects.com/zos/skylark-tools/public/files/2e3d753edf1bcdce077fa6260f705272.png#align=left&display=inline&height=194&margin=%5Bobject%20Object%5D&originHeight=194&originWidth=157&status=done&style=none&width=157)

# 使用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-dice-roller?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### 安装

```shell
npm i ant-mini-dice-roller --save
```

### 注册

```json
//.json
{
  "usingComponents": {
    "diceroller": "ant-mini-dice-roller/es/component/index"
  }
}
```

### 调用

#### .axml 示例代码

```html
//.axml
<view class="container">
  <diceroller
    clickMode="true"
    awardImg="{{awardImg}}"
    onStart="onStart"
    onFinish="onFinish"
  >
    <view slot="button">外部组件摇一摇按钮</view>
  </diceroller>
  <view class="tip-text">{{tipText}}</view>
</view>
```

#### .js 示例代码

```javascript
//.js
var toast = function (title) {
  my.showToast({
    type: 'success',
    content: title,
    duration: 1000,
  });
};
Page({
  data: {
    awardImg: '',
    awardName: '',
    tipText: '',
  },
  onStart() {
    toast('开始摇');
    this.setData({
      tipText: '正在抽奖...',
    });
    setTimeout(() => {
      this.setData({
        awardImg:
          'https://gw.alicdn.com/tfs/TB1JsqGbHPpK1RjSZFFXXa5PpXa-289-298.png',
        awardName: '1等奖',
      });
    }, 2000);
  },
  onFinish() {
    toast('摇完啦');
    this.setData({
      tipText: `抽奖结果：${this.data.awardName}`,
    });
  },
});
undefined;
```

## 属性说明

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| width | Number | 组件宽度（rpx）。<br />**默认值：** 318 |
| height | Number | 组件高度（rpx）。<br />**默认值：** 300 |
| background | String | 背景色。<br />**默认值：** #FFF |
| rollTime | Number | 摇骰子时间（毫秒）。<br />**默认值：** 3000 |
| rollImg | String | 摇奖时逐帧图片。<br />**默认值：** [查看](https://gw.alipayobjects.com/zos/rmsportal/cuSVBODjFpqiVMgnLiXK.png) |
| initImg | String | 初始化骰子图片。<br />**默认值：** [查看](https://gw.alipayobjects.com/zos/rmsportal/cuSVBODjFpqiVMgnLiXK.png) |
| onStart | Func | 开始回调。 |
| onFinish | Func | 结束回调。 |
