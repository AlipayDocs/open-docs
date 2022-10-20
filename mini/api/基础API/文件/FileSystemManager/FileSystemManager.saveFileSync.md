# 简介

[FileSystemManager.saveFile](https://opendocs.alipay.com/mini/api/022b6n) 的同步版本。

## 使用限制

- 基础库 [2.7.4](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。

# 接口调用
FileSystemManager.saveFileSync(tempFilePath, filePath)
## 示例代码

### .js 示例代码

保存为本地用户文件
```javascript
const fs = my.getFileSystemManager();
my.downloadFile({
  url: 'https://img.alicdn.com/tfs/TB1x669SXXXXXbdaFXXXXXXXXXX-520-280.jpg', // 下载文件地址，仅供参考
  success: res => {
    const result = fs.saveFileSync(
      res.apFilePath,
      `${my.env.USER_DATA_PATH}/example.jpg` // 保存为本地用户文件，若保存为本地缓存文件时可以不传
    );
    console.log(result);
  },
});
```
## 入参 

### String tempFilePath

要保存的 [本地临时文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6) 路径。

### String filePath

指定保存后的 [本地用户文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%94%A8%E6%88%B7%E6%96%87%E4%BB%B6) 路径，若不指定，则保存为 [本地缓存文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%BC%93%E5%AD%98%E6%96%87%E4%BB%B6)。

## 返回值
Object 类型的对象，其属性如下：
| **属性**      | **类型** | **描述**           |
| ------------- | -------- | ------------------ |
| savedFilePath | String   | 保存后的文件路径。 |

## 错误码

| **错误码** | **描述**                 |
| ---------- | ------------------------ |
| 10022      | 指定文件不存在。         |
| 10024      | 指定的路径没有写的权限。 |
