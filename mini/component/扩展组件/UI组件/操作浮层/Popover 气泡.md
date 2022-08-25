# 简介

气泡。可通过设置 Popover-item 宽高改变气泡大小，不支持文字自适应宽高。

## 使用限制

设置 popover 位于特定元素的正下方，可以把该元素放在 popover 内并且设置 position 为 bottom 。

## 扫码体验

![|154x191](https://mdn.alipayobjects.com/afts/img/A*KRs3QZ_zR8AAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=HwC0KCFWIPKOGVKzvlzw9gAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-popover?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### .json 示例代码

```json
{
  "defaultTitle": "Popover",
  "usingComponents": {
    "popover": "mini-ali-ui/es/popover/index",
    "popover-item": "mini-ali-ui/es/popover/popover-item/index"
  }
}
```

### .axml 示例代码

```html
<view class="demo-popover">
  <popover
    position="{{position}}"
    show="{{show}}"
    showMask="{{showMask}}"
    onMaskClick="onMaskClick"
  >
    <view class="demo-popover-btn" onTap="onShowPopoverTap"
      >点击{{show ? '隐藏' : '显示'}}</view
    >
    <view slot="items">
      <popover-item
        onItemClick="itemTap1"
        iconType="{{showIcon ? 'qr' : ''}}"
        data-direction="{{position}}"
      >
        <text>{{position}}</text>
      </popover-item>
      <popover-item
        onItemClick="itemTap2"
        iconType="{{showIcon ? 'qr' : ''}}"
        data-index="{{2}}"
      >
        <text>line2</text>
      </popover-item>
    </view>
  </popover>
</view>
<view class="demo-popover-test-btns">
  <button class="demo-popover-test-btn" onTap="onNextPositionTap">
    下个位置
  </button>
  <button class="demo-popover-test-btn" onTap="onMaskChangeTap">
    蒙层{{showMask ? '隐藏' : '显示'}}
  </button>
  <button class="demo-popover-test-btn" onTap="onIconChangeTap">
    显示/隐藏图标
  </button>
</view>
```

### .js 示例代码

```javascript
const position = [
  'top',
  'topRight',
  'rightTop',
  'right',
  'rightBottom',
  'bottomRight',
  'bottom',
  'bottomLeft',
  'leftBottom',
  'left',
  'leftTop',
  'topLeft',
];
Page({
  data: {
    position: position[0],
    show: false,
    showMask: true,
    showIcon: true,
  },
  onShowPopoverTap() {
    this.setData({
      show: !this.data.show,
    });
  },
  onNextPositionTap() {
    let index = position.indexOf(this.data.position);
    index = index >= position.length - 1 ? 0 : index + 1;
    this.setData({
      show: true,
      position: position[index],
    });
  },
  onMaskChangeTap() {
    this.setData({
      showMask: !this.data.showMask,
    });
  },
  onIconChangeTap() {
    this.setData({
      showIcon: !this.data.showIcon,
    });
  },
  onMaskClick() {
    this.setData({
      show: false,
    });
  },
  itemTap1(e) {
    my.alert({
      content: `点击_${e.currentTarget.dataset.direction}`,
    });
  },
  itemTap2(e) {
    my.alert({
      content: `点击_${e.currentTarget.dataset.index}`,
    });
  },
});
```

### .acss 示例代码

```css
.demo-popover {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 400px;
}
.demo-popover-btn {
  width: 100px;
  height: 100px;
  line-height: 100px;
  text-align: center;
  background-color: #fff;
  border: 1px solid #dddddd;
  border-radius: 2px;
}
.demo-popover-test-btns {
  display: flex;
  justify-content: space-around;
}
.demo-popover-test-btn {
  width: 45%;
}
```

## 属性说明

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| className | String | false | 最外层覆盖样式。 |
| show | Boolean | true | 气泡是否展示。<br />**默认值：** false |
| showMask | Boolean | false | 蒙层是否展示。<br />**默认值：** true |
| position | String | false | 气泡位置。<br />**可选值：** top、topRight、topLeft、bottom、bottomLeft、bottomRight、right、rightTop、rightBottom、left、leftBottom、leftTop。<br />**默认值：** bottomRight |
| fixMaskFull | Boolean | - | 用以解决遮罩层受到 transform 影响而显示不全的问题。<br />**默认值：** false<br />**版本要求：** mini-ali-ui [1.0.11](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |

### popover-item

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| className | String | 单项样式。 |
| onItemClick | () => void | 单项点击事件。 |
| iconType | String | 所有的 type 值均来自 icon 组件。可选值参考 icon 组件。 |
| iconURL | String | 图片的 URL<br />**版本要求：** mini-ali-ui [1.1.2](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
