
# 简介
**my.downloadFile** 是下载文件资源到本地的 API。可下载任何格式的文件，不能被识别的文件将以 other 的方式存储起来。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/5730fab3a21f3a650e16da1c67526a1a.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例
![|368x662](https://gw.alipayobjects.com/zos/skylark-tools/public/files/699af658d03164470c0c18765d18e4f2.gif#align=left&display=inline&height=662&margin=%5Bobject%20Object%5D&originHeight=662&originWidth=368&status=done&style=stroke&width=368)

# 接口调用

## 示例代码
**注意**：案例仅供参考，建议使用自己的地址进行测试。
```json
{
    "defaultTitle": "下载文件"
}
```


```html
<!-- API-DEMO page/API/download-file/download-file.axml-->
<view class="container">
  <button onTap="download">下载图片并显示</button>
</view>
```


```javascript
// API-DEMO page/API/download-file/download-file.js
Page({
  download() {
    my.downloadFile({
      url: 'https://img.alicdn.com/tfs/TB1x669SXXXXXbdaFXXXXXXXXXX-520-280.jpg',
      success({ apFilePath }) {
        my.previewImage({
          urls: [apFilePath],
        });
      },
      fail(res) {
        my.alert({
          content: res.errorMessage || res.error,
        });
      },
    });
  },
})
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| url | String | 是 | 下载文件地址。 |
| header | Object | 否 | HTTP 请求 Header。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


### success 回调函数
入参为 Object 类型，属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| apFilePath | String | 文件临时存放的位置。 |


## 错误码
| **错误码** | **说明** | **解决方案** |
| --- | --- | --- |
| 12 | 下载失败。 | 建议检查网络和服务器。 |
| 13 | 没有权限。 | 建议检查权限。 |
| 20 | 请求的 URL 不支持 HTTP。 | 建议将请求的 URL 改成 HTTPS。 |

