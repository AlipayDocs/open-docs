
# 简介
**my.onGyroscopeChange** 是监听陀螺仪数据变化事件，接口调用后会自动开始监听，回调间隔为 500ms，可使用 [my.offGyroscopeChange()](/mini/api/cpt55i) 停止监听。

## 使用限制

- 基础库 [1.9.0](https://opendocs.alipay.com/mini/framework/lib)  或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// .js
my.onGyroscopeChange((res)=>{
   console.log('gyroData.rotationRate.x = ' + res.x);
   console.log('gyroData.rotationRate.y = ' + res.y);
   console.log('gyroData.rotationRate.z = ' + res.z);
});
```

## 入参
入参为 Function(callback) 类型，callback 回调函数的参数类型为 Object 类型，属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| x | Number | x 轴方向角速度。 |
| y | Number | y 轴方向角速度。 |
| z | Number | z 轴方向角速度。 |

