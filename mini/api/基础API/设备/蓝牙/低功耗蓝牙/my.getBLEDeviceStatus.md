# 简介
**my.getBLEDeviceStatus** 是获取设备蓝牙授权和开关状态的 API。

## 使用限制

- 支付宝客户端 10.2.38，基础库 [2.7.11](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。
- 如果是 iOS 系统，需优先处理 authStatus 状态，当 authStatus=3(蓝牙已授权）时，再处理 powerStatus 状态，否则 powerStatus 状态是不准确的。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
my.getBLEDeviceStatus（{
  success: (res) => {
    console.log(res)
  },
  fail: (err) => {
    console.error("getBLEDeviceStatus:"+JSON.stringify(err))
  }
})
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### success 返回值
success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| authStatus | Number | 蓝牙授权状态（仅 iOS） 其中：<br /><ul><li>0：应用从未用过蓝牙（第一次使用时，会有系统弹窗授权提示）。</li><li>2：当前蓝牙授权是被拒绝状态。</li><li>3：蓝牙已被授权。</li></ul><br /> **说明**：建议仅关注 0、2、3 三种错误码，其他错误码可以统一认为蓝牙授权状态无法确定。 |
| powerStatus | Number | 蓝牙开关状态，其中：<ul><li>2：设备不支持。</li><li>4：蓝牙开关为关闭状态。</li><li>5：蓝牙开关为打开状态。</li></ul><br /> **说明**：建议仅关注 2、4、5 三种错误码，其他错误码可以统一认为蓝牙开关状态无法确定. |
