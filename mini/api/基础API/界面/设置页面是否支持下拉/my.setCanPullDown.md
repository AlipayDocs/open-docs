# 简介

**my.setCanPullDown** 是设置页面是否支持下拉（小程序内页面默认支持下拉）的 API。

## 使用限制

- 支付宝客户端 10.1.35 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
my.setCanPullDown({
  canPullDown: true,
});
```

## 入参

入参为 Object 类型，属性如下：

| **属性**    | **类型** | **必填** | **描述**       |
| ----------- | -------- | -------- | -------------- |
| canPullDown | Boolean  | 是       | 是否支持下拉。 |
