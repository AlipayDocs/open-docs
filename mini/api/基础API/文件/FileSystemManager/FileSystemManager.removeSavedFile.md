# 简介

**FileSystemManager.removeSavedFile** 是删除该小程序下已保存的 [本地缓存文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%BC%93%E5%AD%98%E6%96%87%E4%BB%B6) 的API。

## 使用限制

- 基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

// 从已保存的本地缓存文件中删除一个。
```javascript
let fs = my.getFileSystemManager();
my.getSavedFileList({
  success: res => {
    console.log(res.fileList[0])
    if (!res.fileList[0]) return;
    fs.removeSavedFile({
      filePath: res.fileList[0].apFilePath,
      success: res1 => {
        console.log('删除成功');
      },
    });
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| filePath | String | 是 | 需要删除的 [本地缓存文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%BC%93%E5%AD%98%E6%96%87%E4%BB%B6) 路径。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

## 错误码

| **错误码** | **描述**             |
| ---------- | -------------------- |
| 10022      | 文件/目录不存在。    |
| 10024      | 指定路径没有写权限。 |
| 15         | 删除文件失败。       |
