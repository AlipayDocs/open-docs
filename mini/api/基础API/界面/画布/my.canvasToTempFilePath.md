# 简介

**my.canvasToTempFilePath** 把当前画布指定区域的内容导出生成指定大小的图片。

## 使用限制

- IDE 模拟器暂不支持调试，请以真机调试结果为准。

# 接口调用

## 新版接口

关于新老版本接口的差异和升级方法，请参考 [旧版 Canvas 迁移指南](https://opendocs.alipay.com/mini/055eid)。

### .axml 示例代码

```html
<canvas type="2d" id="canvas" onReady="onCanvasReady" />
```

### .js 示例代码

```javascript
Page({
  onCanvasReady() {
    const query = my.createSelectorQuery();
    query
      .select('#canvas')
      .node()
      .exec(res => {
        const canvas = res[0].node;
        const ctx = canvas.getContext('2d');
        const img = canvas.createImage();
        img.src = 'https://img.alicdn.com/tfs/TB1GvVMj2BNTKJjy0FdXXcPpVXa-520-280.jpg';
        img.onload = () => {
          ctx.drawImage(img, 10, 10, 100, 100);
          my.canvasToTempFilePath({
            canvas,
            success(res) {
              console.log('success', res.apFilePath);
            },
          });
        };
      });
  },
});
```

### 旧版接口

### .axml 示例代码
```html
<canvas id="canvas" />
```

### .js 示例代码

```javascript
Page({
  onReady() {
    const ctx = my.createCanvasContext('canvas');
    const src = 'https://img.alicdn.com/tfs/TB1GvVMj2BNTKJjy0FdXXcPpVXa-520-280.jpg';
    ctx.drawImage(src, 10, 10, 100, 100);
    ctx.draw(false, () => {
      // 请注意此 API 需要在 ctx.draw 的回调中调用
      my.canvasToTempFilePath({
        canvasId: 'canvas',
        success: (res) => {
          console.log('success', res.apFilePath);
        }
      });
    });
  },
});
```

## 入参

Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| canvas | Object | 是。新版接口必填 | 画布对象。 |
| canvasId | String | 是。旧版本接口必填 | 画布标识，canvas 组件的 id。 |
| x | Number | 否 | 指定的画布区域的左上角横坐标。 |
| y | Number | 否 | 指定的画布区域的左上角纵坐标。 |
| width | Number | 否 | 指定的画布区域的宽度。 |
| height | Number | 否 | 指定的画布区域的高度。 |
| destWidth | Number | 否 | 输出的图片的宽度。 |
| destHeight | Number | 否 | 输出的图片的高度。 |
| fileType | String | 否 | 目标文件的类型。可选值：`jpg`、`png`。默认值 `png`。 |
| quality | Number | 否 | 图片的质量，目前仅对 `jpg` 有效。取值范围为 `(0, 1]`，不在范围内时当作 `1` 处理。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### 出参

success 回调函数会收到一个 Object 类型的参数，其属性如下：

| **属性**   | **类型** | **描述**            |
| ------------ | -------- | ------------------------------- |
| apFilePath | String   | 生成的图片文件路径（[本地临时文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6)]。 |
