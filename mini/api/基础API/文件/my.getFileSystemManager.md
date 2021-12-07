
# 简介
**my.getFileSystemManager** 获取全局唯一的文件管理器。如何接入以及更多介绍信息，请参见 [文件管理器](https://opendocs.alipay.com/mini/introduce/022rw2)。

## 使用限制

- 基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 添加能力
小程序创建完成后，开发者登录 开放平台控制台> 找到已创建的小程序 > 点击进入小程序管理后台 >在 版本管理 页面的 能力列表 部分点击添加能力 > 勾选 文件管理器 能力并点击 确定 完成能力添加。
![image](https://cdn.nlark.com/yuque/0/2021/png/179989/1632723260442-7f25bf73-7450-47e5-a8f8-070f9e45cf94.png?x-oss-process=image%2Fresize%2Cw_1436)


# 接口调用

## 示例代码

### .js 示例代码
```javascript
let fs = my.getFileSystemManager();
```

## 返回值
[FileSystemManager](https://opendocs.alipay.com/mini/api/0226od) 文件管理器。
