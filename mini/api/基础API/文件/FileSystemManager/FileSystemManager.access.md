# 简介

**FileSystemManager.access** 判断文件/目录是否存在。

## 使用限制

- 基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 仅支持校验本地文件是否存在，不支持包文件判断。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
let fs = my.getFileSystemManager();
fs.access({
  path: `${my.env.USER_DATA_PATH}/test.txt`,
  success: res => {
    console.log('文件存在'，res);
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| path | String | 是 | 当前小程序内[文件系统](https://opendocs.alipay.com/mini/03dt4s) 中的文件夹路径或者文件路径。 |
| success | Function | 否 | 调用成功的回调函数 |
| fail | Function | 否 | 调用失败的回调函数 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行） |

## 错误码

| **错误码** | **说明**               |
| ---------- | ---------------------- |
| 10022      | 文件/目录不存在        |
| 10024      | 传入的路径没有读的权限 |
