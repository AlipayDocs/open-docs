## 全局参数和页面参数的区别
- 拼接方式不同，全局参数是在 scheme 地址的 query 中拼接，详情可查看 [小程序scheme链接介绍](https://opendocs.alipay.com/support/01rb18)；页面参数是在 [路由API](https://opendocs.alipay.com/mini/api/zwi8gx) 的 URL 后拼接，如：path?key1=value1&key2=value2。
- 获取参数不同，全局参数在 app.js 的 onLaunch 中获取，页面参数在对应页面 Page.onLoad 中取得。
- 运行返回时机不同，全局参数在小程序启动初始化时就返回；页面参数需要打开对应页面才会返回。 

## 开发工具启动参数配置
开发工具 IDE 首次使用默认为普通编译模式，即默认刷新模拟器会打开首页，并且没有传入任何参数。可以添加自定义的编译模式，让模拟器刷新时从其它页面启动，并带上相关参数，提升调试效率。<br />打开 IDE 顶部功能区中的 **普通编译模式** 添加编译模式，选择 **添加编译模式**。

- **模式名称：**自定义填写名称不影响测试。
- **启动页面：**下拉选择需要测试的页面。
- **页面参数：**填写需要获取的页面启动参数，在对应页面 page.js 中 onLoad 获取；例如：pageKey=abc123。
- **全局参数：** 填写需要获取的全局启动参数，在 app.js 中 onLaunch/onShow 获取；例如：appKey=abc123。 

**注意：**新增编译模式生成的真机预览二维码可在开发版中进行测试启动参数。<br />![](https://gw.alipayobjects.com/zos/sptworksff_prod/227c0cdf-6b80-4fc9-8d60-70bc4de6fd9b.png#align=left&display=inline&height=414&margin=%5Bobject%20Object%5D&originHeight=414&originWidth=587&status=done&style=none&width=587)

## 开发工具启动参数获取

### 全局参数获取示例
```javascript
//app.js中获取全局参数
onLaunch(options) {
   my.alert({
     content:JSON.stringify(options.query.appKey)
   })   
   console.log(JSON.stringify(options)) }, 
   onShow(options) {
   my.alert({    
    content:JSON.stringify(options.query.appKey)  
    })  
   console.log(JSON.stringify(options)) 
 },
```

### 页面参数获取示例
```javascript
//对应页面page.js中获取页面参数
onLoad(query) {   
  my.alert({ 
    content:JSON.stringify(query.pageKey)
  })  
  console.log(JSON.stringify(query)) 
},
```
 <br /> 
