# 简介

页面上有 N 张卡牌，每张卡牌对应不同奖品，用户点击卡牌进行翻牌抽奖。开发者可自定义卡牌数量和翻牌的次数。

更多详细信息请参见 [代码市场](https://openhome.alipay.com/platform/mas.htm#/templateDetail/comps/7)。

## 扫码体验

![|157x194](https://gw.alipayobjects.com/zos/skylark-tools/public/files/a7b7935583c0e6fdabae23bf6763c784.png#align=left&display=inline&height=194&margin=%5Bobject%20Object%5D&originHeight=194&originWidth=157&status=done&style=none&width=157)

# 使用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-flip-draw?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### 安装

```shell
npm i ant-mini-flip-draw --save
```

### 注册

```json
//.json
{
  "usingComponents": {
    "flipdraw": "ant-mini-flip-draw/component/index"
  }
}
```

### 调用

#### .axml 示例代码

```html
<!-- .axml -->
<view>
  <flipdraw
    prizeList="{{prizeList}}"
    prizeName="{{prizeName}}"
    isDrawing="{{isDrawing}}"
    flipAllCards="{{flipAllCards}}"
    onFlipStart="onFlipStart"
  />
</view>
```

#### .js 示例代码

```javascript
//.js
Page({
  data: {
    docParamsImg:
      'https://img.alicdn.com/tfs/TB1sfaaJSzqK1RjSZFHXXb3CpXa-1326-846.png',
    prizeList: [
      {
        name: '谢谢参与1',
        icon: 'https://zos.alipayobjects.com/rmsportal/dexmbhnbsLRGIZGBqTcA.png',
      },
      {
        name: '666元红包',
        icon: 'https://zos.alipayobjects.com/rmsportal/nxpXbcNBOmbeIOVCUsuS.png',
      },
      {
        name: '1元红包',
        icon: 'https://zos.alipayobjects.com/rmsportal/RxQruKQwiQCeYXhvwCfP.png',
      },
      {
        name: '3元红包',
        icon: 'https://zos.alipayobjects.com/rmsportal/tyMAYvTdjRFOVxqWVhsj.png',
      },
      {
        name: '谢谢参与2',
        icon: 'https://zos.alipayobjects.com/rmsportal/dexmbhnbsLRGIZGBqTcA.png',
      },
      {
        name: '1元红包',
        icon: 'https://zos.alipayobjects.com/rmsportal/RxQruKQwiQCeYXhvwCfP.png',
      },
      {
        name: '谢谢参与3',
        icon: 'https://zos.alipayobjects.com/rmsportal/dexmbhnbsLRGIZGBqTcA.png',
      },
      {
        name: '5元红包',
        icon: 'https://zos.alipayobjects.com/rmsportal/qanDEFeGBoiPflYxkhJY.png',
      },
    ],
    cardBgImg:
      'https://gw.alicdn.com/tfs/TB1P.AMXMHqK1RjSZJnXXbNLpXa-610-600.png',
    prizeName: '',
    flipAllCards: false,
    isDrawing: false,
  },
  onFlipStart() {
    console.log('开始了，这个时候最好页面控制下 loading 状态，组件内不做控制');
    this.setData({
      isDrawing: true, // 修改抽奖状态，防止重复点击多次请求
    });
    // 开始抽奖
    setTimeout(() => {
      console.log('拿到结果，设置奖品信息');
      if (Math.random() > 0.3) {
        this.setData({
          prizeName: '666元红包',
          isDrawing: false,
        });
      } else {
        this.setData({
          isDrawing: false, // 抽奖结束一定要还原 isDrawing 状态
        });
      }
      this.showResultDialog();
    }, 1000);
  },
  showResultDialog() {
    // do something
    this.setData({
      flipAllCards: true, // 将剩下未翻过的牌自动翻，展示奖品结果。
    });
  },
});
undefined;
```

## 属性说明

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| prizeList | Array | true | 奖项列表，须包含 name 和 icon 字段。 |
| prizeName | String | true | 抽奖结果的奖品 name，其值必须位于 prizeList 中。 |
| cardNum | Number | true | 展示多少张卡片，推荐 3/6/9。<br />**默认值：** 9 |
| cardHeight | Number | true | 宽度固定 210，高度需要等比换算设置。<br />**默认值：** 210 |
| cardBgImg | String | true | 卡片图片。 |
| unawardImg | String | true | 未中奖展示图片。 |
| isDrawing | Boolean | true | 是否正在抽奖，用于限制点击。 |
| flipAllCards | String | false | 是否翻转剩余卡片。 |
| onFlipStart | Function | false | 转动开始的回调。<br />**默认值：** () => {} |

**注意：**

- 请求前一定要设置 `isDrawing = true`，请求结束后一定要设置 `isDrawing = false`。
- `cardHeight` 卡片高度是相对 750 视觉稿设置的，宽高默认 210x210 rpx。宽度固定，高度可变。比如 210x300 的图片，cardHeight 就设置为 300；如果是 200x250 的图片需要等比转换一下，cardHeight = 210 \* (250/200)。
