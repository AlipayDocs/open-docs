
## 说明
- @antv/f2 引入用于网页绘制，里面有用到 window 等，@antv/f2 不适于小程序。
- F2 针对小程序引入做了单独的自定义组件封装可以 @antv/my-f2 安装并引用。（小程序的自定义组件，故需要支付宝小程序基础库支持自定义组件（小程序基础库版本 **1.7.0** 或以上））。
- F2 的支付宝小程序版本，支持原生 F2 的所有功能，F2 API 可查看 [https://f2.antv.vision/zh/docs/api/f2](https://f2.antv.vision/zh/docs/api/f2)。  

## 安装依赖

### npm 安装
```
npm install @antv/my-f2 --save
```
具体可浏览器访问 GitHub 官网：[https://github.com](https://github.com) 搜索：antvis/my-f2 >选择 F2 的支付宝小程序版本。

### 开发工具中安装
打开 [NPM依赖管理](https://opendocs.alipay.com/mini/ide/npm-manage) 输入 @antv/my-f2 回车运行安装。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/d7e6dc56-2467-4c57-b8bd-0fc3674e38b9.png#align=left&display=inline&height=253&margin=%5Bobject%20Object%5D&originHeight=253&originWidth=302&status=done&style=none&width=302)

### 自定义组件方式

#### JSON 文件引入组件
```json
{  
  "usingComponents": { 
    "f2": "@antv/my-f2"  
  }}
```

#### AXML 使用组件
```xml
<view class="container"> 
  <f2 class="f2-chart" onInit="onInitChart"></f2>
</view>
```

#### ACSS 设置宽高
```css
.f2-chart { 
  width: 100%;
  height: 500rpx;
}
```

#### 实例化图表
```javascript
Page({ 
  data: {}, 
  onInitChart(F2, config) { 
    const chart = new F2.Chart(config);
    const data = [    
      { value: 63.4, city: 'New York', date: '2011-10-01' },    
      { value: 62.7, city: 'Alaska', date: '2011-10-01' },   
      { value: 72.2, city: 'Austin', date: '2011-10-01' },   
      { value: 58, city: 'New York', date: '2011-10-02' },     
      { value: 59.9, city: 'Alaska', date: '2011-10-02' },     
      { value: 67.7, city: 'Austin', date: '2011-10-02' },    
      { value: 53.3, city: 'New York', date: '2011-10-03' },  
      { value: 59.1, city: 'Alaska', date: '2011-10-03' },  
      { value: 69.4, city: 'Austin', date: '2011-10-03' },   
    ]; 
    chart.source(data, {   
      date: {     
        range: [0, 1],   
        type: 'timeCat',      
        mask: 'MM-DD'   
      },    
      value: {  
        max: 300,    
        tickCount: 4   
      } 
    });    
    chart.area().position('date*value').color('city').adjust('stack');  
    chart.line().position('date*value').color('city').adjust('stack');  
    chart.render();   // 注意：需要把chart return 出来   
    return chart; 
  }});
```
具体使用可安装完成 @antv/my-f2 后打开 node_modules 查看对应 README.md。

### 效果图
![](https://gw.alipayobjects.com/zos/sptworksff_prod/41210820-0b81-4d22-a0e7-19f2bfcb5b7f.png#align=left&display=inline&height=490&margin=%5Bobject%20Object%5D&originHeight=490&originWidth=371&status=done&style=none&width=371)<br /> <br /> 
