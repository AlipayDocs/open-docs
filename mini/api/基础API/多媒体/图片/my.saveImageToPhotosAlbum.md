# 简介

保存图片到系统相册。

## 使用限制

- 基础库 [1.15.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// 网络地址图片
my.saveImageToPhotosAlbum({
  filePath:
    'https://gw.alipayobjects.com/zos/skylark-tools/public/files/66539db61b570eb2b7cf2df4241ea56c.png',
  complete(res) {
    console.log(res);
  },
});
```

## 入参

Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| filePath | String | 是 | 图片文件路径，支持网络地址、[本地临时文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6)、[本地缓存文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%BC%93%E5%AD%98%E6%96%87%E4%BB%B6)、[本地用户文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%94%A8%E6%88%B7%E6%96%87%E4%BB%B6)。<br>对本地用户文件的支持始于客户端 10.2.70 版本。<br>**如需保存 base64 图片数据，请参考后文常见问题示例代码。** |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

## 错误码

| **错误码** | **描述** |
| --- | --- |
| 2 | 参数无效，没有传 filePath 参数。 |
| 15 | 没有开启相册权限（iOS only）。 |
| 16 | 手机相册存储空间不足（iOS only）。 |
| 17 | 保存图片过程中的其他错误。一般情况下由于 filePath 的值不符合要求导致，请检查 filePath 值。 |

## 已知问题

连续调用 my.saveImageToPhotosAlbum 时只会触发 success 一次回调，规避办法：请在 my.saveImageToPhotosAlbum 的 complete 触发后再接着调用 my.saveImageToPhotosAlbum。例如：

```plain
Page({
  onReady() {
    // 连续保存多张图片
    this.saveImages([
      'https://gw.alipayobjects.com/zos/skylark-tools/public/files/66539db61b570eb2b7cf2df4241ea56c.png',
      'https://gw.alipayobjects.com/zos/skylark-tools/public/files/66539db61b570eb2b7cf2df4241ea56c.png',
      'https://gw.alipayobjects.com/zos/skylark-tools/public/files/66539db61b570eb2b7cf2df4241ea56c.png',
    ]);
  },
  async saveImages(filePaths) {
    for (const filePath of filePaths) {
      await new Promise(resolve => {
        my.saveImageToPhotosAlbum({
          filePath: filePath,
          complete(res) {
            console.log(res);
            resolve(res);
          }
        })
      })
    }
  }
});
```

# 常见问题

## Q：如何保存 base64 格式的图片到相册？

A：先通过 [my.downloadFile](https://opendocs.alipay.com/mini/api/xr054r) 接口将 base64 数据保存为本地文件，再通过 my.saveImageToPhotosAlbum 接口保存到相册。
示例代码：
```javascript
my.downloadFile({
  url: 'data:image/png;base64,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',
  success(res) {
    my.saveImageToPhotosAlbum({
      filePath: res.apFilePath,
      complete(res) {
        console.log(res);
      }
    });
  }
});
```
