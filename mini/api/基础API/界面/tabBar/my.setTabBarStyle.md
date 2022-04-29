# 简介
**my.setTabBarStyle** 是动态设置标签页（tabbar）的整体样式的 API，如文字颜色、标签背景色、标签边框颜色等。

相关问题可查看 [tabBar 常见问题](https://opendocs.alipay.com/mini/api/do7urq)。

## 使用限制

- 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- IDE 模拟器 1.13 及以上版本支持该接口调用。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// .js
my.setTabBarStyle({
  color: '#FF0000',
  selectedColor: '#00FF00',
  backgroundColor: '#0000FF',
  borderStyle: 'white'
})
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| color | HexColor | 是 | 标签（tab）上的文字默认颜色。 |
| selectedColor | HexColor | 是 | 标签（tab）上的文字选中时的颜色。 |
| backgroundColor | HexColor | 是 | 标签（tab）的背景色。 |
| borderStyle | String | 是 | 标签页（tabbar）上边框的颜色（边框高度 1 px）。<br />支持传参如下：<ul><li>black：对应色值为 `#FFE5E5E5` 。</li><li>white：对应色值为 `#FFFFFFFF`。</li><li>#开头的自定义的 RGB 色值，如 `#FFABABAE` 或 `#FFFFFF`。</li></ul> |
| success | Function | 否 | 接口调用成功的回调函数。 |
| fail | Function | 否 | 接口调用失败的回调函数。 |
| complete | Function | 否 | 接口调用结束的回调函数（调用成功、失败都会执行）。 |
