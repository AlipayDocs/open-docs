# 简介
**my.alert** 方法用于弹出一个带有标题、内容以及确认按钮的警告框。

## 使用限制

- 暂不支持设置图片等样式。
- 不支持在 IoT 双屏小程序的副屏调用。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/34912116506eb06e4f55f825b4ff9120.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/examples/caeb252f-f08f-4569-8489-338e707969dc) 

### .axml 示例代码
```html
<!-- API-DEMO page/API/alert/alert.axml-->
<view class="page">
  <view class="page-description">警告框 API</view>
  <view class="page-section">
    <view class="page-section-title">my.alert</view>
    <view class="page-section-demo">
      <button type="primary" onTap="alert">显示警告框</button>
    </view>
  </view>
</view>
```

### .js 示例代码
```javascript
// API-DEMO page/API/alert/alert.js
Page({
  alert() {
    my.alert({
      title: '亲',
      content: '您本月的账单已出',
      buttonText: '我知道了',
      success: () => {
        my.alert({
          title: '用户点击了「我知道了」',
        });
      }
    });
  },
})
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| title | String | 否 | 警告框的标题。 |
| content | String | 否 | 警告框的内容。 |
| buttonText | String | 否 | 按钮文字，默认为 **确定**。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

# 常见问题
## Q：警告框内容 content 文字如何进行换行？
A：content 文字可通过 \n 或 \r\n 进行换行，代码示例： 
```javascript
my.alet({
  content: '第一行\n第二行\r\n第三行'
})
```

## Q：content 属性支持设置样式吗？content 属性支持html解析吗？
A：content 不支持设置样式和 html 解析。如有相关需求，可使用 [Modal](https://opendocs.alipay.com/mini/component-ext/modal) 组件实现一个自定义弹窗。

## Q：content 属性文字对齐方式？
A：在安卓系统下，content属性文字是左对齐的；在 iOS 系统下，content 属性文字是居中对齐的。

## Q：在 my.alert 唤起警告框后进行页面跳转，警告框是否消失？
A：如果在 my.alert 唤起警告框后进行跳转页面，在安卓系统下页面跳转后 my.alert 警告框依然存在，在 iOS 系统下跳转页面后 my.alert 警告框消失。 
