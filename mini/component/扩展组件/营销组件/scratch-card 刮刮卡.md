# 简介

在刮刮卡区域进行刮卡抽奖。

更多详细信息请参见 [代码市场](https://openhome.alipay.com/platform/mas.htm#/templateDetail/comps/4)。

## 扫码体验

![|157x194](https://gw.alipayobjects.com/zos/skylark-tools/public/files/42bcbce7b1330fb44adbe7e0eac0b314.png#align=left&display=inline&height=194&margin=%5Bobject%20Object%5D&originHeight=194&originWidth=157&status=done&style=none&width=157)

# 使用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-scratch-card?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### 安装

```shell
npm i ant-mini-scratch-card --save
```

### 注册

```json
// .json
{
  "usingComponents": {
    "scratch": "ant-mini-scratch-card/es/scratch/index"
  }
}
```

### 调用

#### .axml 示例代码

```html
<!-- .axml -->
<view>
  <scratch
    tipText="刮刮我，有惊喜~"
    tipColor="#902d02"
    coverColor="#ffae8a"
    ctxLogoUrl="https://gw.alipayobjects.com/zos/rmsportal/iGLmHkSxYfXveGhuzzFf.png"
    autoFadeOut="true"
    resultText="{{result}}"
    onFinish="onFinish"
  />
</view>
<!-- 其中，result 为动态获取的抽奖结果 -->undefined
```

#### .js 示例代码

```javascript
//.js
const app = getApp();
Page({
  data: {
    result: '',
  },
  onLoad(options) {
    setTimeout(() => {
      this.setData({
        result: '很遗憾，差点就中奖了',
      });
    }, 500);
  },
  onFinish() {
    console.log('刮奖结束了');
  },
});
```

当抽奖结果显示为图片或需要自定义样式修饰时，可以传入 slot，并将 resultText 值设置为''。

```html
<!-- .axml -->
<!-- 将 resultText 设置为空字符串 -->
<scratch resultText="">
  <!-- 此处为 slot 子节点内容 -->
  <view class="result">
    <text>{{result}}</text>
  </view>
</scratch>
```

## 属性说明

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| width | Number | 刮刮卡宽度，单位 px。<br />**默认值：** 300 |
| height | Number | 刮刮卡高度，单位 px。<br />**默认值：** 300 |
| tipText | String | 刮奖区域提示文字。<br />**默认值：** 刮刮我，有惊喜 |
| tipColor | String | 提示文字的颜色。<br />**默认值：** #aaa |
| tipSize | Number | 提示文字的字号，单位 px。<br />**默认值：** 20 |
| lineWidth | Number | 擦除线宽度，单位 px。<br />**默认值：** 25 |
| activePercent | Number | 当被擦除比例达到该值时刮奖结束，取值范围 0-1。<br />**默认值：** 0.4 |
| autoFadeOut | Boolean | 当值为 true 且被擦除比例达到 `activePercent` 选项值时刮奖图层自动消失。<br />**默认值：** true |
| ctxLogoUrl | String | 刮奖区图片背景，小程序接口限制目前只支持线上 cdn 地址或离线包地址，cdn 需返回头 `Access-Control-Allow-Origin: *`。 |
| coverColor | String | 刮奖区背景色，当背景图片透明度为 0 时无效。<br />**默认值：** #dbdbdb |
| resultText | String | 刮奖结果。<br />**默认值：** 谢谢参与 |
| onFinish | Function | 刮奖结束回调，当被擦除比例达到 `activePercen`t 选项值时触发。<br />**默认值：** ()=>{} |
