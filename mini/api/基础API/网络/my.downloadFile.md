# 简介

**my.downloadFile** 是下载文件资源到本地的 API。

## 使用限制

- 仅可下载 HTTPS 资源或 [Data URL](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Data_URLs)，文件下载后保存为[本地临时文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6)。
- 如果文件格式不能被识别，则会以 `.other` 类型的文件进行存储。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/5730fab3a21f3a650e16da1c67526a1a.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例

![|368x662](https://gw.alipayobjects.com/zos/skylark-tools/public/files/699af658d03164470c0c18765d18e4f2.gif#align=left&display=inline&height=662&margin=%5Bobject%20Object%5D&originHeight=662&originWidth=368&status=done&style=stroke&width=368)

# 接口调用

## 示例代码

**注意**：案例仅供参考，建议使用自己的地址进行测试。

```javascript
my.downloadFile({
  url: 'https://img.alicdn.com/tfs/TB1x669SXXXXXbdaFXXXXXXXXXX-520-280.jpg',
  success(res) {
    // 基础库 2.7.23 开始支持返回 tempFilePath
    if (my.canIUse('downloadFile.return.tempFilePath')) {
      my.previewImage({
        urls: [res.tempFilePath],
      });
    } else {
      my.previewImage({
        urls: [res.apFilePath],
      });
    }
  },
  fail(res) {
    my.alert({
      content: res.errorMessage || res.error,
    });
  },
});
```

## 入参

Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| url | String | 是 | 下载文件地址。除在线 URL 以外，也接受包含图片 base64 数据的 [Data URL](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Data_URLs) |
| header | Object | 否 | HTTP 请求 Header。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### success 回调函数

success 回调会收到一个 Object 类型的参数，属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| apFilePath | String | 文件临时存放的位置（[本地临时文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6)）。 |
| tempFilePath | String | 文件临时存放的位置（本地临时文件）<br/> 实际与 apFilePath 相同，基础库 [2.7.23](https://opendocs.alipay.com/mini/ide/framework-changelog-v2) 开始支持。 |

### 错误码

| **错误码** | **说明** | **解决方案** |
| --- | --- | --- |
| 12 | 下载失败。 | 检查 URL 是否有误、服务器状态是否正常；也可能为网络问题，可请用户稍后重试。 |
| 20 | 请求的 URL 不支持 HTTP。 | 使用 HTTPS 协议的 URL。 |

## 常见问题 FAQ

### Q: my.downloadFile 接口下载的文件在哪里？

- 通过 my.downloadFile 接口下载的文件，其路径样式符合 `https://resource/xxx` 类型，属于[本地临时文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6)。本地临时文件随时有可能会被回收，推荐使用 my.saveFile 接口将下载后的文件存储为[本地缓存文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%BC%93%E5%AD%98%E6%96%87%E4%BB%B6)，代码示例详见[此处](https://opendocs.alipay.com/mini/03dt4s#%E7%A4%BA%E4%BE%8B%E4%BB%A3%E7%A0%81)。

### Q: my.downloadFile 都支持哪些类型？支持下载 PDF 文件吗？

- 支持下载任何类型的文件，包含 PDF 文件。需要**注意**的是，如果未能根据文件头信息获取到正确的拓展名信息，则将以 `.other` 的后缀名进行存储。
- PDF 的下载及预览，可参考 [my.openDocument](https://opendocs.alipay.com/mini/api/mwpprc) 的代码示例。

### Q: 为什么我下载的 PDF 文件通过 my.openDocument 接口预览时出现渲染异常？

- 低版本支付宝客户端里 my.openDocument 接口在预览 PDF 时存在兼容性问题，10.2.80 及以上版本已解决。如果高版本仍有问题，请联系技术支持反馈。
