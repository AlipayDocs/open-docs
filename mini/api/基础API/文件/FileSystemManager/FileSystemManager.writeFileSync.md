
# 简介
[FileSystemManager.writeFile](https://opendocs.alipay.com/mini/api/022b6s) 的同步版本。

## 使用限制

- 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 此 API 暂不支持在 IDE 模拟器上测试，开发中请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 进行测试。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
const fs = my.getFileSystemManager();
const result = fs.writeFileSync(
  `${my.env.USER_DATA_PATH}/test.txt`,
  'some text or arrayBuffer',
  'utf8'
);
console.log(result);
```

## 入参

#### string filePath
要写入的文件路径 (本地路径)。

#### string|ArrayBuffer data
要写入的文本或二进制数据。

#### string encoding
指定写入文件的字符编码。

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
| 10024 | 指定的路径没有写的权限。 |
| 3 | 未知错误，文件写入失败。 |
| 10028 | 写入文件单个超过10M 或者写入文件夹超过 50M。 |



