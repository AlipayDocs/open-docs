# 简介
**my.getTitleColor** 是获取导航栏背景色的 API。

## 使用限制

- 基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib)  或更高版本；支付宝客户端 10.1.50 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/examples/e8797275-4ed8-48ce-8d15-da107782c8ae) 

### .json 示例代码
```json
{
  "defaultTitle": "获取导航栏背景颜色"
}
```

### .axml 示例代码
```html
<!-- API-DEMO page/API/get-title-color/get-title-color.axml-->
<view>
  <view class="page-section-demo">
    <text>目前导航栏的背景色:</text>
    <input type="text" disabled="{{true}}" value="{{titleColor.color}}" />
  </view>
  <view class="page-section-btns">
    <view onTap="getTitleColor">获取导航栏背景颜色
    </view>
  </view>
</view>
```

### .js 示例代码
```javascript
// API-DEMO page/API/get-title-color/get-title-color.js
Page({
  data: {
    titleColor: {},
  },
  getTitleColor() {
    my.getTitleColor({
      success: (res) => {
        this.setData({
          titleColor: res.color
        })
      }
    })
  }
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| color | HexColor | 返回当前导航栏背景色。<br />ARGB 格式的十六进制颜色值，如 #323239FF。 |


# 常见问题

## Q：小程序右上角的 分享与收藏 可以设置颜色吗？

A：这是默认的，无法设置颜色。

## Q: 小程序标题栏文字颜色支持自定义吗？

A: 不支持用户手动设置文字颜色，只能根据标题栏背景颜色做动态显示，例如：设置黑色背景则显示白色文字，设置白色背景则显示黑色文字。

