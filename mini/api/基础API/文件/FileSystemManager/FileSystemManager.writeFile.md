
# 简介
**FileSystemManager.writeFile** 用于写文件。

## 使用限制

- 基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 代码示例

### .js 示例代码
```javascript
let fs = my.getFileSystemManager();
fs.writeFile({
  filePath: `${my.env.USER_DATA_PATH}/test.txt`,
  data: 'some text or arrayBuffer',
  success: (res) => {
		console.log(res);
  }
})
```

## 入参
| **属性** | **类型** | **必填** | **默认值** | **描述** |
| --- | --- | --- | --- | --- |
| filePath | String | 是 | - | 要写入的文件路径。 |
| data | String/ArrayBuffer | 是 | - | 要写入的文本或二进制数据。 |
| encoding | String | 否 | utf8 | 指定写入文件的字符编码。 |
| success | Function | 否 | - | 调用成功的回调函数。 |
| fail | Function | 否 | - | 调用失败的回调函数。 |
| complete | Function | 否 | - | 调用结束的回调函数（调用成功、失败都会执行）。 |


### encoding 合法值
| **值** | **说明** |
| --- | --- |
| ascii | - |
| base64 | - |
| hex | - |
| binary | - |
| ucs2/ucs-2/utf16le/utf-16le | - |
| utf-8/utf8 | - |
| latin1 | - |


## 错误码
| **错误码** | **说明** |
| --- | --- |
| 10024 | 指定的路径没有写的权限 |
| 3 | 未知错误，文件写入失败 |
| 10028 | 写入文件单个超过10M或者写入文件夹超过50M |

