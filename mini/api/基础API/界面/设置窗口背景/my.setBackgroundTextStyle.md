# 简介

**my.setBackgroundTextStyle** 是动态设置下拉  loading  页面的文字颜色的 API。

## 使用限制

此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
my.setBackgroundTextStyle({
  textStyle: 'dark', // 下拉 loading 页面的文字颜色为dark
});
```

## 入参

入参为 Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| textStyle | String | 是 | 下拉背景字体、loading 图的样式，仅支持 'dark', 'light'。 |
| success | Function | 否 | 接口调用成功的回调函数。 |
| fail | Function | 否 | 接口调用失败的回调函数。 |
| complete | Function | 否 | 接口调用结束的回调函数（调用成功、失败都会执行）。 |
