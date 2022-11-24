# 简介

**my.downloadFile** 用于下载文件到本地。

# 接口调用

## 示例代码

```javascript
// 示例一：不指定 filePath，保存为本地临时文件
my.downloadFile({
  url: 'https://img.alicdn.com/tfs/TB1x669SXXXXXbdaFXXXXXXXXXX-520-280.jpg',
  success(res) {
    my.previewImage({
      urls: [ res.apFilePath ] // apFilePath 为图片时，扩展名将为 .image
    });
  },
  fail(res) {
    alert({
      title: 'downloadFile fail',
      content: JSON.stringify(res)
    });
  },
});

// 示例二：指定文件下载后存储的路径 (本地路径)
my.downloadFile({
  url: 'https://my.com/my.pdf', // 请替换为有效的 url
  filePath: `${my.env.USER_DATA_PATH}/my.pdf`, // 指定存储路径
  success(res) {
    my.openDocument({
      fileType: 'pdf',
      filePath: res.filePath // 与入参 filePath 相同
    });
  },
  fail(res) {
    alert({
      title: 'downloadFile fail',
      content: JSON.stringify(res)
    });
  },
});
```

## 入参

Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| url | String | 是 | 下载地址。支持 HTTPS，不支持 HTTP。除在线 URL 以外，也接受包含图片 base64 数据的 [Data URL](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Data_URLs)。 |
| filePath | string | 否 | 指定文件下载后存储的路径 ([本地路径](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%94%A8%E6%88%B7%E6%96%87%E4%BB%B6))。若不指定此参数，下载的文件会被存储为[本地临时文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6)。参见代码示例。<br> **注意**：目前 IDE 暂不支持此参数。建议使用真机测试。 |
| header | Object | 否 | HTTP 请求头。 |
| timeout | Number | 否 | 超时时间，默认值 60000，单位 ms。<br> **注意**：目前 IDE 暂不支持此参数。建议使用真机测试。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

## 出参

success 回调会收到一个 Object 类型的参数，属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| apFilePath | String | 下载文件保存的路径（[本地临时文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6)）。入参未指定 filePath 的情况下可用。 |
| tempFilePath | String | 与 apFilePath 相同。基础库 [2.7.23](https://opendocs.alipay.com/mini/ide/framework-changelog-v2) 开始支持。 |
| filePath | String | 下载文件保存的路径（[本地用户文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%94%A8%E6%88%B7%E6%96%87%E4%BB%B6)），与入参指定的 filePath 相同。|


## 错误码

fail 回调会收到一个 Object 类型的参数，其 error 字段为错误码：

| **错误码** | **说明** | **解决方案** |
| --- | --- | --- |
| 2 | 参数无效。 | 检查传入的 url、filePath 等参数是否有效。 |
| 12 | 下载失败。 | 检查传入的 url 是否有误、服务器状态是否正常；也可能为网络问题，可请用户稍后重试。 |
| 20 | 不支持下载 HTTP 资源。 | 使用 HTTPS 协议的 url。 |


## 常见问题 FAQ

### Q: my.downloadFile 接口下载的文件在哪里？

A: my.downloadFile 保存的文件路径可从出参 apFilePath 或 filePath 获取，两者均为内部虚拟路径，只能通过小程序的 API 访问。暂不支持保存文件到外部存储。如有图片需要保存到系统相册，可使用 my.saveImageToPhotosAlbum()。

### Q: my.downloadFile 都支持哪些类型？支持下载 PDF 文件吗？

A: my.downloadFile 支持下载任何类型的文件，包含 PDF。**注意：**在未指定 filePath 的情况下，my.downloadFile 产生的本地临时文件，其扩展名由文件实际内容确定，可能为以下几种之一：.image、.video、.audio、.pdf、.other。

### Q: 为什么我下载的 PDF 文件通过 my.openDocument 接口预览时出现渲染异常？

A: 较低版本支付宝客户端上 my.openDocument 接口在预览 PDF 时存在兼容性问题，10.2.80 及以上版本已解决。如果发现新版本仍有问题，请联系技术支持反馈。
