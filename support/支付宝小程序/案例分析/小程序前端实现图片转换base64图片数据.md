在小程序开发中往往会遇到图片转 base64 的场景，目前小程序 [my.createCanvasContext](https://opendocs.alipay.com/mini/api/ui-canvas)，提供了 [CanvasContext.toDataURL](https://opendocs.alipay.com/mini/api/vemgc6) 用于获取画布指定区域的 data URL 数据。返回的数据就是 base64 图片数据，可直接使用 [image](https://opendocs.alipay.com/mini/component/image) 组件展示。<br />**注意**：

- 图片转 base64 需要依赖 [canvas](https://opendocs.alipay.com/mini/component/canvas) 组件的能力，如页面不需要展示 canvas 可对其进行隐藏。
- canvas.draw 和 canvas.toDataURL 方法均为延迟方法需要在方法回调中进行进行其它操作。

获取 base64 图片字符串数据代码如下：
```xml
//axml
<view> <canvas
               id="canvas"      
               width="610"     
               height="610"     
               class="canvas"    
               onTouchStart="log"  
               onTouchMove="log"  
               onTouchEnd="log"
    /><image mode="widthFix"  src="{{dataImage}}"/></view>
```
```javascript
//js
data: {
    dataImage:"",},
      onLoad(){
        const ctx = my.createCanvasContext('canvas');  
        ctx.setFillStyle('#108ee9');
        ctx.arc(50, 50, 50, 0, Math.PI * 2, true); 
        ctx.fill();  ctx.draw();  //可通过设置fileType和quality来设置图片的格式和质量 
        ctx.toDataURL({
          x: 50,  
          y: 50,  
          width: 50,
          height: 50,  
          destWidth: 100,   
          destHeight: 100, 
        }).then(dataURL=>{  
          ctx.drawImage(dataURL, 0, 0);  
          console.log("dataURL", dataURL)  
          this.setData({    
            dataImage:dataURL  
          })   
          ctx.draw(); 
        }) 
      }
```
显示效果如下：<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/5c63addd-5e70-4a8b-bf33-3490142dfd91.png#align=left&display=inline&height=604&margin=%5Bobject%20Object%5D&originHeight=604&originWidth=377&status=done&style=none&width=377)<br />开发者实现转换用户的本地相册图片，可通过三个步骤实现：<br />第一步：使用 [my.chooseImage](https://opendocs.alipay.com/mini/api/media/image/my.chooseimage) 拍照或从本地相册中选择图片。<br />第二步：使用 [CanvasContext.drawImage](https://opendocs.alipay.com/mini/api/pzmtqk) 将上一步获取到的图片绘制图像到画布，图像保持原始尺寸。<br />第三步：[CanvasContext.toDataURL](https://opendocs.alipay.com/mini/api/vemgc6) 获取画布指定区域的 data URL 数据。<br />小程序前端 axml 代码：
```xml
<view onTap="tap">点击转换</view>
<canvas id="canvas"></canvas>
<image mode="scaleToFill" src="{{src}}"/>
```
小程序页面 JS 代码：
```javascript
Page({
   data: {  },  
   onLoad() {
     this.ctx = my.createCanvasContext('canvas');  }, 
     tap(e) {
     let ctx = this.ctx 
     let that = this
     my.chooseImage({ /** 调取相册*/
       sourceType: ['camera', 'album'],  
       count: 1,     
       success: (res1) => {        
         console.log('res1', res1.apFilePaths[0])        
         ctx.drawImage(res1.apFilePaths[0], 0, 0);
         ctx.draw(false, () => {          
            ctx.toDataURL({          
            }).then(dataURL => {            
             console.log('dataURL', dataURL)            
             that.setData({
               src: dataURL            
               })
             })        
           })     
         },
      fail: (e) => {        
        console.log('fail----------------------')      
      }   
    }) 
  },
});
```
