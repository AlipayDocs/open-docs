如果需要在高 DPR（devicePixelRatio）下取得更细腻的显示，需要先将 canvas 用属性设置放大，用样式缩小，例如：
```
<!-- getSystemInfoSync().pixelRatio === 2 -->
<canvas width="200" height="200" style="width:100px;height:100px;"/>
```

# 常见问题 

### 原生 Canvas 组件适配
参考 [原生 Canvas 组件适配](https://opendocs.alipay.com/support/01rb26)。 

### 小程序中如何进行手写签名
参考 [小程序中如何进行手写签名](https://opendocs.alipay.com/support/01rb1b)。 

### 如何解决画布模糊问题
参考 [如何解决画布模糊问题](https://opendocs.alipay.com/support/01rb86)。 

### 小程序前端实现图片转换base64图片数据
参考 [小程序前端实现图片转换base64图片数据](https://opendocs.alipay.com/support/01rb15)。 

### 小程序canvas生成图片保存
可以使用 [CanvasContext.toTempFilePath](https://opendocs.alipay.com/mini/api/rod3ti) 把当前画布的内容导出生成图片，并返回文件路径。<br />**注：**返回的文件路径是临时路径，所以还需要通过 [my.saveImage](https://opendocs.alipay.com/mini/api/media/image/my.saveimage) 保存图片到相册。 

### canvas画布不显示

- 创建画布的方法 my.createCanvasContext('canvasid') 没有放到 onReady 方法中。
- createCanvasContext 方法中的 id 与 amxl 文件中的 canvas 的 id 不一致。 

### 多次调用canvas.draw()之前的画布内容未清除
执行方法之前保存状态，参数设置好之后恢复状态再画，具体可以参考 [CanvasContext.draw](https://opendocs.alipay.com/mini/api/he6iwx)。 

### 小程序是否支持Echart
小程序由于兼容问题目前不支持直接使用 echarts，如需要使用可使用 [antv-f2](https://antv.vision/zh) 的 F2 支付宝小程序 my-f2（**推荐**）。<br />**说明：**F2 的支付宝小程序版本，支持原生 F2 的所有功能，F2 API 参见：[https://f2.antv.vision/zh/docs/api/f2](https://f2.antv.vision/zh/docs/api/f2)<br />**npm安装：**<br />npm install @antv/my-f2 --save<br />**开发工具中安装：**<br />打开 [NPM依赖管理](https://opendocs.alipay.com/mini/ide/npm-manage)--输入 @antv/my-f2 回车运行安装。<br />具体使用可安装完成 @antv/my-f2 后打开 node_modules 查看对应 README.md。

### toTempFilePath导出图片空白

- 使用 image 看下图片是否可以正常显示，正常显示才可以导出图片。
- 若使用了 ctx.drawImage，ctx.drawImage 调用后建议等执行完成后再调用 toTempFilePath 进行导出图片，否则会出现 ctx.drawImage 未执行完成就 toTempFilePath 进行导出图片会出现空白的。this.context.toTempFilePath 放到 this.context.draw() 的回调里执行。
```javascript
this.context.drawImage('https://abc.png', 2, 2, 800, 800);this.context.draw(false,() => {this.context.toTempFilePath()});
```

### canvas图片保存到手机
[canvas](https://docs.alipay.com/mini/api/ui-canvas) 把画布生成图片的，可以用 toTempFilePath 生成临时路径，再使用 [my.saveImage](https://opendocs.alipay.com/mini/api/media/image/my.saveimage) 保存到手机相册。<br /> 
