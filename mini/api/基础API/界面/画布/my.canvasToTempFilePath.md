# 简介

**my.canvasToTempFilePath** 把当前画布指定区域的内容导出生成指定大小的图片，需在 `draw()` 回调里调用该方法才能保证图片导出成功。

## 使用限制

- 支付宝客户端 10.2.38 版本，基础库 [2.7.15](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持适配 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 新接口。可通过 `my.canIUse('canvasToTempFilePath.object.canvas')` 进行检测。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- IDE 模拟器暂不支持调试，请以真机调试结果为准。

# 接口调用

## 示例代码

### .axml 示例代码

```html
// canvas 1.0
<canvas id="canvas1" />
// canvas 2.0 // 基础库2.7.15 开始支持传入canvas 参数
<canvas type="2d" id="canvas2" onReady="onCanvasReady" />
```

### .js 示例代码

```javascript
Page({
  onReady() {
    const ctx = my.createCanvasContext('canvas1');
    ctx.drawImage('/image/ant.png', 0, 0);
    ctx.draw(false, () => {
      my.canvasToTempFilePath({
        canvasId: 'canvas1',
        success: res => {
          console.log(res.tempFilePath);
        },
      });
    });
  },
  onCanvasReady() {
    const query = my.createSelectorQuery();
    query
      .select('#canvas2')
      .node()
      .exec(res => {
        const canvas = res[0].node;
        const ctx = canvas.getContext('2d');
        const img = canvas.createImage();
        img.src =
          'https://img.alicdn.com/tfs/TB1GvVMj2BNTKJjy0FdXXcPpVXa-520-280.jpg';
        img.onload = () => {
          ctx.drawImage(img, 10, 10, 100, 100);
          my.canvasToTempFilePath({
            canvas,
            success(res) {
              console.log(res.tempFilePath);
            },
            fail(res) {
              console.log(res);
            },
            complete(res) {
              console.log(res);
            },
          });
        };
      });
  },
});
```

## 入参

Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| canvasId | String | 否 | 画布标识，传入 canvas 组件的 id。 |
| canvas | Object | 否 | 画布标识，传入 canvas 组件实例 （canvas type="2d/webgl" 时使用该属性）。<br />基础库 [2.7.15](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持。可通过 `my.canIUse('canvasToTempFilePath.object.canvas')` 进行检测。 |
| x | Number | 否 | 指定的画布区域的左上角横坐标。 |
| y | Number | 否 | 指定的画布区域的左上角纵坐标。 |
| width | Number | 否 | 指定的画布区域的宽度。 |
| height | Number | 否 | 指定的画布区域的高度。 |
| destWidth | Number | 否 | 输出的图片的宽度。 |
| destHeight | Number | 否 | 输出的图片的高度。 |
| fileType | String | 否 | 目标文件的类型。<br />可选值：<ul><li>jpg：.jpg 图片。</li><li>png：.png 图片。</li></ul><br /> 默认 `png`。 |
| quality | Number | 否 | 图片的质量，目前仅对 `jpg` 有效。取值范围为 `(0, 1]`，不在范围内时当作 `1` 处理。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### success 返回值

值类型为 Object，其结构如下：

| **属性**     | **类型** | **描述**                        |
| ------------ | -------- | ------------------------------- |
| tempFilePath | String   | [本地临时文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6)路径。 |
