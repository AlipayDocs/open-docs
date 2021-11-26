
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
// .js
my.downloadFile({
  // 示例 url，并非真实存在
      url: 'http://documentExample.com/alipay.pdf',
      success({ apFilePath }) {
        my.hideLoading();
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
| filePath | String | 是 | 文件路径，可通过 [my.downloadFile](https://opendocs.alipay.com/mini/api/xr054r) 获得。 |
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

