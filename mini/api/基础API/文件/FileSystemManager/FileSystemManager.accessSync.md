# 简介

[FileSystemManager.access](https://opendocs.alipay.com/mini/api/0226oe) 的同步版本。

## 使用限制

- 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
let fs = my.getFileSystemManager();
let result = fs.accessSync(`${my.env.USER_DATA_PATH}/test.txt`);
console.log(result);
```

## 入参

### String path

当前小程序[文件系统](https://opendocs.alipay.com/mini/03dt4s) 中的文件夹路径或者文件路径

## 错误码

| **错误码** | **说明**                 |
| ---------- | ------------------------ |
| 10022      | 文件 / 目录不存在。      |
| 10024      | 传入的路径没有读的权限。 |
