# 简介
**my.getMapInfo** 是获取地图基础信息的 API，在使用 [map 地图组件](https://opendocs.alipay.com/mini/component/map) 之前进行兼容逻辑操作。

## 使用限制

- 基础库 [1.24.6](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.95 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// .js
my.getMapInfo({
  success: res => {
    console.log(res);
  }
});
```

## success 回调函数
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| is3d | Boolean | 是否为 3D 地图引擎。 |
| isSupportAnim | Boolean | 是否支持动画。 |
| sdkName | String | SDK 名称。 |
| sdkVersion | String | SDK 版本号。 |
| isSupportOversea | Boolean | 是否支持海外地图。 |
| needStyleV7 | Boolean | 需要 7.x 版本的样式文件。 |
