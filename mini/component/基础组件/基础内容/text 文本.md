
# 简介
文本。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark/b4c189f1-22d5-4832-9080-5c786ab589fd/2018/jpeg/3b380081-14e7-43a2-a4b2-17ae32d50d6f.jpeg#align=left&display=inline&height=1906&margin=%5Bobject%20Object%5D&originHeight=1906&originWidth=1540&status=done&style=none&width=127)

# 使用

## Herbox
[小程序在线](https://opendocs.alipay.com/examples/4ba7cd59-c4b5-4877-ba85-299e460ee87d) 

## 示例代码

### .axml 示例代码
```html
<!-- API-DEMO page/component/text.axml -->
<view class="page">
  <view class="page-description">
    <view class="text-demo-title">
      <text class="text-demo-text">这是一段文本。\n<text>\</text><text>n</text> 可以换行。</text>
    </view>  
  </view>
  <view class="page-section">
    <view class="page-section-demo">
      <text>{{text}}</text>
    </view>
  </view>
</view>
```

### .js 示例代码
```js
// API-DEMO page/component/text.js
Page({
  data: {
    text: `支付宝是一个大型生活服务类的平台，用户群非常广泛，上至五六十岁，下至十几岁。
      这里不仅有官方自营应用，还有第三方接入应用，用户的选择很多。
      只有你的产品做得足够简单，才能让更多的用户使用。而更多人的使用，也意味着你更大的收益。\n\n:)
    `,
  },
});
```

### .acss 示例代码
```css
/* API-DEMO page/component/text.acss */
.page {
  padding: 0;
}
.text-demo-title {
  margin-left: 30rpx;
  margin-top: 30rpx;
}
.text-demo-text {
  font-size: 36rpx;
}
```

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| selectable | Boolean | 是否可选。<br />**默认值：** false |
| space | String | 以何种方式显示连续空格。 |
| decode | Boolean | 是否解码。为 true 时表示对文本内容进行解码，可解析的 HTML 实体字符有：`&nbsp;&lt;&gt;&amp;&apos;&ensp;&emsp;`。<br />**默认值：** false |
| number-of-lines | Number | 多行省略，值须大于等于 1，表现同 css 的 `-webkit-line-clamp` 属性一致。 |


### space 有效值
**说明：** 各个操作系统的空格标准并不一致。

| **属性** | **描述** |
| --- | --- |
| nbsp | 根据字体设置的空格大小。 |
| ensp | 中文字符空格一半大小。 |
| emsp | 中文字符空格大小。 |



