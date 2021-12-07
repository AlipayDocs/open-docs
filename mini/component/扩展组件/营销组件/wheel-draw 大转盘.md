
# 简介
通过点击转盘中心按钮转动转盘，进行抽奖，可以自定义转盘转动抽奖的次数。

更多详细信息请参见 [代码市场](https://openhome.alipay.com/platform/mas.htm#/templateDetail/comps/1)。

## 扫码体验
![|157x194](https://gw.alipayobjects.com/zos/skylark-tools/public/files/0763a00f96be0f11bfddac893db5c54f.png#align=left&display=inline&height=194&margin=%5Bobject%20Object%5D&originHeight=194&originWidth=157&status=done&style=none&width=157)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-wheel-draw?theme=light&previewZoom=75&chInfo=openhome-doc)


## 示例代码

### 安装


```shell
npm i ant-mini-wheel-draw --save
```

### 注册

```json
//.json
{
  "usingComponents": {
    "wheel": "ant-mini-wheel-draw/es/wheel/index"
  }
}
```

### 调用

#### .axml 示例代码
```html
<!-- .axml -->
<view class="container">
  <wheel
    width="22em"
    prizeList="{{prizeList}}" // 奖项列表
    prizeName="{{prizeName}}" // 获奖项目名称
    rotTimes="{{totalTimes}}" // 转盘机会次数
    onStart="onStart" // 转盘开始旋转回调
    onFinish="onFinish" // 转盘结束旋转回调
  />
  <view class="times">
    <text>你还有{{totalTimes - curTimes}}次抽奖机会</text>
  </view>
  <view class="result">
    <text>{{result}}</text>
  </view>
</view>undefined
```

#### .js 示例代码
```javascript
// .js
Page({
  data: {
    prizeList: [
      {
        name: 'H&M100元优惠券',
        img: 'https://gw.alipayobjects.com/zos/rmsportal/nIQUKeYBbJWliGJVhVmx.png'
      }, {
        name: '2元话费券',
        img: 'https://gw.alipayobjects.com/zos/rmsportal/HkrVjjjuxZPUMCUbPazb.png'
      }, {
        name: '45元飞猪出行券',
        img: 'https://gw.alipayobjects.com/zos/rmsportal/cDctUxwBLPCszQHRapYV.png'
      }, {
        name: 'H&M10元优惠券',
        img: 'https://gw.alipayobjects.com/zos/rmsportal/FAmIWZAWpUwlRFKqQDLz.png'
      }, {
        name: '2元流量券',
        img: 'https://gw.alipayobjects.com/zos/rmsportal/cuGomeXzMyeeZMjvVjBj.png'
      }, {
        name: '未中奖',
        img: 'https://zos.alipayobjects.com/rmsportal/dwhgPyWAcXuvJAWlSSgU.png'
      }
    ],
    prizeName: '2元话费券',
    totalTimes: 2,
    curTimes: 0,
    result: '',
  },
  /*
    @param name 获奖项名字
    @param times 当前转动次数
  */
  onStart (name, times) {
    // 转盘开始转动
    this.setData({
      result: `第${times}次抽奖中，请稍候...`,
      curTimes: times++
    })
  },
  /*
    @param name 获奖项名字
    @param times 当前转动次数
  */
  onFinish (name, times) {
    // 转盘结束转动
     this.setData({
      result: name === '未中奖' ? '很遗憾，差点就中奖了' : `恭喜你，获得${name}`,
      prizeName: this.data.prizeList[Math.floor(Math.random() * 6)].name,
    })
  }
});undefined
```

## 属性说明
| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| width | Number | true | 转盘容器宽度，默认单位 px。<br />**默认值：** 300 |
| initDeg | Number | false | 转盘初始化角度旋转偏移，单位 reg。<br />**默认值：** 0 |
| rotTimes | Number | false | 抽奖机会次数，当抽奖次数大于该值时不可再抽奖。<br />**默认值：** 1 |
| prizeList | Array | true | 奖品列表，长度为6，每一项必须包含img（奖品图片） 和 name（奖品名字）。 |
| prizeName | String | true | 中奖的奖品名字，值需要存在于 prizeList 的 name 字段中。 |
| prizeWidth | Number | false | 奖品图片宽度，默认单位 px，插件会根据 width 选项值自动计算，建议不填。<br />**默认值：** 80 |
| prizePaddingTop | Number | false | 奖品图片距圆弧的内边距，默认单位 px，插件会根据 width 选项值自动计算，建议不填。<br />**默认值：** 20 |
| bgImg | String | false | 转盘扇面背景图地址。 |
| btnImg | String | false | 转盘按钮背景图地址。 |
| onStart | Function | false | 旋转开始回调，name：中奖项name，times：当前是第几次旋转。<br />**默认值：** (name, times) => {} |
| onFinish | Function | false | 旋转结束回调，name：中奖项name，times：当前是第几次旋转。<br />**默认值：** (name, times) => {} |
| onTimesUp | Function | false | 抽奖次数用尽后，再次点击抽奖按钮会触发该回调。<br />**默认值：** () => {} |

