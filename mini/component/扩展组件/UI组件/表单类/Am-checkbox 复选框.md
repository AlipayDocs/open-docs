
# 简介
复选框。 对齐 ant design checkbox 的设计，当  ctrlChecked===undefined （默认）时 am-checkbox 是非受控组件，否则为受控组件。

## 扫码体验

![|154x191](https://mdn.alipayobjects.com/afts/img/A*2utdSJ4pVQIAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=YNFG8j9uSgTPpwzq-7EBRAAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-am-checkbox?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .json 示例代码
```json
{
  "defaultTitle": "am-checkbox",
  "usingComponents": {
    "list": "mini-ali-ui/es/list/index",
    "list-item": "mini-ali-ui/es/list/list-item/index",
    "am-checkbox": "mini-ali-ui/es/am-checkbox/index",
    "button": "mini-ali-ui/es/button/index"
  }
}
```

### .axml 示例代码
```html
<list>
  <view slot="header">
    列表+复选框（非受控）
  </view>
  <block a:for="{{items}}">
    <list-item
      thumb=""
      arrow="{{false}}"
      index="{{index}}"
      key="items-{{index}}"
      last="{{index === (items.length - 1)}}"
    >
      <view style="display: flex; align-items: center;">
        <am-checkbox data-id="{{item.id}}" id="{{item.id}}" value="{{item.value}}" disabled="{{item.disabled}}" checked="{{item.checked}}" />
        <label for="{{item.id}}">{{item.title}}</label>
      </view>
    </list-item>
  </block>
</list>
<view style="padding: 24rpx 0 0 24rpx;">
  <button capsuleSize="small" shape="capsule" type="primary" onTap="checkedON" style="margin-left: 20rpx;">全选</button>
  <button capsuleSize="small" shape="capsule" type="primary" onTap="checkedOFF" style="margin-left: 20rpx;">不全选</button>
</view>
<list>
  <view slot="header">
    列表+复选框（受控）
  </view>
  <block a:for="{{items1}}">
    <list-item
      thumb=""
      arrow="{{false}}"
      index="{{index}}"
      key="items-{{index}}"
      last="{{index === (items.length - 1)}}"
    >
      <view style="display: flex; align-items: center;">
        <am-checkbox data-id="{{item.id}}" id="{{item.id}}" value="{{item.value}}" disabled="{{item.disabled}}" ctrlChecked="{{item.ctrlChecked}}" onChange="onChange" />
        <label for="{{item.id}}">{{item.title}}</label>
      </view>
    </list-item>
  </block>
</list>
```

### .js 示例代码
```javascript
Page({
  data: {
    items: [
      { value: 'a', title: '复选框-默认未选中', id: 'checkbox1' },
      { checked: true, value: 'b', title: '复选框-默认选中', id: 'checkbox2' },
      { checked: true, disabled: true, value: 'c', title: '复选框-默认选中disabled', id: 'checkbox3' },
    ],
    items1: [
      { ctrlChecked: false, disabled: false, value: 'd', title: '复选框-默认未选中', id: 'checkbox4' },
      { ctrlChecked: true, disabled: true, value: 'e', title: '复选框-默认未选中disabled', id: 'checkbox5' },
      { ctrlChecked: true, value: 'f', title: '复选框-默认选中', id: 'checkbox6' },
    ],
  },
  onChange(e) {
    const { id } = e.currentTarget.dataset;
    const { value } = e.detail;
    const { items1 } = this.data;
    items1.forEach((element) => {
      if (element.id === id) {
        // eslint-disable-next-line no-param-reassign
        element.ctrlChecked = value;
      }
    });
    this.setData({
      items1
    });
  },
  // 全选
  checkedON() {
    this.checkedAll(true);
  },
  // 全不选
  checkedOFF() {
    this.checkedAll(false);
  },
  checkedAll(status) {
    const { items1 } = this.data;
    items1.forEach((element) => {
      // eslint-disable-next-line no-param-reassign
      element.ctrlChecked = status;
    });
    this.setData({
      items1
    });
  },
});
```

## 属性说明
| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| value | String | false | 组件值，选中时 change 事件会携带的 value。 |
| ctrlChecked | Boolean | false | 当 ctrlChecked 不等于 undefined 时 am-checkbox 是受控组件。需要启用 component2 编译。<br />**可选值：** true、false<br />**默认值：** undefined |
| checked | Boolean | false | 当前是否选中，可用来设置默认选中。<br />**可选值：** true、false<br />**默认值：** false |
| disabled | Boolean | false | 是否禁用。<br />**可选值：** true、false<br />**默认值：** false |
| onChange | (e: Object) => void | false | change 事件触发的回调函数。 |
| id | String | false | 与 label 组件的 for 属性组合使用。 |

