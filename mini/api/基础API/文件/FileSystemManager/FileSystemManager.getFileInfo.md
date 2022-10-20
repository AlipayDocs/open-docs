# 简介

**FileSystemManager.getFileInfo** 获取该小程序下的 [本地文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E6%96%87%E4%BB%B6) 信息。

## 使用限制

- 基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
let fs = my.getFileSystemManager();
fs.getFileInfo({
  filePath: `${my.env.USER_DATA_PATH}/test.txt`, // 支持其它类型文件，这里以 txt 文件示例。
  success: res => {
    console.log(res);
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| filePath | String | 是 | 本地文件路径（[本地临时文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6)、[本地缓存文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%BC%93%E5%AD%98%E6%96%87%E4%BB%B6)、[本地用户文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%94%A8%E6%88%B7%E6%96%87%E4%BB%B6)）。 |
| digestAlgorithm | String | 否 | 生成文件摘要的算法，默认 md5。<br/> 可选值：<ul><li>md5：生成 16 个字节，32 个 16 进制数字的字符。</li><li>sha1：生成 20 个字节，40 个 16 进制数字的字符。</li></ul>|
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调会携带一个 Object 类型的对象，其参数如下：

| **属性** | **类型** | **说明**                 |
| -------- | ------- | ------------------------ |
| size     | Number  | 文件大小，以字节为单位。 |
| digest   | String  | 生成的摘要。 |
## 错误码

| **错误码** | **描述**               |
| ---------- | ---------------------- |
| 10024      | 指定文件没有读的权限。 |
