# 简介
**Canvas.toTempFilePath** 把当前画布指定区域的内容导出生成指定大小的图片。

## 使用限制

- 支付宝客户端 10.2.38 版本，基础库 [2.7.15](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .axml 示例代码
```html
<canvas type="2d" id="canvas" onReady="onCanvasReady"></canvas>
```

### .js 示例代码
```javascript
Page({
  onCanvasReady() {
    const query = my.createSelectorQuery();
    query.select('#canvas').node().exec((res) => {
      const canvas = res[0].node;
      const ctx = canvas.getContext('2d');
      const img = canvas.createImage();
      img.src = "https://img.alicdn.com/tfs/TB1GvVMj2BNTKJjy0FdXXcPpVXa-520-280.jpg";
      img.onload = () => {
        ctx.drawImage(img, 10, 10, 100, 100);
        canvas.toTempFilePath({
          success(res) {
            console.log(res);
          }
        })
      }
    })
  }
})
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| x | Number | 否 | 指定的画布区域的左上角横坐标。 |
| y | Number | 否 | 指定的画布区域的左上角纵坐标。 |
| width | Number | 否 | 指定的画布区域的宽度。 |
| height | Number | 否 | 指定的画布区域的高度。 |
| destWidth | Number | 否 | 输出的图片的宽度。 |
| destHeight | Number | 否 | 输出的图片的高度。 |
| fileType | String | 否 | 目标文件的类型。<br />可选值：<ul><li>jpg：.jpg 图片。</li><li>png：.png 图片。</li></ul><br />默认值 `png`。 |
| quality | Number | 否 | 图片的质量，目前仅对 `jpg` 有效。取值范围为 `(0, 1]`，不在范围内时当作 `1` 处理。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


### success 返回值
值类型为 Object，其结构如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| tempFilePath | String | 生成文件的临时路径 (本地路径)。 |
