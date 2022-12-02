
## 使用限制
版本要求：基础库 2.6.2 及以上，支付宝 10.2.0 及以上。

## 操作步骤
为了提升性能、优化小程序体验，[Canvas](https://opendocs.alipay.com/mini/component/canvas) 组件会逐步切换为原生 Canvas 组件实现。实际使用中若遇到 iOS 平台上覆盖于 Canvas 组件上的 web 元素（后称：覆盖元素）无法收到 UI 事件时，可以进行如下适配，以确保顺利收到 UI 事件。<br />以下两个步骤缺一不可。

1. 当前小程序 app.json 的 window 节点中配置 enableComponentOverlayer 为 YES，这个配置项用于指示小程序运行时将目标区域内 UI 事件派发给 Canvas 组件。
```json
{   
  "pages":[    
    "pages/index/index"   
  ],  
  "window":{  
    "enableComponentOverlayer":"YES"  
  }  
}
```

2. 为覆盖元素添加 AF-COMPONENT-OVERLAYER class 属性来指示小程序运行时将 UI 事件派发给覆盖元素，而不传递给后边的 Canvas 组件；若不添加 AF-COMPONENT-OVERLAYER class 属性，则会默认派发给 Canvas 组件。<br />**注意**：如果在开发中遇到 Canvas 组件上没有可见的 web 元素覆盖（即：开发视角下无覆盖元素）时也收不到 UI 事件，可以只采用步骤 1 来尝试解决。
```css
/* declare style for top class in acss */
.top {  
  z-index: 2;
}
```
```xml
<!-- axml 中为覆盖元素增加 AF-COMPONENT-OVERLAYER class 属性的样例 -->
<view class="page">  
  <canvas style="width: 100%; height: 500px;">
  </canvas>  
  <!-- 假设下方的View需要盖在 canvas 上（即 z-index 层级要比 canvas 高），那么需要在这个 view 上增加class "AF-COMPONENT-OVERLAYER" 这样-->  
    <view class="top AF-COMPONENT-OVERLAYER" onTap="viewClick"  >    
    </view>
</view>
```

 <br /> 
