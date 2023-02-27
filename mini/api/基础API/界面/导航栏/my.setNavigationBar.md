# 简介

**my.setNavigationBar** 是设置导航栏样式（包括：导航栏标题、导航栏背景色、导航栏底部边框颜色、导航栏左上角 LOGO 图片）的 API。

## 使用限制

- 导航栏左上角 LOGO 图片支持 GIF 格式，必须使用 HTTPS 图片链接。
- 若设置了导航栏背景色 backgroundColor，则导航栏底部边框颜色 borderBottomColor 不会生效，默认会和 backgroundColor 颜色一样。
- 导航栏背景色不支持渐变色。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/8fe00977a77cdb4a0bc53594a2db1075.png#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 在线示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/set-navigation-bar?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light)

### .js 示例代码

```javascript
Page({
  setNavigationBar(e) {
    var title = e.detail.value.title;
    var backgroundColor = e.detail.value.backgroundColor;
    var borderBottomColor = e.detail.value.borderBottomColor;
    var image = e.detail.value.image;
    console.log(title);
    my.setNavigationBar({
      title,
      backgroundColor,
      borderBottomColor,
      image,
    });
  },
  resetNavigationBar() {
    my.setNavigationBar({
      reset: true,
      title: '重置导航栏样式',
    });
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| title | String | 否 | 导航栏标题。 |
| image | String | 否 | 图片链接地址（支持 GIF 格式图片），必须是 HTTPS，请使用 iOS @3x 分辨率标准的高清图片。<br />若设置了 image 则 title 参数失效。 |
| frontColor | String | 否 | 导航栏前景色，包括返回键、标题、收藏、右上角胶囊按钮的颜色，仅支持 #ffffff 和 #000000。 <br /> <strong>基础库 2.7.24 开始支持</strong> |
| backgroundColor | String | 否 | 导航栏背景色，支持十六进制颜色值。 |
| borderBottomColor | String | 否 | 导航栏底部边框颜色，支持十六进制颜色值。<br />若设置了 backgroundColor，则 borderBottomColor 不会生效，默认会和 backgroundColor 颜色一样。 |
| reset | Boolean | 否 | 是否重置导航栏为支付宝默认配色，默认为 false。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

# 常见问题

## Q：小程序右上角的 分享与收藏 可以设置颜色吗？

A：通过设置frontColor的颜色为#000000或#FFFFFF可设置分享与收藏按钮的颜色。

# 相关信息

iOS @3x 分辨率标准的更多信息，可查看 [Image Size and Resolution](https://developer.apple.com/design/human-interface-guidelines/ios/icons-and-images/image-size-and-resolution/)。
