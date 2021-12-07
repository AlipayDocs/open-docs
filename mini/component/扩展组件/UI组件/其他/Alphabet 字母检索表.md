
# 简介
字母检索表。

## 扫码体验
![|154x191](https://mdn.alipayobjects.com/afts/img/A*KNOYT4LW3VEAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=LvZJ0dVW6YGHzehjluyj7wAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-alphabet?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .json 示例代码
```json
{
  "defaultTitle": "Alphabet",
  "usingComponents":{
    "alphabet": "mini-ali-ui/es/list/alphabet/index",
    "am-icon": "mini-ali-ui/es/am-icon/index"
  }
}
```

### .axml 示例代码
```html
<view style="position: relative; height: 100vh;">
 <alphabet alphabet="{{alphabet}}" onClick="onAlphabetClick" >
 	<view slot="prefix"><am-icon size="12" type="check_"/></view>
 </alphabet>
</view>
```

### .js 示例代码
```javascript
Page({
  data: {
    alphabet: ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z'],
  },
  onAlphabetClick(ev) {
    my.alert({
      content: JSON.stringify(ev.data),
    });
  },
});
```

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| alphabet | Array | 字母表内容。 |

**说明：** 右侧索引表内内容，左侧空白部分需开发者使用 List 列表做内容填充。 
