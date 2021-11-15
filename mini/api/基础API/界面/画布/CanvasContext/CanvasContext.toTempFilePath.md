> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。


# 简介
**CanvasContext.toTempFilePath** 用于把当前画布的内容导出生成图片，并返回文件路径。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624962222812-82486f2e-f6a8-42d1-b5f8-7870226c27fc.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&name=1.png&originHeight=158&originWidth=128&size=17896&status=done&style=stroke&width=128)

## 效果示例
![|300x540](https://cdn.nlark.com/yuque/0/2021/gif/179989/1624962231975-39be289a-69e4-4f7e-94e3-8913bfb7c322.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&name=2.gif&originHeight=540&originWidth=300&size=1429075&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码
```javascript
//.js
const CanvasContext = my.createCanvasContext('canvas');
CanvasContext.toTempFilePath({
  success(res) {
  //res.apFilePath
  }
})
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| x | Number | 否 | 画布 x 轴起点。默认值为 0。 |
| y | Number | 否 | 画布 y 轴起点。默认值为 0。 |
| width | Number | 否 | 画布宽度。默认为 canvas 宽度 x。 |
| height | Number | 否 | 画布高度。默认为 canvas 高度 y。 |
| destWidth | Number | 否 | 输出的图片宽度。默认为 width。 |
| destHeight | Number | 否 | 输出的图片高度。默认为 height。 |
| fileType | String | 否 | 图片格式，可选值为 jpg 或 png。默认为 png。 |
| quality | Number | 否 | 图片的质量，目前仅对 jpg 有效，取值范围为 (0, 1]，不在范围内时当作 1.0 处理。 |
| success | Function | 否 | 接口成功回调。 |
| fail | Function | 否 | 接口失败回调。 |
| complete | Function | 否 | 接口完成回调。 |


### success 回调函数
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| tempFilePath | String | 客户端内部路径。例如“/sdcard/xxx”，小程序内不识别。 |
| apFilePath | String | http 协议临时路径。例如“http://res/xxx.image”，小程序内可正常使用。 |


### fail 回调函数
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| error | String | 错误信息。 |

