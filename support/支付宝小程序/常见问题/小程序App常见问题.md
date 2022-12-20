# 跳转/启动参数
[小程序跳转能力](https://opendocs.alipay.com/support/01rb03)<br />
[小程序scheme链接介绍](https://opendocs.alipay.com/support/01rb18)<br />
[三方APP/浏览器如何跳转小程序](https://opendocs.alipay.com/support/01rb6e)

### 小程序链接怎么查看
小程序链接查看可参考[scheme链接介绍](https://opendocs.alipay.com/support/01rb18)。<br />
示例链接：`alipays://platformapi/startapp?appId=xxx`，xxx 为小程序的 APPID。

### 小程序scheme链接转成短链接

1. 先将 scheme 链接拼接在 `https://render.alipay.com/p/s/i/?scheme=` 中，拼接示例：`https://render.alipay.com/p/s/i/?scheme=alipays://platformapi/startapp?appId=` 填写实际 APPID。
2. 使用网络上在线工具拼接好的链接转换成短链接。

### 短信中如何跳转小程序
短信中可以使用超链接的方式跳转小程序具体拼接方式如下：<br />`https://render.alipay.com/p/s/i/?scheme=+` encode 后的小程序 scheme。<br />
例如小程序 scheme 链接为 `scheme=alipays://platformapi/startapp?appId=377587690000`。<br />
encode 后与上面链接进行拼接，最后链接为：`https://render.alipay.com/p/s/i/?scheme=scheme%3dalipays%3a%2f%2fplatformapi%2fstartapp%3fappId%3d377587690000`。

### H5传多个值到支付宝小程序
外部 APP/浏览器唤起小程序，需要通过 scheme 调用，在 scheme 中可以传参和设置跳转的首页参数，参考 [小程序scheme链接介绍](https://opendocs.alipay.com/support/01rb18?ant_source=zsearch)。 

# 注册/规则
[小程序各端支持介绍](https://opendocs.alipay.com/support/01rb1m)<br />[小程序依赖安装/引用](https://opendocs.alipay.com/support/01rb23)<br />[全局变量更新介绍](https://opendocs.alipay.com/support/01rb2b)<br />[调试跳转未上线小程序版本（开发版/体验版）](https://opendocs.alipay.com/support/01rb0j)<br />[小程序上架新旧版本更新规则](https://opendocs.alipay.com/support/01rb0k)<br />[支付宝小程序添加到支付宝首页应用列表](https://opensupport.alipay.com/support/knowledge/31868/201602515845)

### 小程序保活时间
小程序（Android/iOS）正常后台保活时长为5分钟（若用户手机运存紧张可能达不到5分钟）。小程序不可以延长后台保活时间。正常的页面关闭的时候是会把当前的页面全部销毁，然后二次打开的时候在重新创建。但是很多场景下，二次打开其实并不需要打开新的页面，或者就算打开新的页面，由于小程序有后台的 work 统一管理多个页面，所有也不需要重新在 Native 层面重启 App。所以小程序做了保活，在退出的时候不会把页面销毁，达到了二次秒开的效果。 

### 能否在 app.js 中关闭小程序
不可以，只能点击右上角的关闭按钮。 

### app.js 中怎么声明全局方法
[App](https://opendocs.alipay.com/mini/framework/app-detail)() 用于注册小程序，接受一个 Object 作为属性，用来配置小程序的生命周期等。App() 必须在 app.js 中调用，必须调用且只能调用一次。<br />和设置globalData全局数据类似，声明全局方法也是需要放在 App() 中，通过 [getApp](https://opendocs.alipay.com/mini/framework/get-app)() 在子页面中获取并调用全局方法。<br />声明示例：
```javascript
// app.js
App({
  //定义全局方法，在整个App中有效
  appFunction(){
     my.alert({
         content:"这是一个App function"
     })}
 });
```
调用示例：
```javascript
//page.js
var app = getApp();
app.appFunction();//调用appFunction()
```

### 启动体验版小程序时指定打开页面
小程序启动无法指定页面，但是通过 [小程序跳转](https://opendocs.alipay.com/mini/api/yz6gnx) 或者 [scheme链接](https://opendocs.alipay.com/support/01rb18?ant_source=zsearch) 唤起小程序可以实现打开小程序并指定打开的页面。<br />**注意：**体验版打开需要参考 [调试跳转未上线小程序版本（开发版/体验版）](https://opendocs.alipay.com/support/01rb0j?ant_source=zsearch)文档提前设置。 

### 可以控制小程序在最近使用中的是否显示吗
最近使用的小程序列表显示与隐藏无法进行控制的，没有相关的API。 

# 报错/异常
[Cannot read property 'setData' of undefined](https://opendocs.alipay.com/support/01rb61) 

### 小程序启动报错EACCES
问题描述：小程序启动报错Error: EACCES: permission denied, mkdir /Users/xiaoqiang/Tuhu/Gitlab/Ali_ App/Ali_App/dist/.tea。<br />
解决方案：权限问题，用超级用户来执行。在npm install 指令前加 sudo 变为： sudo npm install。 

### 暂未找到此功能，请稍后重试
报错描述：<br />
进入小程序提示“暂未找到此功能，请稍后重试”。<br />
报错原因：<br />
因该小程序没有已上架版本，导致无法进入目标小程序页面。<br />
解决方案：<br />
通过IDE提交小程序版本后，在开发者中心后台上架小程序版本。 

### 导航栏设置透明后iOS和Android标题颜色不一致
检查是否设置了 titleBarColor 属性，如果设置了导航栏透明后再设置 titleBarColor 会导致 iOS 和 Android 标题颜色不一致。 

### 小程序退出后重新进入小程序状态还是退出前的状态
小程序退出后重新进入小程序状态还是退出前的状态，属于正常情况，小程序后台理论上存活5分钟，但用户手机当前运存不够情况下不到5分钟。 
