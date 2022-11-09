MediaQueryObserver 对象，用于监听页面 media query 状态的变化，如界面的长宽是不是在某个指定的范围内。

## 使用限制

- 基础库 [2.8.2](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上版本。若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 接口调用

### 示例代码

#### .js 示例代码
```javascript
Component({
  didMount() {
    const mediaQueryObserver = this.createMeidaQueryObservers();
    mediaQueryObserver.observe(
      {minWidth: 100},
      res => {
        console.log(res.matches);
      }
    );
    // mediaQueryObserver.disconnect();
  }
})
```

### 方法

#### MediaQueryObserver.observe(Object descriptor, MediaQueryObserver.observeCallback callback)
开始监听页面 media query 变化情况。

#### MediaQueryObserver.disconnect()
停止监听。回调函数将不再触发。
