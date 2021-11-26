
# 简介
**my.getFileSystemManager** 获取全局唯一的文件管理器。如何接入以及更多介绍信息，请参见 [文件管理器](https://opendocs.alipay.com/mini/introduce/022rw2)。

## 使用限制

- 基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
let fs = my.getFileSystemManager();
```

## 返回值
[FileSystemManager](https://opendocs.alipay.com/mini/api/0226od) 文件管理器。
