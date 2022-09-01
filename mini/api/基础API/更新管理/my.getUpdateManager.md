# 简介

**my.getUpdateManager** 获取**全局唯一**的版本更新管理器，用于管理小程序更新。关于小程序的更新机制，可以查看 [更新机制](https://opendocs.alipay.com/support/01rb0k) 文档。

## 使用限制

- 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
const updateManager = my.getUpdateManager();
updateManager.onCheckForUpdate(function (res) {
  // 检查更新结果
  console.log(res.hasUpdate);
});
updateManager.onUpdateReady(function () {
  my.confirm({
    title: '更新提示',
    content: '新版本已经准备好，是否重启应用？',
    success: function (res) {
      if (res.confirm) {
        // 新版本已经下载好，调用 applyUpdate 应用新版本并重启
        updateManager.applyUpdate();
      }
    },
  });
});
updateManager.onUpdateFailed(function () {
  // 新版本下载失败
});
```

## 返回值

返回值为 [UpdateManager](https://opendocs.alipay.com/mini/api/ngwgfi)。

# 常见问题 FAQ

## Q：如何测试更新管理功能？

A：查看 [如何测试更新管理功能](https://opendocs.alipay.com/support/01rb3e)。注意该配置只对 **IDE 模拟器**生效，真机调试、真机预览不生效。
