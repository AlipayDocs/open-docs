
# 场景说明
小程序应用中 tab主页在有新内容或者信息需要提醒用户查看时，如何实现子 tab 按钮上提醒用户，目前小程序提供 [my.setTabBarBadge](https://opendocs.alipay.com/mini/api/qm7t3v)、[my.removeTabBarBadge](https://opendocs.alipay.com/mini/api/lpbp5g)、[my.showTabBarRedDot](https://opendocs.alipay.com/mini/api/dquxiq)、[my.hideTabBarRedDot](https://opendocs.alipay.com/mini/api/mg428a) 用于设置标签页（tabbar）某一项的右上角消息条数的红点提醒实现。 

## 使用限制

- **基础库** [1.11.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；**支付宝客户端** 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- IDE 模拟器 1.13 及以上版本支持该接口调用。 

# tabbar信息红点提示方案
通过 [my.showTabBarRedDot](https://opendocs.alipay.com/mini/api/dquxiq) 和 [my.hideTabBarRedDot](https://opendocs.alipay.com/mini/api/mg428a) 的结合使用，达到给与用户在 tabbar 中的提示及查看后的隐藏效果。 

## tabbar 部分代码
```json
// app.json配置信息
{\t"tabBar": {
    "textColor": "#dddddd",    
    "selectedColor": "#49a9ee",   
    "backgroundColor": "#ffffff",  
    "items": [
       {
         "pagePath": "pages/index/index",    
         "name": "首页"
      },
      {
        "pagePath": "pages/index2/index2", 
        "name": "日志"
      }    
    ] 
  }}
```

## app.js 中的状态部分代码
```javascript
App({
  onLaunch(options) {
    // 第一次打开   
    // options.query == {number:1} 
    console.info('App onLaunch'); 
  }, 
  globalData: {
    isView: false, // 是否查看过 
  },
  onShow(options) { 
    // 从后台被 scheme 重新打开   // 
    options.query == {number:1} 
  },
});
```

## index.js 中部分代码
```javascript
const app = getApp();
Page({  
  checkDot() {
    // 检查是否查看过方法  
    const { isView } = app.globalData;
    // 是否查看   
    if (!isView) {  
      app.globalData.isView = true;
      // 查看是否显示  
      my.showTabBarRedDot({  
        index: 0   
      });   
    }
    else {
      my.hideTabBarRedDot({       
        index: 0   
      });   
    }
  },
  onShow() { 
    // 页面显示   
    this.checkDot(); 
    //
  }, 
  onHide() { 
    // 页面隐藏  
    this.checkDot(); 
    // 
  }});
```

## 显示效果图
![](https://gw.alipayobjects.com/zos/sptworksff_prod/bb159ad5-3bda-4eb0-89ae-509074476e0b.png#align=left&display=inline&height=539&margin=%5Bobject%20Object%5D&originHeight=602&originWidth=371&status=done&style=none&width=332)

# 提示信息并显示信息数量方式
通过 [my.setTabBarBadge](https://opendocs.alipay.com/mini/api/qm7t3v) 和 [my.removeTabBarBadge](https://opendocs.alipay.com/mini/api/lpbp5g) 的结合使用，提示用户信息且显示对应的信息简数。

## 示例代码
```javascript
App({ 
  onLaunch(options) {
    // 第一次打开    // 
    options.query == {number:1}    
  console.info('App onLaunch');
}, 
    globalData: {    
      isView: false, // 是否查看过,   
      infoNum: 42 
    },  
  onShow(options) { 
    // 从后台被 scheme 重新打开  //
    options.query == {number:1}  
  },
});
```

## index.js 信息
```javascript
const app = getApp();
Page({
  checkDot() {
    // 检查是否查看过方法 
    const { isView, infoNum } = app.globalData; // 是否查看   
    if (!isView) {   
      app.globalData.isView = true; // 查看是否显示  
      my.setTabBarBadge({   
        index: 0,       
        text: infoNum // 熟练信息 
      }); 
    } 
    else {  
      my.removeTabBarBadge({  
        index: 0  
      });   
    } 
  }, 
  onShow() { 
    // 页面显示    this.checkDot(); //  
  }, 
  onHide() { 
    // 页面隐藏    this.checkDot(); //  
  }});
```

## 显示效果图
![](https://gw.alipayobjects.com/zos/sptworksff_prod/1d9f11fa-3ccc-42c1-ac19-a7d03a925e1f.png#align=left&display=inline&height=603&margin=%5Bobject%20Object%5D&originHeight=603&originWidth=384&status=done&style=none&width=384)

# 常见问题
[tabbar常见问题](https://opendocs.alipay.com/support/01rb85)<br /> <br /> <br /> 
