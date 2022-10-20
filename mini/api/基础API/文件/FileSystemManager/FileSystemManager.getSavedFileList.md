# 简介

**FileSystemManager.getSavedFileList** 获取该小程序下已保存的 [本地缓存文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%BC%93%E5%AD%98%E6%96%87%E4%BB%B6) 列表。

## 使用限制

- 基础库 [1.3.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
let fs = my.getFileSystemManager();
fs.getSavedFileList({
  success: res => {
    console.log('从fileList文件数组中取值', res.fileList);
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型**        | **说明**   |
| -------- | --------------- | ---------- |
| fileList | Array\<Object\> | 文件数组。 |

#### Object fileList

| **属性** | **类型** | **说明** |
| --- | --- | --- |
| filePath | String | [本地缓存文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%BC%93%E5%AD%98%E6%96%87%E4%BB%B6) 路径。 |
| size | Number | 本地文件大小，以字节（B）为单位。 |
| createTime | Number | 文件保存时的时间戳，从 1970/01/01 08:00:00 到当前时间的秒数。 |
