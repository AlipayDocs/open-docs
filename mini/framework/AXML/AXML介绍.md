AXML 是小程序框架设计的一套标签语言，用于描述小程序页面的结构。 AXML 语法可分为五个部分：[数据绑定](https://opendocs.alipay.com/mini/framework/data-binding)、[条件渲染](https://opendocs.alipay.com/mini/framework/conditional-render)、[列表渲染](https://opendocs.alipay.com/mini/framework/list-render)、[模板](https://opendocs.alipay.com/mini/framework/axml-template)、[引用](https://opendocs.alipay.com/mini/framework/import)。

AXML 代码示例：
```html
<!-- pages/index/index.axml -->
<view a:for="{{items}}"> {{item}} </view>
<view a:if="{{view == 'WEBVIEW'}}"> WEBVIEW </view>
<view a:elif="{{view == 'APP'}}"> APP </view>
<view a:else> alipay </view>
<view onTap="add"> {{count}} </view>
```

对应的 .js 文件示例：
```javascript
// pages/index/index.js
Page({
  data: {
    items: [1, 2, 3, 4, 5, 6, 7],
    view: 'alipay',
    count: 1,
  },
  add(e) {
    this.setData({
      count: this.data.count + 1,
    });
  },
});
```

对应的 .acss 文件示例：
```css
/* pages/index/index.acss */
view {
  padding-left: 10px;
}
```

效果示例：

![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/4f86582eabf8293eae3b1e207037b18f.png#align=left&display=inline&height=720&margin=%5Bobject%20Object%5D&originHeight=720&originWidth=1280&status=done&style=none&width=1280)

# 相关文档

- [小程序页面介绍](https://opendocs.alipay.com/mini/framework/page)
- [数据绑定](https://opendocs.alipay.com/mini/framework/data-binding)
- [条件渲染](https://opendocs.alipay.com/mini/framework/conditional-render)
- [列表渲染](https://opendocs.alipay.com/mini/framework/list-render)
- [模板](https://opendocs.alipay.com/mini/framework/axml-template)
- [引用](https://opendocs.alipay.com/mini/framework/import)




