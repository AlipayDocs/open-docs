# 简介

[FileSystemManager.saveFile](https://opendocs.alipay.com/mini/api/022b6n) 的同步版本。

## 使用限制

- 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
const fs = my.getFileSystemManager();
my.downloadFile({
  url: zipFileUrl, // 下载文件地址
  success: res => {
    const result = fs.saveFileSync(
      res.apFilePath,
      `${my.env.USER_DATA_PATH}/example`
    );
    console.log(result);
  },
});
```

## 入参

### String tempFilePath

临时存储文件路径。

### String filePath

要存储的文件路径。

**说明：** 如果不传，默认存储在小程序缓存目录

## 返回值

| **属性**      | **类型** | **描述**           |
| ------------- | -------- | ------------------ |
| savedFilePath | String   | 存储后的文件路径。 |

## 错误码

| **错误码** | **描述**                 |
| ---------- | ------------------------ |
| 10022      | 指定文件不存在。         |
| 10024      | 指定的路径没有写的权限。 |
