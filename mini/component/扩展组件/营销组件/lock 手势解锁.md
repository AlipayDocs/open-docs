# 简介

与手机屏幕解锁类似，需要保证两次绘制的手势图案一致。

更多详细信息请参见 [代码市场](https://openhome.alipay.com/platform/mas.htm#/templateDetail/comps/8)。

## 扫码体验

![|157x194](https://gw.alipayobjects.com/zos/skylark-tools/public/files/fcd67fc4166680799b123b43607ed429.png#align=left&display=inline&height=194&margin=%5Bobject%20Object%5D&originHeight=194&originWidth=157&status=done&style=none&width=157)

# 使用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-lock?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### 安装

```shell
npm i ant-mini-lock --save
```

### 注册

```json
//.json
{
  "usingComponents": {
    "lock": "ant-mini-lock/src/lock/index"
  }
}
```

### 调用

#### .axml 示例代码

```html
//.axml
<lock
  canvasWidth="300"
  canvasHeight="300"
  drawColor="#3985ff"
  canvasId="canvasLock"
  chooseType="3"
  titleColor="#000000"
  titleText="绘制解锁图案"
  onFinish="onFinish"
>
</lock>
```

#### .js 示例代码

```javascript
//.js
Page({
  data: {},
  onFinish() {
    console.log('finish');
  },
});
```

## 属性说明

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| canvasWidth | Number | canvas 区域宽度，单位 px。<br />**默认值：** 300 |
| canvasHeight | Number | canvas 区域高度，单位 px。<br />**默认值：** 300 |
| canvasId | String | canvas 区域 id。<br />**默认值：** canvasLock |
| drawColor | String | 圆圈和连线绘制颜色。<br />**默认值：** #3985ff |
| chooseType | Number | 矩阵单边圆圈个数，默认九宫格。<br />**默认值：** 3 |
| titleColor | String | 标题文案颜色。<br />**默认值：** #000000 |
| titleText | String | 标题默认文案。<br />**默认值：** 绘制解锁图案 |
| onFinish | Function | 刮奖回调，当绘制正确时触发。<br />**默认值：** ()=>{} |
