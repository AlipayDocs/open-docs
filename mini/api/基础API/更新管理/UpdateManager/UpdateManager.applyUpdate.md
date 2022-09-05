# 简介

**UpdateManager.applyUpdate** 用于小程序新版本下载完成（即收到 [onUpdateReady](https://opendocs.alipay.com/mini/api/gfz316) 回调）后提示用户重启小程序以使用新版本。

## 使用限制

此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
const updateManager = my.getUpdateManager();
updateManager.onUpdateReady(function () {
  my.confirm({
    title: "更新提示",
    content: "新版本已经准备好，是否重启应用？",
    success: function (res) {
      if (res.confirm) {
        // 新版本已经下载好，调用 applyUpdate 应用新版本并重启
        updateManager.applyUpdate();
      }
    },
  });
});
```
