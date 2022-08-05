
# 简介
**my.SDKVersion** 是获取基础库版本号的 API。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/fcc0c9ce29b9e4aaaafbff09963ab8f6.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

## 效果示例
![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/001a7b0119688f18184236143cc2c1e3.gif#align=left&display=inline&height=525&margin=%5Bobject%20Object%5D&originHeight=525&originWidth=300&status=done&style=none&width=300)

# 接口调用

## 示例代码
示例代码仅供参考，代码逻辑请勿依赖此值。

### .axml 示例代码
```html
<!-- API-DEMO page/API/sdk-version/sdk-version.axml-->
<view class="page">
  <view class="page-description">获取基础库版本号 API</view>
  <view class="page-section">
    <view class="page-section-title">my.SDKVersion</view>
    <view class="page-section-demo">
      <button type="primary" onTap="getSDKVersion">获取基础库版本号</button>
    </view>
  </view>
</view>
```

### .js 示例代码
```javascript
// API-DEMO page/API/sdk-version/sdk-version.js
Page({
  getSDKVersion() {
    my.alert({
      content: my.SDKVersion,
    });
  }, 
});
```

## 返回值
为 `String` 类型，表示基础库版本号。

# 常见问题
## Q：IDE 中选择基础库版本号后不生效，怎么办？
A：如果项目本身使用了 1.x 的基础库，需要 IDE 的项目详情中勾选 `启用小程序基础库 2.0 构建`。

