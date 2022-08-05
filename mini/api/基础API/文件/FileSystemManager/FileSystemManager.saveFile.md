# 简介

**FileSystemManager.saveFile** 用于将临时文件保存为本地用户文件或本地缓存文件。

如果指定存储的文件路径（filePath），则保存为[本地用户文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%94%A8%E6%88%B7%E6%96%87%E4%BB%B6)，否则保存为[本地缓存文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%BC%93%E5%AD%98%E6%96%87%E4%BB%B6)。

注意：此接口实质是移动文件，调用成功后，原临时文件将不复存在。


## 使用限制

- 基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

保存为本地用户文件：

```javascript
let fs = my.getFileSystemManager();
my.chooseImage({
  count: 1,
  success(res) {
  	fs.saveFile({
      tempFilePath: res.apFilePaths[0],
      filePath: `${my.env.USER_DATA_PATH}/img.png`,
      success: (res1) => {
        console.log(res1.savedFilePath);
      }
    })
  }
});
```

保存为本地缓存文件：

```JavaScript
let fs = my.getFileSystemManager();
my.downloadFile({
  url: 'https://img.alicdn.com/tfs/TB1x669SXXXXXbdaFXXXXXXXXXX-520-280.jpg',
  success({ apFilePath }) {
    console.log(JSON.stringify(apFilePath))
    fs.saveFile({
      tempFilePath: apFilePath,
      success: (res1) => {
        console.log(res1.savedFilePath)
      }
    })
  },
  fail(res) {
    my.alert({
      content: res.errorMessage || res.error,
    });
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| tempFilePath | String | 是 | 临时存储文件路径。 |
| filePath | String | 否 | 要存储的文件路径。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

**说明**：如果不传 filePath，默认存储在小程序缓存目录。

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **名称** | **类型** | **描述** |
| --- | --- | --- |
| savedFilePath | String | 存储后的文件路径。 |

## 错误码
| **错误码** | **描述** |  **解决方案** |
| --- | --- | --- |
| 10022 | 指定文件不存在。 | 检查临时文件是否存在 |
| 10024 | 指定的路径没有写的权限。 | 检查是否有权限写入 |
| 10028 | 单个文件大小超出上限 10MB / 超出最大存储量 50MB。 | 更换文件 / [FileSystemManager.removeSavedFile](https://opendocs.alipay.com/mini/api/0229pv) 删除缓存 |

# 常见问题 FAQ

## Q: 调用 FileSystemManager.saveFile 保存成功之后，文件保存在哪里了，怎么可以找到？
A: 不论传入不传入 filePath，FileSystemManager.saveFile 保存之后返回的路径都是虚拟路径，需要通过小程序内的 API 才能访问。如果是图片文件，可通过
 [my.saveImageToPhotosAlbum](https://opendocs.alipay.com/mini/api/media/image/my.saveImagetophotosalbum) 保存到系统相册，到相册中找到。
