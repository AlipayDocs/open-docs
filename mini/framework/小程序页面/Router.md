页面路由器对象，有 switchTab、 reLaunch 、redirectTo、 navigateTo、 navigateBack 五个方法。可以通过 this.pageRouter 或 this.router 获得当前页面或自定义组件的路由器对象。<br />与同名的全局方法 [my.switchTab](https://opendocs.alipay.com/mini/api/ui-tabbar)、[my.reLaunch](https://opendocs.alipay.com/mini/api/hmn54z)、[my.redirectTo](https://opendocs.alipay.com/mini/api/fh18ky)、[my.navigateTo](https://opendocs.alipay.com/mini/api/zwi8gx)、[my.navigateBack](https://opendocs.alipay.com/mini/api/kc5zbx) 功能相同，唯一区别在于页面路由器中的方法调用时，相对路径是相对于 this 指代的页面或自定义组件。通常情况下，更推荐使用 this.pageRouter 和 this.router 进行路由跳转。<br />基础库 [2.7.22](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，若版本较低，建议做 [兼容](https://opendocs.alipay.com/mini/framework/compatibility) 处理。

# 页面的 Router
在页面中调用时，this.pageRouter 和 this.router 获得的是同一个页面路由器对象（即 this.pageRouter === this.router），将相对于 this 指代的页面进行路由跳转。

# 自定义组件的 Router
在自定义组件中调用时，this.router 将相对于 this 指代的自定义组件自身定义时的路径进行路由跳转。<br />this.pageRouter 将相对于 this 指代的自定义组件所在页面的路径进行路由跳转。自定义组件的 this.pageRouter 和自定义组件所在页面的 this.pageRouter  获得的是同一个页面路由器对象。

# 路由的相对路径
| **this** | **this.router** | **this.pageRouter** |
| --- | --- | --- |
| **页面** | 相对于 this 指代的页面的路径 | 相对于 this 指代的页面的路径 |
| **自定义组件** | 相对于 this 指代的自定义组件自身定义时的路径 | 相对于 this 指代的自定义组件所在页面的路径 |


## 使用说明

- 由于插件和宿主的权限管控，由插件（插件自定义组件或插件页面）发起的路由跳转，无论是使用页面路由器对象 Router 上的路由方法还是全局对象 my 上的路由方法，均不支持跳转到宿主小程序页面或另一个插件页面。
- 由于插件和宿主的权限管控，当插件自定义组件被用在宿主小程序或另一个插件中时，该插件自定义组件的 this.pageRouter 为 null。
- 如果在页面 A 通过 redirectTo、reLaunch、navigateBack 方法跳转到页面 B，页面 A 会被销毁，在销毁后的页面 A 调用 this.pageRouter 或 this.router 的路由方法不会生效。

# 示例代码
项目目录结构如下所示。<br />![12.png](https://cdn.nlark.com/yuque/0/2022/png/179989/1658209600139-81520d04-02bd-49a1-8a42-c9dbe2e85ba5.png#align=left&display=inline&height=267&margin=%5Bobject%20Object%5D&name=12.png&originHeight=534&originWidth=256&size=26153&status=done&style=none&width=128)<br />假设当前页面(栈顶页面)路径为 pages2/index/index，分别在页面 page/index/index 和 自定义组件 components/com/com 中调用路由方法 my.navigateTo、this.pageRouter.navigateTo、this.router.navigateTo 进行路由跳转，跳转结果如下：
```javascript
// 自定义组件 components/com/com.json
{
  "component": true
}


// components/com/com.js
Components({
  myNavigateTo(){
    // 相对于栈顶页面的路径 pages2/index/index 进行路由跳转
    // 将会跳转到 pages2/test/test 页面
    my.navigateTo({
      url: '../test/test'
    });
  },
  pageRouterNavigateTo(){
    // 相对于自定义组件所在页面的路径 pages/index/index 进行路由跳转
    // 将会跳转到 pages/test/test 页面
    this.pageRouter.navigateTo({
      url: '../test/test'
    });
  },
  routerNavigateTo(){
    // 相对于 this 指代的自定义组件自身定义时的路径 components/com/com 进行路由跳转
    // 将会跳转到 components/test/test 页面
    this.router.navigateTo({
      url: '../test/test'
    });
  },
})
```
```javascript
// pages/index/index.json
{
  "usingComponents": {
    "com": "../../components/com/com",
  }
}


// pages/index/index.axml
<com />
  

//页面 pages/index/index.js
Page({
  myNavigateTo(){
    // 相对于栈顶页面的路径 pages2/index/index 进行路由跳转
    // 将会跳转到 pages2/test/test 页面
    my.navigateTo({
      url: '../test/test'
    });
  },
  pageRouterNavigateTo(){
    // true
    console.log(this.router === this.pageRouter);
    
    // 相对于 this 指代的页面路径 pages/index/index 进行路由跳转
    // 将会跳转到 pages/test/test 页面
    this.pageRouter.navigateTo({
      url: '../test/test'
    });
  },
  routerNavigateTo(){
    // 相对于 this 指代的页面路径 pages/index/index 进行路由跳转
    // 将会跳转到 pages/test/test 页面
    this.router.navigateTo({
      url: '../test/test'
    });
  },
})
```
