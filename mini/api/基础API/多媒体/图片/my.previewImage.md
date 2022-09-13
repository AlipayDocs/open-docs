# 简介

**my.previewImage** 是预览图片的 API。

## 使用限制

- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![1.jpeg](https://cdn.nlark.com/yuque/0/2021/jpeg/179989/1625191726620-5e45ee53-b35c-4a2f-9088-24c5dce03300.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&name=1.jpeg&originHeight=157&originWidth=127&size=19820&status=done&style=stroke&width=127#alt=&width=127)

## 效果示例

![](https://gw.alipayobjects.com/mdn/rms_aba389/afts/img/A*QtdsQIBkcP8AAAAAAAAAAAAAARQnAQ#alt=&width=300)

# 接口调用

## 示例代码

### .js 示例代码

```javascript
my.previewImage({
  current: 2, // 默认显示第三张图片
  urls: [
    'https://img.alicdn.com/tps/TB1sXGYIFXXXXc5XpXXXXXXXXXX.jpg',
    'https://img.alicdn.com/tps/TB1pfG4IFXXXXc6XXXXXXXXXXXX.jpg',
    'https://img.alicdn.com/tps/TB1h9xxIFXXXXbKXXXXXXXXXXXX.jpg',
  ],
  enablesavephoto: true, // 长按下载
  enableShowPhotoDownload: true, // 右下角显示下载入口
  success: res => {
    console.log({ content: 'success回调' + JSON.stringify(res) });
  },
  fail: error => {
    my.alert({ content: 'fail回调' + JSON.stringify(error) });
  },
});
```

## 入参

Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| urls | Array | 是 | 要预览的图片地址。<br />支持网络 url、[本地临时文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6)、[本地缓存文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%BC%93%E5%AD%98%E6%96%87%E4%BB%B6)，[本地用户文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%94%A8%E6%88%B7%E6%96%87%E4%BB%B6)。 <br /> 注: iOS 10.2.70 开始支持[本地用户文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%94%A8%E6%88%B7%E6%96%87%E4%BB%B6)。 |
| current | Number | 否 | 显示第几张图片，默认值为 0，即 urls 中的第一个。 |
| enablesavephoto | Boolean | 否 | 照片支持长按下载。<br />基础库 1.13.0 版本开始支持。 |
| enableShowPhotoDownload | Boolean | 否 | 是否在右下角显示下载入口。<br />基础库 1.13.0 版本开始支持。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


## Fail 回调 错误码

| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 2 | 接口参数无效 | 检查入参是否正确 |
| 2 | 只支持 http/https 图片链接 | 确保图片 urls 为 https/http 协议的图片地址。 |


# 常见问题 FAQ

## Q：部分图片预览不显示怎么办？
A：原因是 my.previewImage 底层下载接口能力有欠缺，传入的图片地址底层下载库不支持。目前暂时可以通过调用 [my.downloadFile](https://opendocs.alipay.com/mini/api/xr054r) 将图片地址格式转换为下载库可以支持的格式，然后再调用 my.previewImage，即可预览成功。
