
# 简介
选择输入。

## 扫码体验
![|154x191](https://mdn.alipayobjects.com/afts/img/A*XwVVT66kNG0AAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=p9aFDx4PxuycTqU6HHzUNAAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-picker-item?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .json 示例代码
```json
{
  "defaultTitle": "Picker-item",
  "usingComponents": {
    "list": "mini-ali-ui/es/list/index",
    "picker-item": "mini-ali-ui/es/picker-item/index"
  }
}
```

### .axml 示例代码
```html
<view>
  <list>
    <picker-item
      data-field="bank"
      placeholder="选择发卡银行"
      value="{{bank}}"
      onPickerTap="onPickerTap"
    >
      发卡银行
    </picker-item>
    <picker-item
      data-field="bank"
      placeholder="选择发卡银行"
      value="{{bank}}"
      onPickerTap="onPickerTap"
      layer="vertical"
    >
      发卡银行
    </picker-item>
  </list>
</view>
```

### .js 示例代码
```javascript
const banks = ['网商银行', '建设银行', '工商银行', '浦发银行'];
Page({
  data: {
    bank: '',
  },
  onPickerTap() {
    my.showActionSheet({
      title: '选择发卡银行',
      items: banks,
      success: (res) => {
        this.setData({
          bank: banks[res.index],
        });
      },
    });
  },
});
```

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| className | String | 自定义的 class。 |
| labelCls | String | 自定义 label 的 class。 |
| pickerCls | String | 自定义选择区域的 class。 |
| last | Boolean | 是否最后一行。<br />**默认值：** false |
| value | String | 初始内容。 |
| placeholder | String | picker-item 的值。 |
| onPickerTap | (e: Object) => void | 点击 pickeritem 时触发。 |
| layer | String | 文本输入框是否为垂直排列。<br />**可选值：** vertical 时为垂直排列，空值为横向排列。<br />**版本要求：** mini-ali-ui [1.0.4](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| iconType | String | 更改 picker-item 的 icon 类型，参考 [Am-icon](https://opendocs.alipay.com/mini/component-ext/am-icon) 的 type 值。<br />**默认值：** right<br />**版本要求：** mini-ali-ui [1.0.12](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |


### slots
| **slotname** | **必填** | **描述** |
| --- | --- | --- |
| extra | 否 | 用于渲染 picker-item 项右边说明。 |

