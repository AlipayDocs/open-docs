
# 简介
**CameraContext.setZoom** 设置缩放级别。

## 使用限制

- 基础库 [2.7.16](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2)、支付宝客户端 10.2.58  或更高版本，若版本较低，建议采取 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。

# 接口调用

## 示例代码

### .axml 示例代码<br />
```html
<camera 
  id="camera"
  device-position="front"
  flash="off"
  style="width: 100%; height: 300px;"
  onReady="onCameraReady"
/>
```

### .js 示例代码
```javascript
Page({
  onCameraReady(e) {
    const { maxZoom } = e.detail; //最大缩放级别
    this.cameraContext = my.createCameraContext('camera');
    this.cameraContext.setZoom({
      zoom: 2,   //缩放级别
    	success(res) {
      	console.log(res.zoom); //实际设置的缩放级别。
      }
    })
  },
})
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| zoom | Number | 是 | 缩放级别，范围 [1, maxZoom]。zoom 可取小数，精确到小数后一位。maxZoom 可在 onReady 返回值中获取。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


### Function success
success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| zoom | Number | 实际设置的缩放级别。由于系统限制，某些机型可能无法设置成指定值，会改用最接近的可设值。 |


