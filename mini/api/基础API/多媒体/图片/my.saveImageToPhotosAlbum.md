# 简介
保存图片到系统相册。

## 使用限制

- 基础库 [1.15.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// 网络地址图片
my.saveImageToPhotosAlbum({
  filePath:'https://gw.alipayobjects.com/zos/skylark-tools/public/files/66539db61b570eb2b7cf2df4241ea56c.png',
  complete(res) {
    console.log(res);
  }
});
```

## 入参

Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| filePath | String | 是 | 图片文件路径，支持网络地址、[本地临时文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6)、[本地缓存文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%BC%93%E5%AD%98%E6%96%87%E4%BB%B6)、[本地用户文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%94%A8%E6%88%B7%E6%96%87%E4%BB%B6)。<br>对本地用户文件的支持始于客户端 10.2.70 版本。 |
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
连续调用 my.saveImageToPhotosAlbum 时只会触发 success一次回调，规避办法：请在 my.saveImageToPhotosAlbum 的 complete 触发后再接着调用 my.saveImageToPhotosAlbum。例如：
  ```
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
A：可以先通过 [my.downloadFile](https://opendocs.alipay.com/mini/api/xr054r) 接口下载 base64 图片到本地，再通过 my.saveImageToPhotosAlbum 接口保存到相册。
