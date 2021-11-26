
# 简介
**my.previewImage** 是预览图片的 API。

## 使用限制

- 不支持本地图片路径。
- 基础库 版本 [1.0.0](https://opendocs.alipay.com/mini/framework/lib) 在 iOS 上不支持 `my.previewImage` 和 `my.chooseImage` 的组合使用。 
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|127x157](https://cdn.nlark.com/yuque/0/2021/jpeg/179989/1625191726620-5e45ee53-b35c-4a2f-9088-24c5dce03300.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&name=1.jpeg&originHeight=157&originWidth=127&size=19820&status=done&style=stroke&width=127)

## 效果示例
![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1625191739247-40979909-a04d-4601-bf9d-1a4903bf80f8.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=558650&status=done&style=stroke&width=300)

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
| urls | Array | 是 | 要预览的图片 HTTP 链接列表。<br />支持网络 url，apfilePath。 |
| current | Number | 否 | 当前显示图片索引，默认值为 0，即 urls 中的第一张图片。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |
| enablesavephoto | Boolean | 否 | 照片支持长按下载。<br />基础库 1.13.0 版本开始支持。 |
| enableShowPhotoDownload | Boolean | 否 | 是否在右下角显示下载入口。<br />基础库 1.13.0 版本开始支持。 |

