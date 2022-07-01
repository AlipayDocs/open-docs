# 简介

**my.getFileSystemManager** 获取全局唯一的文件管理器，用于文件及目录读写等操作。更多介绍信息，可查看 [FileSystemManager 概览](https://opendocs.alipay.com/mini/api/0226od)。

调用此 API 前，需要登录 [支付宝开放平台](https://open.alipay.com/develop/manage)，点击进入对应小程序详情页，在 **能力管理** 中添加 **文件管理器**。

## 使用限制

- 基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
let fs = my.getFileSystemManager();
// 
fs.readFile({
  filePath: `${my.env.USER_DATA_PATH}/test.txt`,
  encoding: "utf8",
  success: (res) => {
    console.log(res);
  }
});
```

## 返回值
[FileSystemManager](https://opendocs.alipay.com/mini/api/0226od) 文件管理器。
