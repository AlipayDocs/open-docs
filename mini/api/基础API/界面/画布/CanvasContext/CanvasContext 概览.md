> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。

### 属性

**string fillStyle**

填充颜色。用法同 [CanvasContext.setFillStyle()](https://opendocs.alipay.com/mini/api/vyfyp2)。

**string strokeStyle**

边框颜色。用法同 [CanvasContext.setStrokeStyle()](https://opendocs.alipay.com/mini/api/lqmreg)。

**number lineWidth**

线条的宽度。用法同 [CanvasContext.setLineWidth()](https://opendocs.alipay.com/mini/api/ugcrcq)。

**string lineCap**

线条的端点样式。用法同 [CanvasContext.setLineCap()](https://opendocs.alipay.com/mini/api/de22sq)。

**string lineJoin**

线条的交点样式。用法同 [CanvasContext.setLineJoin()](https://opendocs.alipay.com/mini/api/sfqcgi)。

**number miterLimit**

最大斜接长度。用法同 [CanvasContext.setMiterLimit()](https://opendocs.alipay.com/mini/api/vul12s)。

**number lineDashOffset**

虚线偏移量，初始值为 0。

**string textBaseline**

当前文本的文本基线。用法同 [CanvasContext.setTextBaseline()](https://opendocs.alipay.com/mini/api/wo3gqy)。

**string font**

当前字体样式的属性。符合 [CSS font 语法](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font) 的 DOMString 字符串，至少需要提供字体大小和字体族名。默认值为 "10px Arial"。

**string textAlign**

文本的对齐方式。用法同 [CanvasContext.setTextAlign()](https://opendocs.alipay.com/mini/api/rf1uma)。

**number fontSize**

字体大小。用法同 [CanvasContext.setFontSize()](https://opendocs.alipay.com/mini/api/mg4uir)。

**number globalAlpha**

全局画笔透明度。范围 0-1，0 表示完全透明，1 表示完全不透明。用法同 [CanvasContext.setGlobalAlpha()](https://opendocs.alipay.com/mini/api/cptvsl)。

**string globalCompositeOperation**

在绘制新形状时应用的合成操作的类型。

### 方法

| **名称** | **描述** |
| --- | --- |
| [CanvasContext.arc](https://opendocs.alipay.com/mini/api/lut4uo) | 画一条弧线。 |
| [CanvasContext.arcTo](https://opendocs.alipay.com/mini/api/arcto) | 根据控制点和半径绘制圆弧路径。 |
| [CanvasContext.beginPath](https://opendocs.alipay.com/mini/api/vk0ohr) | 开始创建一个路径，需要调用 `fill` 或者 `stroke` 才会使用路径进行填充或描边。 |
| [CanvasContext.bezierCurveTo](https://opendocs.alipay.com/mini/api/dzf516) | 创建三次方贝塞尔曲线路径。 |
| [CanvasContext.clearRect](https://opendocs.alipay.com/mini/api/xg3h06) | 清除画布上在该矩形区域内的内容。 |
| [CanvasContext.clip](https://opendocs.alipay.com/mini/api/rgl453) | 将当前创建的路径设置为当前剪切路径。 |
| [CanvasContext.closePath](https://opendocs.alipay.com/mini/api/fg8c9b) | 关闭一个路径。 |
| [CanvasContext.createCircularGradient](https://opendocs.alipay.com/mini/api/ix6opq) | 创建一个圆形的渐变色。起点在圆心，终点在圆环。 |
| [CanvasContext.createLinearGradient](https://opendocs.alipay.com/mini/api/qgb1mf) | 创建一个线性的渐变色。 |
| [CanvasContext.createRadialGradient](https://opendocs.alipay.com/mini/api/radialgradient) | 创建一个放射性的渐变色。 |
| [CanvasContext.createPattern](https://opendocs.alipay.com/mini/api/pattern) | 对指定的图像创建模式的方法，可在指定的方向上重复元图像。 |
| [CanvasContext.draw](https://opendocs.alipay.com/mini/api/he6iwx) | 将之前在绘图上下文中的描述（路径、变形、样式）画到 canvas 中。 |
| [CanvasContext.drawImage](https://opendocs.alipay.com/mini/api/pzmtqk) | 绘制图像，图像保持原始尺寸。 |
| [CanvasContext.fill](https://opendocs.alipay.com/mini/api/yywmib) | 对当前路径中的内容进行填充。 |
| [CanvasContext.fillRect](https://opendocs.alipay.com/mini/api/vfpyra) | 填充矩形。 |
| [CanvasContext.fillText](https://opendocs.alipay.com/mini/api/saf43s) | 在画布上绘制被填充的文本。 |
| [CanvasContext.getImageData](https://opendocs.alipay.com/mini/api/bukvhw) | 获取 canvas 区域隐含的像素数据。 |
| [CanvasContext.lineTo](https://opendocs.alipay.com/mini/api/zkno7s) | 增加一个新点，然后创建一条从上次指定点到目标点的线。 |
| [CanvasContext.measureText](https://opendocs.alipay.com/mini/api/rn2r7f) | 测量文本尺寸信息，目前仅返回文本宽度。同步接口。 |
| [CanvasContext.moveTo](https://opendocs.alipay.com/mini/api/avy1f9) | 把路径移动到画布中的指定点，不创建线条。 |
| [CanvasContext.putImageData](https://opendocs.alipay.com/mini/api/pusaxg) | 将像素数据绘制到画布。 |
| [CanvasContext.quadraticCurveTo](https://opendocs.alipay.com/mini/api/rq2yds) | 创建二次贝塞尔曲线路径。 |
| [CanvasContext.rect](https://opendocs.alipay.com/mini/api/xgywt5) | 创建二次贝塞尔曲线路径。 |
| [CanvasContext.restore](https://opendocs.alipay.com/mini/api/gwoqt0) | 恢复之前保存的绘图上下文。 |
| [CanvasContext.rotate](https://opendocs.alipay.com/mini/api/ncimzx) | 以原点为中心，原点可以用 [translate](https://opendocs.alipay.com/mini/api/ui-canvas#translate) 方法修改。顺时针旋转当前坐标轴。多次调用 `rotate`，旋转的角度会叠加。 |
| [CanvasContext.save](https://opendocs.alipay.com/mini/api/qnyf7h) | 保存当前的绘图上下文。 |
| [CanvasContext.scale](https://opendocs.alipay.com/mini/api/gp3kpy) | 在调用 `scale` 方法后，之后创建的路径其横纵坐标会被缩放。多次调用 `scale`，倍数会相乘。 |
| [CanvasContext.setFillStyle](https://opendocs.alipay.com/mini/api/vyfyp2) | 设置填充色。 |
| [CanvasContext.setFontSize](https://opendocs.alipay.com/mini/api/mg4uir) | 设置字体大小。 |
| [CanvasContext.setGlobalAlpha](https://opendocs.alipay.com/mini/api/cptvsl) | 设置全局画笔透明度。 |
| [CanvasContext.setLineCap](https://opendocs.alipay.com/mini/api/de22sq) | 设置线条的端点样式。 |
| [CanvasContext.setLineDash](https://opendocs.alipay.com/mini/api/cvqcwt) | 设置虚线的样式。 |
| [CanvasContext.setLineJoin](https://opendocs.alipay.com/mini/api/sfqcgi) | 设置线条的交点样式。 |
| [CanvasContext.setLineWidth](https://opendocs.alipay.com/mini/api/ugcrcq) | 设置线条的宽度。 |
| [CanvasContext.setMiterLimit](https://opendocs.alipay.com/mini/api/vul12s) | 设置最大斜接长度。 |
| [CanvasContext.setShadow](https://opendocs.alipay.com/mini/api/btvtra) | 设置阴影样式。 |
| [CanvasContext.setStrokeStyle](https://opendocs.alipay.com/mini/api/lqmreg) | 设置边框颜色。 |
| [CanvasContext.setTextAlign](https://opendocs.alipay.com/mini/api/rf1uma) | Canvas 2D API 描述绘制文本时，文本的对齐方式的属性。 |
| [CanvasContext.setTextBaseline](https://opendocs.alipay.com/mini/api/wo3gqy) | Canvas 2D API 描述绘制文本时，当前文本基线的属性。 |
| [CanvasContext.setTransform](https://opendocs.alipay.com/mini/api/wt6glg) | 使用单位矩阵重新设置（覆盖）当前的变换并调用变换的方法，此变换由方法的变量进行描述。 |
| [CanvasContext.stroke](https://opendocs.alipay.com/mini/api/pgahxv) | 画出当前路径的边框。默认 `black`。 |
| [CanvasContext.strokeRect](https://opendocs.alipay.com/mini/api/vz04q8) | 画一个矩形（非填充）。 |
| [CanvasContext.strokeText](https://opendocs.alipay.com/mini/api/stroketext) | 给定的 (x, y) 位置绘制文本描边的方法。 |
| [CanvasContext.toDataURL](https://opendocs.alipay.com/mini/api/vemgc6) | 获取画布指定区域的 data URL 数据。 |
| [CanvasContext.toTempFilePath](https://opendocs.alipay.com/mini/api/rod3ti) | 把当前画布的内容导出生成图片，并返回文件路径。 |
| [CanvasContext.transform](https://opendocs.alipay.com/mini/api/fv97do) | 使用矩阵多次叠加当前变换的方法，矩阵由方法的参数进行描述。可以缩放、旋转、移动和倾斜上下文。 |
| [CanvasContext.translate](https://opendocs.alipay.com/mini/api/lgqkb2) | 对当前坐标系的原点(0, 0)进行变换，默认的坐标系原点为页面左上角。 |
