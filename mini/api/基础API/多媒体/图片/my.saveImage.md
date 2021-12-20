
# 简介
**my.saveImage** 是将在线图片保存至本地相册的 API。推荐使用 [my.saveImagetophotosalbum](https://opendocs.alipay.com/mini/02eizl)。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|127x157](https://cdn.nlark.com/yuque/0/2021/jpeg/179989/1625192315385-81fddf22-2258-48ea-9ce1-61b3ca326e7e.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&name=1.jpeg&originHeight=157&originWidth=127&size=19820&status=done&style=stroke&width=127)

## 效果示例
![|723x407](https://cdn.nlark.com/yuque/0/2021/png/179989/1625192299721-b765c561-e661-4dcd-a6cb-433efe715073.png#align=left&display=inline&height=562&margin=%5Bobject%20Object%5D&name=2.png&originHeight=720&originWidth=1280&size=28691&status=done&style=stroke&width=999)

# 接口调用

## 示例代码

### .json 示例代码
```json
{
    "defaultTitle": "图片"
}
```

### .axml 示例代码
```html
<!-- API-DEMO page/API/image/image.axml -->
<view class="page">
  <view class="page-section">
    <view class="page-section-btns">
      <view onTap="chooseImage">选择照片</view>
      <view onTap="previewImage">预览照片</view>
      <view onTap="saveImage">保存照片</view>
    </view>
  </view>
</view>
```

### .js 示例代码
```javascript
// API-DEMO page/API/image/image.js
Page({
  chooseImage() {
    my.chooseImage({
      sourceType: ['camera','album'],
      count: 2,
      success: (res) => {
        my.alert({
          content: JSON.stringify(res),
        });
      },
      fail:()=>{
        my.showToast({
          content: 'fail', // 文字内容
        });
      }
    })
  },
  previewImage() {
    my.previewImage({
      current: 2,
      urls: [
        'https://img.alicdn.com/tps/TB1sXGYIFXXXXc5XpXXXXXXXXXX.jpg',
        'https://img.alicdn.com/tps/TB1pfG4IFXXXXc6XXXXXXXXXXXX.jpg',
        'https://img.alicdn.com/tps/TB1h9xxIFXXXXbKXXXXXXXXXXXX.jpg'
      ],
    });
  },
  saveImage() {
    my.saveImage({
      url: 'https://img.alicdn.com/tps/TB1sXGYIFXXXXc5XpXXXXXXXXXX.jpg',
      showActionSheet: true,
      success: () => {
        my.alert({
          title: '保存成功',
        });
      },
    });
  }
});
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| url | String | 是 | 要保存的图片链接。 |
| showActionSheet | Boolean | 否 | 是否显示图片操作菜单，默认为 true。<br />基础库 [1.24.0](https://opendocs.alipay.com/mini/00d5f5) 版本开始支持。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


## 错误码
| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 2 | 参数无效，没有传 URL 参数。 | 重新传入正确的 URL 参数。 |
| 15 | 没有开启相册权限（仅在 iOS 上可用）。 | 开启相册权限。 |
| 16 | 手机相册存储空间不足 （仅在 iOS 上可用）。 | 释放手机存储空间。 |
| 17 | 保存图片过程中的其他错误。 | 稍后重试。 |
| 2001 | 用户拒绝给小程序授权。 | 提示用户接受小程序授权。 |


## 常见问题 FAQ

### Q：my.saveImage 接口不能保存 Base64 的图片吗？

A：目前 my.saveImage 暂不支持保存 Base64 的图片。
