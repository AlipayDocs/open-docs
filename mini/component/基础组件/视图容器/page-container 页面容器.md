
# 简介
小程序如果在页面内进行复杂的界面设计（如在页面内弹出半屏的弹窗、在页面内加载一个全屏的子页面等），用户进行返回操作会直接离开当前页面，不符合用户预期，预期应为关闭当前弹出的组件。 为此提供“假页”容器组件，效果类似于 popup 弹出层，页面内存在该容器时，当用户进行返回操作，关闭该容器不关闭页面。返回操作包括右滑手势、安卓物理返回键和调用 navigateBack 接口三种情形。

## 使用限制

- 基础库 [2.8.0](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- **Native 渲染引擎**：暂不支持。可以通过 `my.canIUse('page-container')` 判断是否支持。
- 当前页面最多只有 1 个容器，若已存在容器的情况下，无法增加新的容器。
- [my.navigateBack](https://opendocs.alipay.com/mini/api/kc5zbx) 无法在页面栈顶调用，此时没有上一级页面。
- 必须在 onAfterLeave 中执行 `this.setData({show: false})` 同步 show 属性状态。

# 使用

## 示例代码

### .axml
```html
<view class="title">弹出位置</view>
<view class="box">
  <button class="btn" onTap="popup" data-position="right">右侧弹出</button>
  <button class="btn" onTap="popup" data-position="top">顶部弹出</button>
  <button class="btn" onTap="popup" data-position="bottom">底部弹出</button>
  <button class="btn" onTap="popup" data-position="center">中央弹出</button>
</view>


<view class="title">弹窗圆角</view>
<view class="box">
  <button class="btn" onTap="changeRound">设置{{round ? '直角' : '圆角'}}</button>
</view>

<view class="title">遮罩层</view>
<view class="box">
  <button class="btn" onTap="changeOverlay">设置{{overlay ? '无' : '有'}}遮罩</button>
  <button class="btn" onTap="changeOverlayStyle" data-type="black">黑色半透明遮罩</button>
  <button class="btn" onTap="changeOverlayStyle" data-type="white">白色半透明遮罩</button>
  <button class="btn" onTap="changeOverlayStyle" data-type="blur">模糊遮罩</button>
</view>


<page-container 
  show="{{show}}"
  round="{{round}}"
  overlay="{{overlay}}"
  duration="{{duration}}"
  position="{{position}}"
  close-on-slide-down="{{false}}"
  onBeforeEnter="onBeforeEnter"
  onEnter="onEnter"
  onEnterCancelled="onEnterCancelled"
  onAfterEnter="onAfterEnter"
  onBeforeLeave="onBeforeLeave"
  onLeave="onLeave"
  onLeaveCancelled="onLeaveCancelled"
  onAfterLeave="onAfterLeave"
  onClickOverlay="onClickOverlay"
  custom-style="{{customStyle}}"
  overlay-style="{{overlayStyle}}"
  >
  <view class="detail-page">
    <button type="primary" onTap="exit" class="btn">退出</button>
  </view>
</page-container>
```

### .js
```javascript
Page({
  data: {
    show: false,
    duration: 300,
    position: "right",
    round: false,
    overlay: true,
    customStyle: "",
    overlayStyle: "",
  },
  popup(e) {
    const position = e.currentTarget.dataset.position;
    let customStyle = "";
    let duration = this.data.duration;
    switch (position) {
      case "top":
      case "bottom":
        customStyle = "height: 30%";
        break;
      case "right":
        customStyle = "width: 70%; margin-left: 30%";
        break;
    }
    this.setData({
      position,
      show: true,
      customStyle,
      duration,
    });
  },
  changeRound() {
    this.setData({ round: !this.data.round });
  },
  changeOverlay() {
    this.setData({ overlay: !this.data.overlay, show: true });
  },
  changeOverlayStyle(e) {
    let overlayStyle = "";
    const type = e.currentTarget.dataset.type;
    switch (type) {
      case "black":
        overlayStyle = "background-color: rgba(0, 0, 0, 0.7)";
        break;
      case "white":
        overlayStyle = "background-color: rgba(255, 255, 255, 0.7)";
        break;
      case "blur":
        overlayStyle =
          "background-color: rgba(0, 0, 0, 0.7); filter: blur(4px);";
    }
    this.setData({ overlayStyle, show: true });
  },
  exit() {
    this.setData({ show: false });
  },
  onBeforeEnter(res) {
    console.log(res);
  },
  onEnter(res) {
    console.log(res);
  },
  onEnterCancelled(res) {
    console.log(res);
  },
  onAfterEnter(res) {
    console.log(res);
  },
  onBeforeLeave(res) {
    console.log(res);
  },
  onLeave(res) {
    console.log(res);
  },
  onLeaveCancelled(res) {
    console.log(res);
  },
  onAfterLeave(res) {
    console.log(res);
    this.setData({ show: false });
  },
  onClickOverlay(res) {
    console.log(res);
  },
});
```

### .acss
```css
page {
  background-color: #f7f8fa;
  color: #323232;
  width: 100%;
  height: 100%;
}

.box {
  margin: 0 12px;
}

.title {
  margin: 0;
  padding: 32px 16px 16px;
  color: rgba(69, 90, 100, 0.6);
  font-weight: normal;
  font-size: 18px;
  line-height: 20px;
  text-align: center;
}

.btn {
  display: block;
  width: 70%;
  margin: 10px auto;
  background-color: #108ee9;
  border-radius: 12px;
  border: none;
}

.detail-page {
  width: 100%;
  height: 100%;
  min-height: 300px;
  display: flex;
  align-items: center;
  justify-content: center;
}
```

## 属性说明

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| show | Boolean | 是否显示容器组件。<br />**默认值：** false |
| duration | Number | 动画时长，单位毫秒。<br />**默认值：** 300 |
| z-index | Number | z-index 层级。<br />**默认值：** 100 |
| overlay | Boolean | 是否显示遮罩层。<br />**默认值：** true |
| position | String | 弹出位置。<br />**可选值：** top、bottom、right、center。<br />**默认值：** bottom |
| round | Boolean | 是否显示圆角。<br />**默认值：** false |
| close-on-slide-down | Boolean | 是否在下滑一段距离后关闭。<br />**默认值：** false |
| overlay-style | String | 自定义遮罩层样式。 |
| custom-style | String | 自定义弹出层样式。 |
| onBeforeEnter | EventHandle | 进入前触发。 |
| onEnter | EventHandle | 进入中触发。 |
| onEnterCancelled | EventHandle | 进入被打断时触发（通过 a: if 打断时不会触发）。 |
| onAfterEnter | EventHandle | 进入后触发。 |
| onBeforeLeave | EventHandle | 离开前触发。 |
| onLeave | EventHandle | 离开中触发。 |
| onLeaveCancelled | EventHandle | 离开被打断时触发（通过 a: if 打断时不会触发）。 |
| onAfterLeave | EventHandle | 离开后触发。 |
| onClickOverlay | EventHandle | 点击遮罩层时触发。 |

