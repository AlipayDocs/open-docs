
# 简介
**my.openDocument** 是在新页面打开文件预览的 API，暂时只支持预览 PDF 格式文件。

## 使用限制

- 基础库 [1.15.0 ](https://opendocs.alipay.com/mini/framework/lib)或更高版本，支付宝客户端 10.1.60 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- my.openDocument 只支持在真机上测试，无法在 IDE 上调试。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
my.downloadFile({
  // 示例 url，并非真实存在
  url: 'http://documentExample.com/alipay.pdf',
  success({ apFilePath }) {
    my.openDocument({
      filePath: apFilePath,
      fileType: 'pdf',
      success: (res) => {
        console.log('open document success')
      }
    })
  }
})
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| filePath | String | 是 | 文件路径([本地临时文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6)、[本地缓存文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%BC%93%E5%AD%98%E6%96%87%E4%BB%B6)、[本地用户文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%94%A8%E6%88%B7%E6%96%87%E4%BB%B6))。其中本地缓存文件、本地用户文件路径客户端10.2.60开始支持，之前的客户端版本存在兼容性问题。 |
| fileType | String | 否 | 文件类型。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


### fileType 合法值
| **值** | **说明** |
| --- | --- |
| pdf | PDF 格式。 |


## 错误码
| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 4011 | 无效的文件路径，或者传入路径没有权限访问。 | 检查传入的文件路径。 |
| 4012 | 预览文件不存在。 | 确保文件路径对应的文件存在。 |
| 4013 | 文件类型暂不支持。 | 目前暂仅支持 PDF 文件格式的预览 。 |

# Bug & Tips

- iOS: 10.2.60之前的版本不支持[本地缓存文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%BC%93%E5%AD%98%E6%96%87%E4%BB%B6)。
- Android: 10.2.60之前的版本不支持[本地用户文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%94%A8%E6%88%B7%E6%96%87%E4%BB%B6)。
- iOS: 通过[my.downloadFile](https://opendocs.alipay.com/mini/api/xr054r)获取的本地临时文件路径可能因为下载的文件头信息设置不规范进而打开失败(由于系统原因)。可通过将本地临时文件保存为本地用户文件（指定`filePath`值带`pdf`后缀）来规避，例如：

```javascript
// 注：如何接入文档管理器（my.getFileSystemManager）请查看文档 https://opendocs.alipay.com/mini/introduce/022rw2
const fs = my.getFileSystemManager();
my.downloadFile({
  // 示例 url，并非真实存在
  url: "http://documentExample.com/alipay.pdf",
  success(res) {
    fs.saveFile({
      tempFilePath: res.apFilePath,
      filePath: `${my.env.USER_DATA_PATH}/alipay.pdf`,
      success(res1) {
        my.openDocument({
          filePath: res1.savedFilePath,
          fileType: 'pdf',
        })
      }
    })
  }
});
```
