
# 简介
[FileSystemManager.readFile](https://opendocs.alipay.com/mini/api/0226oj) 的同步版本。

## 使用限制

- 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 读取小程序包内容前需在 mini.project.json 中配置可读取的小程序文件内容。
- 填写地址为文件的绝对路径，* 代表任意的名称，需要开发者自行填写。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 此 API 暂不支持在 IDE 模拟器上测试，开发中请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 进行测试。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
const fs = my.getFileSystemManager();
const res = fs.readFileSync(`${my.env.USER_DATA_PATH}/test.txt`, "utf8");
console.log(res);
```

## 入参

#### string filePath
文件地址。

#### string encoding
指定读取文件的字符编码，如果不传 encoding，则以 ArrayBuffer 格式读取文件的二进制内容。

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


## 返回值
| **属性** | **类型** | **说明** |
| --- | --- | --- |
| data | string/ArrayBuffer | 文件内容。 |
| dataType | String | 如果未传入 dataType，则默认以 arrayBuffer 读取数据。 |


## 错误码
| **错误码** | **说明** |
| --- | --- |
| 10022 | 文件/目录不存在。 |
| 10024 | 指定的路径没有读权限。 |
| 3 | 文件读取未知错误。 |


## 读取小程序包内容
内容配置为要读取的内容：
```json
{
  "include": [
    "resource/*.txt",
    "resource/*.json"
  ]
}
```
