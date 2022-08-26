# 简介

通过点击水果机（九宫格）中心按钮来进行抽奖，可以自定义转动抽奖的次数。

更多详细信息请参见 [代码市场](https://openhome.alipay.com/platform/mas.htm#/templateDetail/comps/2)。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/5756b0c26387d6ec946407ea5d17a182.png#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 使用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-fruit-slots?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### 安装

```shell
npm i ant-mini-fruit-slots --save
```

### 注册

```json
// .json
{
  "usingComponents": {
    "fruit-slots": "ant-mini-fruit-slots/es/fruit-slots/index"
  }
}
```

### 调用

#### .axml 示例代码

```html
<!-- .axml -->
<view class="container">
  <fruit-slots
    prizeList="{{prizeList}}"
    prizeName="{{prizeName}}"
    disabled="{{disabled}}"
    currentIndex="{{currentIndex}}"
    onStart="onStart"
    onFinish="onFinish"
  />
  <view class="tip-text">{{tipText}}</view>
</view>
```

#### .js 示例代码

```javascript
// .js
Page({
  data: {
    prizeList: [
      // prizeList 长度必须为8，其中须包含奖项名字 name 和图标地址 icon
      {
        name: '谢谢参与',
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
        name: '谢谢参与',
        icon: 'https://zos.alipayobjects.com/rmsportal/dexmbhnbsLRGIZGBqTcA.png',
      },
      {
        name: '1元红包',
        icon: 'https://zos.alipayobjects.com/rmsportal/RxQruKQwiQCeYXhvwCfP.png',
      },
      {
        name: '谢谢参与',
        icon: 'https://zos.alipayobjects.com/rmsportal/dexmbhnbsLRGIZGBqTcA.png',
      },
      {
        name: '5元红包',
        icon: 'https://zos.alipayobjects.com/rmsportal/qanDEFeGBoiPflYxkhJY.png',
      },
    ],
    prizeName: '5元红包',
    disabled: false,
    currentIndex: 4,
    tipText: '',
  },
  onStart() {
    this.setData({
      tipText: '正在抽奖...',
    });
  },
  onFinish(index, name) {
    this.setData({
      currentIndex: Math.floor(Math.random() * 8),
      tipText: `抽奖结果：${name}`,
    });
  },
});
```

## 属性说明

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| width | Number | false | 组件宽度，单位 rpx。<br />**默认值：** 700 |
| margin | Number | false | 格子间的边距，单位 rpx。<br />**默认值：** 20 |
| prizeList | Array | true | 奖项列表，长度必须为 8，须包含 name 和 icon 字段。 |
| prizeName | String | true | 抽奖结果的奖品 name，其值必须位于 prizeList 中。 |
| rollTimes | Number | false | 转动圈数。<br />**默认值：** 3 |
| currentIndex | Number | false | 转动开始的格子下标。<br />**默认值：** 0 |
| speed | Number | false | 转动速度，单位 ms。<br />**默认值：** 100 |
| class | String | false | 自定义类名。 |
| disabled | Boolean | false | 抽奖按钮是否可点击。<br />**默认值：** false |
| onStart | Function | false | 转动开始的回调。<br />**默认值：** () => {} |
| onFinish | Function | false | 转动结束的回调, @params(index: 奖品所在格子下标，name: 奖品名称)。<br />**默认值：** (index, name) => {} |

## 说明

### 关于抽奖模式 mode 说明

默认情况下 mode = 'pre'，即向服务端请求拿到抽奖结果后，将 prizeName 传给组件，然后组件开始执行动画抽奖效果。

但是如果抽奖请求时间较长的情况下，用户就可能点击抽奖后要等待一段时间才能看到抽奖动画，体验不太好，因此新增了 realtime 实时模式。

#### 示例代码

```html
<fruit-slots
  mode="realtime"
  prizeList="{{prizeList}}"
  prizeName="{{prizeName}}"
  onStart="onStart"
  onFinish="onFinish"
/>
```

```javascript
Page({
  data: {
    prizeList: [
      // prizeList 长度必须为8，其中须包含奖项名字 name 和图标地址 icon
      {
        name: '谢谢参与',
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
        name: '谢谢参与',
        icon: 'https://zos.alipayobjects.com/rmsportal/dexmbhnbsLRGIZGBqTcA.png',
      },
      {
        name: '1元红包',
        icon: 'https://zos.alipayobjects.com/rmsportal/RxQruKQwiQCeYXhvwCfP.png',
      },
      {
        name: '谢谢参与',
        icon: 'https://zos.alipayobjects.com/rmsportal/dexmbhnbsLRGIZGBqTcA.png',
      },
      {
        name: '5元红包',
        icon: 'https://zos.alipayobjects.com/rmsportal/qanDEFeGBoiPflYxkhJY.png',
      },
    ],
    prizeName: '',
  },
  onStart() {
    // 注意，点击开始抽奖时需要将 prizeName 置为空，等待请求拿到结果之后再重新赋值，否则多次抽奖会存在问题
    this.setData({
      prizeName: '',
    });
    // 模拟请求，延迟中奖
    setTimeout(() => {
      this.setData({
        prizeName: Math.random() > 0.4 ? '3元红包' : '谢谢参与',
      });
    }, 3000);
  },
  onFinish(index, name) {
    console.log('抽奖结果：', index, name);
  },
});
```

实际开发中推荐使用 realtime 模式。

### 关于格子下标说明

组件中格子自左上角顺时针开始标号，围绕中间按钮，下标从 0 开始递增到 7。当需要组件从左下角的格子为初始位置开始转动，只需要设置 `currentIndex = 6` 即可。

![|723x407](https://gw.alipayobjects.com/zos/skylark-tools/public/files/6b024a982c9fd681d2549561d01e3d48.png#align=left&display=inline&height=420&margin=%5Bobject%20Object%5D&originHeight=720&originWidth=1280&status=done&style=none&width=746)
