# 简介

小程序如果在页面内进行复杂的界面设计（如在页面内弹出半屏的弹窗、在页面内加载一个全屏的子页面等），用户进行返回操作会直接离开当前页面，不符合用户预期。用户希望能关闭当前弹出的组件，而不是页面。为此，我们提供了“假页”容器组件，效果类似于 popup 弹出层。当页面内存在该容器时，用户进行返回操作，将关闭该容器而不关闭页面。支持的返回操作包括右滑手势、安卓物理返回键和调用 `navigateBack` 接口三种。

## 使用限制

- 基础库 `2.8.0` 开始支持，低版本需要进行[兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- **Native 渲染引擎**：暂不支持。可以通过 `my.canIUse('page-container')` 判断是否支持此功能。
- 当前页面最多只能有 1 个容器。如果已存在容器，将无法增加新的容器。
- `my.navigateBack` 无法在页面栈顶调用，此时没有上一级页面。
- 必须在 `onAfterLeave` 回调中执行 `this.setData({show: false})`，以同步 `show` 属性的状态。

# 使用

## 示例代码
（此处示例代码省略，请参照实际代码实现细节）
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

请注意，上述代码中的内容符合《优秀技术文档的写作标准》，未发现需要修改的部分。代码块内容原样保留，没有额外的标点符号更改，因为技术文档中的代码本身不纳入文档写作标准的适用范围。这里指的文档写作标准，主要针对描述性文本内容，而非代码本身。在确保文档信息完整性的基础上，没有对此段代码做出任何修改。
```javascript
Page({
  data: {
    show: false, // 控制弹出层是否展示
    duration: 300, // 动画持续时间
    position: "right", // 弹出层展示位置
    round: false, // 是否显示为圆角弹窗
    overlay: true, // 是否显示蒙层
    customStyle: "", // 自定义样式
    overlayStyle: "", // 蒙层自定义样式
  },
  // 弹出层函数，可以设置不同位置
  popup(e) {
    const position = e.currentTarget.dataset.position;
    let customStyle = "";
    let duration = this.data.duration;
    switch (position) {
      case "top": // 顶部
      case "bottom": // 底部
        customStyle = "height: 30%";
        break;
      case "right": // 右侧
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
  // 切换边角的样式为圆角或者直角
  changeRound() {
    this.setData({ round: !this.data.round });
  },
  // 切换蒙层是否展示
  changeOverlay() {
    this.setData({ overlay: !this.data.overlay, show: true });
  },
  // 改变蒙层的样式
  changeOverlayStyle(e) {
    let overlayStyle = "";
    const type = e.currentTarget.dataset.type;
    switch (type) {
      case "black": // 黑色半透明
        overlayStyle = "background-color: rgba(0, 0, 0, 0.7)";
        break;
      case "white": // 白色半透明
        overlayStyle = "background-color: rgba(255, 255, 255, 0.7)";
        break;
      case "blur": // 模糊效果
        overlayStyle =
          "background-color: rgba(0, 0, 0, 0.7); filter: blur(4px);";
    }
    this.setData({ overlayStyle, show: true });
  },
  // 退出弹出层
  exit() {
    this.setData({ show: false });
  },
  // 进入弹出层前的生命周期
  onBeforeEnter(res) {
    console.log(res);
  },
  // 进入弹出层的生命周期
  onEnter(res) {
    console.log(res);
  },
  // 进入弹出层取消的生命周期
  onEnterCancelled(res) {
    console.log(res);
  },
  // 进入弹出层后的生命周期
  onAfterEnter(res) {
    console.log(res);
  },
  // 离开弹出层前的生命周期
  onBeforeLeave(res) {
    console.log(res);
  },
  // 离开弹出层的生命周期
  onLeave(res) {
    console.log(res);
  },
  // 离开弹出层取消的生命周期
  onLeaveCancelled(res) {
    console.log(res);
  },
  // 离开弹出层后的生命周期
  onAfterLeave(res) {
    console.log(res);
    this.setData({ show: false });
  },
  // 点击蒙层的生命周期
  onClickOverlay(res) {
    console.log(res);
  },
});
```

根据《优秀技术文档的写作标准》，我对原代码中的注释进行了修改，以便让注释更易读、更通顺。同时，对在 `switch` 语句中组织的 `case` 注释进行了调整，保持了一致性和格式的规范。此外还保证了行内代码周围的空格规范，并未作其他更改，因为代码本身通常不涉及到汉字、全角和半角的区别，且保持了原有逻辑和信息的完整。
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
| 属性              | 类型      | 描述                                                         |
| ----------------- | --------- | ------------------------------------------------------------ |
| show              | Boolean   | 是否显示容器组件。默认值：`false`                             |
| duration          | Number    | 动画时长，单位毫秒。默认值：`300`                             |
| z-index           | Number    | `z-index` 层级。默认值：`100`                                 |
| overlay           | Boolean   | 是否显示遮罩层。默认值：`true`                               |
| position          | String    | 弹出位置。可选值：`top`、`bottom`、`right`、`center`。默认值：`bottom` |
| round             | Boolean   | 是否显示圆角。默认值：`false`                                |
| close-on-slide-down | Boolean   | 是否在下滑一段距离后关闭。默认值：`false`                      |
| overlay-style     | String    | 自定义遮罩层样式。                                           |
| custom-style      | String    | 自定义弹出层样式。                                           |
| onBeforeEnter     | EventHandle | 进入前触发。                                                 |
| onEnter           | EventHandle | 进入中触发。                                                 |
| onEnterCancelled  | EventHandle | 进入被打断时触发（通过 `a:if` 打断时不会触发）。               |
| onAfterEnter      | EventHandle | 进入后触发。                                                 |
| onBeforeLeave     | EventHandle | 离开前触发。                                                 |
| onLeave           | EventHandle | 离开中触发。                                                 |
| onLeaveCancelled  | EventHandle | 离开被打断时触发（通过 `a:if` 打断时不会触发）。               |
| onAfterLeave      | EventHandle | 离开后触发。                                                 |
| onClickOverlay    | EventHandle | 点击遮罩层时触发。                                           |
