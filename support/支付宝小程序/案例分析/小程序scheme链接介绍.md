支付宝小程序不限制来自 H5 页面或者其它 App 的跳转，只要 H5 页面或者其它 App 支持外跳小程序即可跳转，本文介绍通过 scheme 链接方式实现跳转。<br />如需跳转到未上线/体验版小程序，可查看 [联调设置](https://opendocs.alipay.com/mini/ide/integration-testing)。

# 拼接方式 

## URL 格式
```
alipays://platformapi/startapp?appId=[appId]&page=[page]&query=[query]
```
| **参数** | **描述** | **示例** |
| --- | --- | --- |
| appId | 要跳转的目标小程序 APPID。 | 20170713077xxxxx |
| page | 要跳转到目标小程序的具体 page 页面，该值等于 app.json 里面的配置值；如果不带 page 字段，默认跳转到小程序首页。<br />路径中可以在 ？后面附加跳转后的页面参数。页面参数必须进行 UrlEncode 编码，否则只能获取到第一个页面参数。| UrlEncode 编码前：pages/index/index?key1=1&key2=2 <br />UrlEncode 编码后：pages/index/index?key1%3D1%26key2%3D2 |
| query | 表示从外部 App 携带的参数透传到目标小程序，如果不需要携带参数给小程序，可以不带该参数。<br />query：启动参数，内容按照格式为参数名=参数值&参数名=参数值<br />**注意：** query 携带的启动参数必须进行 UrlEncode 编码否则只能获取到第一个参数。 | UrlEncode 编码前：key1=value1&key2=value2<br /> UrlEncode 编码后：key1%3Dvalue1%26key2%3Dvalue2 |


## scheme转换成https链接唤起小程序
需要把 scheme 当作参数进行 **UrlEncode** 编码后，拼接在 `https://ds.alipay.com/?scheme=` 后。<br />
### 拼接过程
第一步、填写贵司正确的应用appId和page页面路径，完成如下：<br />`alipays://platformapi/startapp?appId=202100216xxxxxxx&page=pages/index/index`<br />
携带启动参数场景，先单独对 query 携带的启动参数进行 **UrlEncode** 编码，完成如下：<br />
**UrlEncode** 编码前：<br />
`alipays://platformapi/startapp?appId=202100216xxxxxxx&page=pages/index/index&query=`**`key1=value1&key2=value2`**<br />
**UrlEncode** 编码后：<br />
`alipays://platformapi/startapp?appId=202100216xxxxxxx&page=pages/index/index&query=`**`key1%3Dvalue1%26key2%3Dvalue2`**<br />
第二步、对 **第一步** 拼接完成的链接进行整体 **UrlEncode** 编码并拼接在 https://ds.alipay.com/?scheme= 后（携带启动参数场景），完成完整拼接如下：<br />
`https://ds.alipay.com/?scheme=alipays%3A%2F%2Fplatformapi%2Fstartapp%3FappId%3D202100216xxxxxxx%26page%3Dpages%2Findex%2Findex%26query%3Dkey1%253Dvalue1%2526key2%253Dvalue2`<br />
**以下是 JS 方式进行拼接示例：**

使用 encodeURIComponent 函数先对query携带的启动参数进行 **UrlEncode** 编码，再使用 encodeURIComponent 对整体 scheme 链接进行 **UrlEncode** 编码。
```html
<script>
window.location.href=`https://ds.alipay.com/?scheme=` 
                    + encodeURIComponent(`alipays://platformapi/startapp?appId=202100216xxxxxxx&page=pages/index/index&query=${encodeURIComponent('key1=value1&key2=value2')}`) 
</script>
```
接下来看一下，scheme 调用小程序之后，应用和页面的处理逻辑。在叙述之前，先了解下前后台的定义。

## 前台/后台运行

- **前台运行：** 当用户首次打开小程序时候，小程序会处于前台运行状态。
- **后台运行：** 用户点击右上角关闭按钮关闭小程序，或者按下设备 Home 键离开支付宝客户端时，小程序并不会直接销毁，而是进入后台运行状态。只有当小程序进入后台一定时间，或者系统资源占用过高，才会被真正的销毁。
- **从后台运行切换为前台运行**： 当未被系统销毁的小程序再度被打开或者激活时，会从后台运行切换为前台运行。 

## 应用逻辑
每次通过 scheme 调用，前端表现是重新触发 onLaunch 和 onShow，都会传参给 app.js 的 onLaunch 和 onShow，基础页面会重新触发 onLoad 和 onShow 方法。<br />在**保活期间（5分钟）**，例如锁屏之后，会重新触发 onShow 方法，但是却无法获取参数，即传参 scheme 只会在调用的时候触发一次，再次启动只是触发 onShow 不会传参。只能前端在 onShow 里做相应的业务逻辑。 

## 页面的逻辑
当小程序用 scheme 从后台唤起的时候，其实相当于重新被打开了onLoad，还有 onShow 都会被触发。<br />在保活期间（5分钟）被重新唤起的时候，就只会触发 onShow 。 

# 小程序通过 scheme 跳转如何获取启动参数
参考[如何在小程序启动后获取启动参数](https://opendocs.alipay.com/support/01rb2a)。 

# 小程序 scheme 链接应用
商家可以通过 H5/Android/iOS 应用使用 scheme 链接来跳转到支付宝小程序。

### H5 跳转小程序 
```javascript
window.location.href="alipays://platformapi/startapp?appId=20170713077xxxxx&page=x/yz&query=xx%3dxx";
```

###  Android App 跳转小程序
```javascript
Intent intent=new Intent(Intent.ACTION_VIEW,Uri.parse("alipays://platformapi/startapp?appId=20170713077xxxxx&page=x/yz&query=xx%3dxx"));startActivity(intent);
```

### iOS App 跳转小程序
```javascript
let urlString = "alipays://platformapi/startapp?appId=20170713077xxxxx&page=x/yz&query=xx%3dxx"
       let url = URL(string: urlString)
       if UIApplication.shared.canOpenURL(url!) {
             UIApplication.shared.open(url!)
      }else{
             let appString = "https://www.apple.com/itunes/"             
             let appUrl = URL(string: appString)
             UIApplication.shared.open(appUrl!)
        }
```

