# 简介

**my.hideBackHome** 隐藏标题栏左侧的 **返回首页** 按钮。

## 使用限制

- 基础库 [1.16.4](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.52 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 效果示例

![|600x338](https://cdn.nlark.com/yuque/0/2021/png/179989/1624617388445-56a25e52-e70c-4899-bd62-dea1a8cc24fe.png#align=left&display=inline&height=338&margin=%5Bobject%20Object%5D&name=f663e0473f32d0a8514999ced6d8e65d.png&originHeight=720&originWidth=1280&size=52052&status=done&style=none&width=600)

# 接口调用

## 示例代码

```javascript
// 示例一
Page({
  onReady() {
    if (my.canIUse('hideBackHome')) {
      my.hideBackHome();
    }
  },
});

// 示例二
Page({
  onLoad() {
    // 跳到非首页
    my.reLaunch({
      url: '../swiper/swiper', 
    });
    // 5 秒后隐藏返回首页按钮
    setTimeout(() => {
      my.hideBackHome();
    }, 5000);
  },
});
```

# 常见问题 FAQ

## Q：导航栏左上角的 **返回首页** 按钮和 **返回上一页** 按钮何时会展示？

A: 当页面栈深度为 1 时，标题栏左上角默认展示 **返回首页** 按钮；当页面栈深度大于 1 时，默认展示 **返回上一页** 按钮。默认首页和 tabBar 页面不展示返回首页和返回上一页按钮。

**页面栈** 是小程序框架管理界面的方式，可以使用 [getCurrentPages](https://opendocs.alipay.com/mini/framework/getcurrentpages)().length 查看当前页面栈深度。

小程序导航相关 API 对页面栈深度的影响如下：
- my.navigateTo 保留当前页面，打开新页面，页面栈深度加 1；
- my.redirectTo 关闭当前页面，打开新页面，页面栈深度不变；
- my.navigateBack 关闭当前页面，回到前一页，页面栈减 1（传入的 delta 值大于 1 时请自行类推）；
- my.reLaunch 关闭所有页面，打到新页面，页面栈深度重置为 1。

## Q：如何隐藏页面的 **返回上一页** 按钮？

A：不提供 API 直接隐藏页面的回退按钮，可通过 my.reLaunch 进行页面跳转（将页面栈深度置为 1），返回上一页按钮即不展示；如有必要，也可在跳转目标页面里调用 my.hideBackHome 以隐藏返回首页按钮。
