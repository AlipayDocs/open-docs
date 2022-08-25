
# 简介
**my.getBatteryInfoSync** 是获取电量的同步接口。无需传入参，同步获取当前设备的电量和充电状态。

## 使用限制

- 基础库 [1.12.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.38 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码
```javascript
// .js
var res = my.getBatteryInfoSync();
my.alert({content: '系统信息：'+JSON.stringify(res)});
console.log({content: '系统信息：'+JSON.stringify(res),});
```

## 返回值
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| level | Int | 当前设备电量。 |
| isCharging | Boolean | 当前设备是否充电中。 |

