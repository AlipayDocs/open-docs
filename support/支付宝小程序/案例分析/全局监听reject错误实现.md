
## 场景说明
在小程序中如何统一处理 request 错误请求信息。

## 在小程序中封装my.request api直接在封装接口中处理
可以在工具类中使用 promise 封装小程序的 my.request API。

### 封装 my.request 方法
```javascript
/*uri: 请求地址  data: 请求数据  category: 请求方式*/
export const action = (uri, data = {},
 category = 'post') => { 
  return new Promise((resolve,reject) => {  
    let base_uri = ''    
    let _opts = {
      method: category,   
      dataType: 'json',   
      data,
    };
    if (!(uri.indexOf('https://') > 0 || uri.indexOf('http://') > 0)) {
      // 默认域名或者测试环境域名
      base_uri = 'http://axx.com/';
    }
    _opts.url = base_uri + uri; 
    if (category.toLowerCase() === 'post') {
      _opts.headers = {}    
      _opts.headers['content-type'] = 'application/x-www-form-urlencoded'
    }
    _opts.success = _opts.complete = (r) => {
      return resolve(r)
    };    
    _opts.fail = (err) => {
      // 全局处理请求的错误信息
      my.showToast({
        icon: 'none',     
        content: '错误'
      });
      return reject(err)
    }
    // 生成信息
    return my.request({..._opts});
  })}
```

### 调用方法
```javascript
// 导入方法
import { action } from '../../utils/action';
Page({
  data: {},
  onLoad() {
    // 调用方法
    action('api/Api/t')     
    .then((res) => {
        console.log(res, 111)
      }) 
  },
});
```

## 全局统一处理错误方式使用全局onUnhandledRejection
封装在接口中的 reject 统一请求虽然能解决大部分问题，但是有时候可能部分的 reject 处理流程希望返回后单独处理，这时候就可以在 app.js 中的 onUnhandledRejection 方法来监听没有定义 reject 的处理器的 promise 错误请求。

## app.js 中的方法
```javascript
App({
  onLaunch(options) { 
    // 第一次打开    // 
    options.query == {number:1} 
    console.info('App onLaunch', options);  
  },  
  onShow(options) {   
    // 从后台被 scheme 重新打开    // 
    options.query == {number:1} 
  }, 
  onUnhandledRejection(e) {   
    // 全局错误信息处理   
    my.showToast({  
      icon: 'none',   
      content: '错误信息'  
    }); 
  }});
```

### 封装my.request请求
```javascript
/*uri: 请求地址  data: 请求数据  category: 请求方式*/
export const action = (uri, data = {}, category = 'post') => {
  return new Promise((resolve,reject) => {  
    let base_uri = ''    
  let _opts = {     
    method: category, 
    dataType: 'json',   
    data,   
  };  
    if (!(uri.indexOf('https://') > 0 || uri.indexOf('http://') > 0)) {  
      // 默认域名或者测试环境域名   
      base_uri = 'http://axx.com/';   
    }    
    _opts.url = base_uri + uri;   
    if (category.toLowerCase() === 'post') {  
      _opts.headers = {}   
      _opts.headers['content-type'] = 'application/x-www-form-urlencoded' 
    }   
    _opts.success = _opts.complete = (r) => {  
      return resolve(r) 
    };   
    _opts.fail = (err) => { 
      return reject(err)  
    }  
    // 生成信息    
    return my.request({..._opts});
  })}
```

### 调用方法
```javascript
// 导入方法
import { action } from '../../utils/action';
Page({ 
  data: {}, 
  onLoad() {  
    // 调用方法, 调用方法如果不使用.catch监听就会在全局捕捉到错误   
    action('api/Api/t') 
      .then((res) => {      
      console.log(res, 111)   
    })      
    // 调用方法, 调用方法使用.catch监听就不会在全局监听到reject错误信息    
    action('api/Api/t')  
      .then((res) => {     
      console.log(res, 111)  
    }).catch((err) => {     
      // 特别处理的错误      
      my.showToast({  
        icon: 'none',  
        content: '特殊处理'   
      });    
    }) 
  },
});
```

## 全局统一处理错误方式使用全局onUnhandledRejection
封装在接口中的 reject 统一请求虽然能解决大部分问题，但是有时候可能部分的 reject 处理流程希望返回后单独处理，有希望能够通知对应的监听事件的开启这时候就可以在 app.js 中的 onUnhandledRejection 方法来监听没有定义 reject 的处理器的 promise 错误请求。

### app.js中的方法
```javascript
App({ 
  onLaunch(options) {   
    // 第一次打开    // 
    options.query == {number:1}  
    console.info('App onLaunch', options); 
  },
  onShow(options) { 
    // 从后台被 scheme 重新打开    // 
    options.query == {number:1} 
  },  
  onUnhandledRejection(e) {  
    // 全局错误信息处理    
    my.showToast({    
      icon: 'none',    
      content: '错误信息'  
    });  
  }});
```

### 封装my.request请求
```javascript
/*uri: 请求地址  data: 请求数据  category: 请求方式*/
export const action = (uri, data = {}, 
 category = 'post') => {  
  return new Promise((resolve,reject) => {  
    let base_uri = ''    
    let _opts = {   
      method: category,   
      dataType: 'json',    
      data,   
    };  
    if (!(uri.indexOf('https://') > 0 || uri.indexOf('http://') > 0)) {   
      // 默认域名或者测试环境域名    
      base_uri = 'http://axx.com/';   
    }   
    _opts.url = base_uri + uri;   
    if (category.toLowerCase() === 'post') {     
      _opts.headers = {}    
      _opts.headers['content-type'] = 'application/x-www-form-urlencoded'   
    }  
    _opts.success = _opts.complete = (r) => {  
      return resolve(r)  
    };   
    _opts.fail = (err) => {  
      return reject(err)  
    }   
    // 生成信息  
    return my.request({..._opts}); 
  })}
```

### amxl部分代码
```html
<button type="primary" onTap="startReject"> 开启全局监听reject错误</button>
<button type="primary" onTap="endReject"> 关闭全局监听reject错误</button>
```

### 调用方法
```javascript
// 导入方法import { action } from '../../utils/action';
Page({  
  data: {}, 
  onLoad() {    
    // 调用方法, 调用方法如果不使用.catch监听就会在全局捕捉到错误    
    action('api/Api/t')  
      .then((res) => {      
      console.log(res, 111)  
    })     
    // 调用方法, 调用方法使用.catch监听就不会在全局监听到reject错误信息    
    action('api/Api/t')   
      .then((res) => {     
      console.log(res, 111)   
    }).catch((err) => {     
      // 特别处理的错误 
      my.showToast({     
        icon: 'none', 
        content: '特殊处理' 
      });   
    }) 
  }, 
  // 开启监听 
  startReject() { 
    my.onUnhandledRejection((res) => {    
      console.log(res.reason);    
      console.log(res.promise);   
    });
  },  
  // 关闭监听  
  endReject() {    
    const handleRejection = (res) => {   
      console.log(res.reason);  
      console.log(res.promise); 
    }    
    my.offUnhandledRejection(handleRejection); 
  }});    
```

