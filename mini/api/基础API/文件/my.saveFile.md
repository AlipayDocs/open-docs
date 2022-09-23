**此 API 已停止维护，推荐使用 [FileSystemManager.saveFile](https://opendocs.alipay.com/mini/api/022b6n)，历史接入此 API 的小程序不受影响。**

# 简介

**my.saveFile** 是将临时文件保存为本地缓存文件的 API。

临时文件一般会在退出小程序后删除，而本地缓存文件则不会被删，除非用户从“我的小程序”删除当前小程序，或者开发者调用 [my.removeSavedFile](https://opendocs.alipay.com/mini/api/dgi1fr) 等 API 主动删除。

**注意：** 此 API 已不再维护，推荐使用 [FileSystemManager.saveFile](https://opendocs.alipay.com/mini/api/022b6n) 替代。

## 使用限制

- 基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本，支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

```javascript
my.chooseImage({
  success: res => {
    my.saveFile({
      apFilePath: res.apFilePaths[0],
      success: (res) => my.alert({ title: "my.saveFile success", content: JSON.stringify(res) }),
      fail: (err) => my.alert({ title: "my.saveFile fail", content: JSON.stringify(err) }),
    });
  },
});
```

## 入参

Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| apFilePath | String | 是 | 要保存的 [本地临时文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6) 路径。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### success 回调函数

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| apFilePath | String | 保存得到的([本地缓存文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%BC%93%E5%AD%98%E6%96%87%E4%BB%B6))文件路径。 |

## 错误码
| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 2 | apFilePath 参数为空。 | 传入非空的 apFilePath。|
| 12 | 文件不存在。 | 确保传入的 apFilePath 是有效的本地临时文件路径。  |
| 13 | 文件保存失败。 | 发生未知错误，请重试或放弃操作。|
| 19 | 文件存储大小限制为 10M。 | 传入 10M 以下的临时文件。 |

## 常见问题

### Q: 通过 my.saveFile 保存的文件能否在系统中找到？
- my.saveFile 保存的本地缓存文件为虚拟路径，只能通过小程序 API 访问。如果是图片文件，可以使用 [my.saveImageToPhotosAlbum](https://opendocs.alipay.com/mini/api/media/image/my.saveImagetophotosalbum) 保存然后在系统相册中找到。 

