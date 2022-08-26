# 简介

关闭监听获取到 Wi-Fi 列表数据的事件。

# 使用限制

- **基础库** [1.11.0](https://opendocs.alipay.com/mini/framework/compatibility) 开始支持。若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
my.offGetWifiList(this.callback);
```

## 入参

**function callback**

获取到 Wi-Fi 列表数据的事件回调。

**注意：** 若 my.offGetWifiList 没有传入任何 callback 参数，则会取消监听所有的获取到 Wi-Fi 列表数据的事件回调函数。
