# 简介

小提示。分 tips-dialog（对话型）和 tips-plain（简单型）两种类型。

## 使用限制

- 仅用于 UI 展示没有对应的业务逻辑功能。
- 收藏引导 tips 不针对小程序，只针对用户，用户见到第一次引导收藏 tips 之后，所有小程序都将对该用户隐藏引导收藏的 tips。

## 扫码体验

![|154x191](https://mdn.alipayobjects.com/afts/img/A*yfZURLPdBOsAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=UAAm-g5ooVnIlNHckQOZRgAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-tips?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### .json 示例代码

```json
{
  "defaultTitle": "Tips",
  "usingComponents": {
    "tips-dialog": "mini-ali-ui/es/tips/tips-dialog/index",
    "tips-plain": "mini-ali-ui/es/tips/tips-plain/index"
  }
}
```

### tips-dialog

#### .axml 示例代码

```html
<view>
  <tips-dialog show="{{showDialog}}" className="dialog" type="dialog">
    <view class="content" slot="content">
      <view>hello,</view>
      <view>欢迎使用小程序扩展组件库mini-ali-ui</view>
    </view>
    <view slot="operation" class="opt-button" onTap="onDialogTap">知道了</view>
  </tips-dialog>
  <tips-dialog
    iconUrl="https://gw.alipayobjects.com/zos/rmsportal/AzRAgQXlnNbEwQRvEwiu.png"
    type="rectangle"
    className="rectangle"
    onCloseTap="onCloseTap"
    show="{{showRectangle}}"
  >
    <view class="content" slot="content"> 把“城市服务”添加到首页 </view>
    <view slot="operation" class="add-home" onTap="onRectangleTap"
      >立即添加</view
    >
  </tips-dialog>
</view>
```

#### .js 示例代码

```javascript
Page({
  data: {
    showRectangle: true,
    showDialog: true,
  },
  onCloseTap() {
    this.setData({
      showRectangle: false,
    });
  },
  onRectangleTap() {
    my.alert({
      content: 'do something',
    });
  },
  onDialogTap() {
    this.setData({
      showDialog: false,
    });
  },
});
```

#### .acss 示例代码

```css
.rectangle {
  position: fixed;
  bottom: 100px;
}
.dialog {
  position: fixed;
  bottom: 10px;
}
.content {
  font-size: 14px;
  color: #fff;
}
.opt-button {
  width: 51px;
  height: 27px;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #fff;
  font-size: 12px;
  border: #68baf7 solid 1rpx;
}
.add-home {
  width: 72px;
  height: 27px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #56adeb;
  color: #fff;
  font-size: 14px;
}
```

### tips-plain

##### .axml 示例代码

```html
<tips-plain onClose="onClose" onTimeOut="onTimeOut" time="{{time}}"
  >{{content}}</tips-plain
>
```

#### .js 示例代码

```javascript
Page({
  data: {
    content: '我知道了(2秒后消失)',
    time: 2000,
  },
  onClose() {
    my.alert({
      title: '主动关闭 tips',
    });
  },
  onTimeOut() {
    my.alert({
      title: '时间到了，关闭 tips',
    });
  },
});
```

## 属性说明

### tips-dialog

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| className | String | false | 自定义 class。 |
| show | Boolean | false | 控制组件是否展示。<br />**默认值：** true |
| type | String | false | dialog 表示对话框的样式类型，rectangle 表示矩形的样式类型。<br />**默认值：** dialog |
| onCloseTap | ()=> void | false | 当 type 值为 rectangle 时，组件点击关闭 icon 的回调。 |
| iconUrl | String | false | 展示 icon 的 url 地址。 |
| arrowPosition | String | false | 控制 tips 中的箭头位置。<br />**可选值：** bottom-left、bottom-center、bottom-right、top-left、top-center、top-right、left、right。<br />**默认值：** bottom-left |

### slots

| **slotName** | **描述**                 |
| ------------ | ------------------------ |
| content      | 用于渲染提示的正文内容。 |
| operation    | 用于渲染右侧操作区域。   |

### tips-plain

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| className | String | false | 自定义 class。 |
| time | Number | false | 自动关闭时间（单位：毫秒）。<br />**默认值：** 5000 ms |
| onClose | () => void | false | 回调并关闭提示框。 |
| onTimeOut | () => void | false | 倒计时结束时关闭回调.<br />**版本要求：** mini-ali-ui[1.0.11](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
