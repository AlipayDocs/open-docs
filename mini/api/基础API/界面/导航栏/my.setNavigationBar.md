# 简介

**my.setNavigationBar**  是设置导航栏样式（包括：导航栏标题、导航栏背景色、导航栏底部边框颜色、导航栏左上角 LOGO 图片）的 API。

## 使用限制

- 导航栏左上角 LOGO 图片支持 GIF 格式，必须使用 HTTPS 图片链接。
- 若设置了导航栏背景色 backgroundColor，则导航栏底部边框颜色 borderBottomColor  不会生效，默认会和 backgroundColor 颜色一样。
- 导航栏背景色不支持渐变色。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/8fe00977a77cdb4a0bc53594a2db1075.png#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-set-navigation-bar?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .json 示例代码

```json
{
  "defaultTitle": "设置页面导航栏"
}
```

### .acss 示例代码
```css
/* API-DEMO page/API/set-navigation-bar/set-navigation-bar.acss */
.page-section-btns {
  padding: 26rpx;
}
```

### .axml 示例代码

```html
<!-- API-DEMO page/API/set-navigation-bar/set-navigation-bar.axml-->
<view class="page">
  <view class="page-description">设置导航栏 API</view>
  <form onSubmit="setNavigationBar" style="align-self:stretch">
    <view class="page-section">
      <view class="page-section-demo">
        <input class="page-body-form-value" type="text" placeholder="标题" name="title"></input>
        <input class="page-body-form-value" type="text" placeholder="导航栏背景色" name="backgroundColor"></input>
        <input class="page-body-form-value" type="text" placeholder="导航栏底部边框颜色" name="borderBottomColor"></input>
        <input class="page-body-form-value" type="text" placeholder="导航栏图片地址" name="image"></input>
      </view>
      <view class="page-section-btns">
        <button type="primary" size="mini" formType="submit">设置</button>
        <button type="primary" size="mini" onTap="resetNavigationBar">重置</button>
      </view>
    </view>
  </form>
  <view class="tips">
    tips:
   <view class="item">1. image:图片链接地址，必须 https，请使用一张3x高清图。若设置了 image，则 title 参数失效</view>
   <view class="item">2. backgroundColor: 导航栏背景色，支持 16 进制颜色值</view>
   <view class="item">3. borderBottomColor: 导航栏底部边框颜色，支持16进制颜色值。若设置了 backgroundColor，borderBottomColor 会不生效，默认会和 backgroundColor 颜色一样。</view>
  </view>
</view>
```

### .js 示例代码

```javascript
// API-DEMO page/API/set-navigation-bar/set-navigation-bar.js
Page({
  setNavigationBar(e) {
    var title = e.detail.value.title;
    var backgroundColor = e.detail.value.backgroundColor;
    var borderBottomColor = e.detail.value.borderBottomColor;
    var image = e.detail.value.image;
    console.log(title)
    my.setNavigationBar({
      title,
      backgroundColor,
      borderBottomColor,
      image,
    })
  },
  resetNavigationBar() {
    my.setNavigationBar({
      reset: true,
      title: '重置导航栏样式',
    });
  }
})
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| title | String | 否 | 导航栏标题。 |
| image | String | 否 | 图片链接地址（支持 GIF 格式图片），必须是 HTTPS，请使用 iOS @3x 分辨率标准的高清图片。<br />若设置了 image 则 title 参数失效。 |
| backgroundColor | String | 否 | 导航栏背景色，支持十六进制颜色值。 |
| borderBottomColor | String | 否 | 导航栏底部边框颜色，支持十六进制颜色值。<br />若设置了 backgroundColor，则 borderBottomColor  不会生效，默认会和 backgroundColor 颜色一样。 |
| reset | Boolean | 否 | 是否重置导航栏为支付宝默认配色，默认为 false。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

# 常见问题

## Q：小程序右上角的 分享与收藏 可以设置颜色吗？
A：这是默认的，无法设置颜色。

# 相关信息
iOS @3x 分辨率标准的更多信息，可查看 [Image Size and Resolution](https://developer.apple.com/design/human-interface-guidelines/ios/icons-and-images/image-size-and-resolution/)。
