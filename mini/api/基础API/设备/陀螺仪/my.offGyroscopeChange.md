
# 简介
**my.offGyroscopeChange** 是停止监听陀螺仪数据的 API。

## 使用限制

- 基础库 [1.9.0](https://opendocs.alipay.com/mini/framework/lib)  或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码
```javascript
my.offGyroscopeChange();
```

### 是否需要传 callback 值

- 不传递 callback 值，则会移除监听所有的事件回调。示例代码如下：
```javascript
my.offGyroscopeChange();
```


- 传递 callback 值，只移除对应的 callback 事件。示例代码如下：
```javascript
my.offGyroscopeChange(this.callback);
```
