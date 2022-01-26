
# 简介
保存图片到系统相册。

## 使用限制

- 基础库 [1.15.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。
- 开发者工具暂不支持此能力，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// 本地路径图片
my.chooseImage({
  success: (result) => {
    my.saveImageToPhotosAlbum({
      filePath:result.apFilePaths[0],
      complete(res) {
        console.log(res);
      }
    });
  }
});
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
| filePath | String | 是 | 图片文件路径。支持本地路径和网络路径。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


## 错误码
| **错误码** | **错误码说明** |
| --- | --- |
| 2 | 参数无效，没有传 filePath 参数。 |
| 15 | 没有开启相册权限(iOS only)。 |
| 16 | 手机相册存储空间不足(iOS only)。 |
| 17 | 保存图片过程中的其他错误。 |

