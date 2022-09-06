# 简介

**FileSystemManager.readFile** 用于读取本地文件内容。

## 使用限制

- 基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 读取小程序包内容前需在 mini.project.json 中配置可读取的小程序文件内容。
- 填写地址为文件的绝对路径，\*代表任意的名称，需要开发者自行填写。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .json 示例代码

在 mini.project.json 中配置要读取的小程序文件内容：

```json
{
  "include": ["resource/*.txt", "resource/*.json"]
}
```

### .js 示例代码

```javascript
let fs = my.getFileSystemManager();
fs.readFile({
  filePath: `${my.env.USER_DATA_PATH}/test.txt`,
  encoding: 'utf8',
  success: res => {
    console.log(res);
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| filePath | String | 是 | 文件路径。 |
| encoding | String | 否 | 指定读取文件的字符编码方式（**注**，binary 为二进制），如果不传 encoding，则以 ArrayBuffer 格式读取文件的二进制内容。<br />可选值：<ul><li>ascii</li><li>base64</li><li>hex</li><li>binary</li><li>ucs2/ucs-2/utf16le/utf-16le</li><li>utf-8/utf8</li><li>latin1</li></ul> |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| data | string/ArrayBuffer | 文件内容。 |
| dataType | String | 如果入参不传 encoding，默认输出 "ArrayBuffer"。如果传了 encoding，则不会输出 dataType 这个字段。 |

## 错误码

| **错误码** | **描述**               |
| ---------- | ---------------------- |
| 10022      | 文件/目录不存在。      |
| 10024      | 指定的路径没有读权限。 |
| 3          | 文件读取未知错误。     |
