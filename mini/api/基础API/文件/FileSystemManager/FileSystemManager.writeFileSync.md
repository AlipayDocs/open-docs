# 简介
[FileSystemManager.writeFile](https://opendocs.alipay.com/mini/api/022b6s) 的同步版本。

## 使用限制

- 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。

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

### String filePath
要写入的文件路径 (本地路径)。

### String|ArrayBuffer data
要写入的文本或二进制数据。

### String encoding

指定写入文件的字符编码。

可选值：<ul><li>ascii</li><li>base64</li><li>hex</li><li>binary</li><li>ucs2/ucs-2/utf16le/utf-16le</li><li>utf-8/utf8</li><li>latin1</li></ul>

## 错误码

| **错误码** | **描述** |
| --- | --- |
| 10024 | 指定的路径没有写的权限。 |
| 3 | 未知错误，文件写入失败。 |
| 10028 | 写入文件单个超过 10M 或者写入文件夹超过 50M。 |
