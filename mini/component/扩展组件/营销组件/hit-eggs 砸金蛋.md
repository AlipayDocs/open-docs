
# 简介
红包在各个金蛋之间移动，用户需要快速反应，点击红包所在金蛋进行砸蛋抽奖。

更多详细信息请参见 [代码市场](https://openhome.alipay.com/platform/mas.htm#/templateDetail/comps/5)。

## 扫码体验
![|157x194](https://gw.alipayobjects.com/zos/skylark-tools/public/files/795ce6a3ac5579eaecbf6300a999b549.png#align=left&display=inline&height=194&margin=%5Bobject%20Object%5D&originHeight=194&originWidth=157&status=done&style=none&width=157)

# 使用

## Herbox 
[小程序在线](https://herbox-embed.alipay.com/s/doc-hit-eggs?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### 安装
```shell
npm i ant-mini-hit-eggs --save
```

### 注册
```json
//.json
{
  "usingComponents": {
    "hit-eggs": "ant-mini-hit-eggs/es/hit-eggs/index"
  }
}
```

### 调用

#### .axml 示例代码
```html
//.axml
<view>
  <hit-eggs
    onStart="onStart"
    onFinish="onFinish"
    disabled="{{disabled}}"
  />
</view>undefined
```

#### .js 示例代码
```javascript
//.js
Page({
  data: {
    disabled: false,
    times: 0
  },
  onStart () {
    console.log('开始砸金蛋');
    this.setData({
      times: ++this.data.times,
    })
  },
  onFinish () {
    console.log('砸金蛋结束');
    if (this.data.times >= 3) {
      this.setData({
        disabled: true,
      });
    }
  }
});
```

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| eggsCount | Number | 金蛋个数。<br />**默认值：** 9 |
| eggCol | Number | 金蛋列数。<br />**默认值：** 3 |
| eggWidth | Number | 金蛋大小，单位 rpx。<br />**默认值：** 200 |
| hammerWidth | Number | 锤子大小， 单位 rpx。<br />**默认值：** 100 |
| eggMarginTop | Number | 金蛋上边距。<br />**默认值：** 20 |
| hammerOriginX | Number | 锤子原点距离组件右上顶点的偏移 X，左正右负，单位 rpx。<br />**默认值：** -20 |
| hammerOriginY | Number | 锤子原点距离组件右上顶点的偏移 Y，下正上负，单位 rpx。<br />**默认值：** -20 |
| jumpingInterval | Number | 金蛋跳动时间间隔，单位 ms。<br />**默认值：** 600 |
| smashingDuration | Number | 砸金蛋持续时间，单位 ms。<br />**默认值：** 1500 |
| className | String | 自定义类名。 |
| disabled | Boolean | 是否进行游戏。<br />**默认值：** false |
| onStart | Function | 砸金蛋开始的回调，参数：index 被砸金蛋的下标。<br />**默认值：** (index) => {} |
| onFinish | Function | 砸金蛋结束的回调，参数：index 被砸金蛋的下标。<br />**默认值：** (index) => {} |
| hammerIcon | String | 锤子图标。<br />**默认值：** [src](https://gw.alipayobjects.com/zos/rmsportal/XgogyVJXSBVXPxbTOFDK.png) |
| eggIcon | String | 金蛋图标。<br />**默认值：** [src](https://gw.alipayobjects.com/zos/rmsportal/XgogyVJXSBVXPxbTOFDK.png) |
| jumpIcon | String | 金蛋跳动的图标。<br />**默认值：** [src](https://gw.alipayobjects.com/zos/rmsportal/XgogyVJXSBVXPxbTOFDK.png) |
| redBagIcon | String | 金蛋被砸的图标。<br />**默认值：** [src](https://gw.alipayobjects.com/zos/rmsportal/XgogyVJXSBVXPxbTOFDK.png) |
| smashedIcon | String | 金蛋砸碎的图标。<br />**默认值：** [src](https://gw.alipayobjects.com/zos/rmsportal/XgogyVJXSBVXPxbTOFDK.png) |

