# 简介

**my.hideBackHome** 是隐藏标题栏上的 **返回首页** 按钮和右上角通用菜单中的返回首页功能的 API。

当页面栈深度为 1 时，标题栏左上角默认展示 **返回首页** 按钮；当页面栈深度大于 1 时，默认展示 **返回上一页** 按钮。更多信息可查看 [怎么显示小程序标题栏中的返回首页按钮](https://opendocs.alipay.com/mini/api/ui-navigate#Q：怎么显示小程序标题栏中的返回首页按钮？)

## 使用限制

- 基础库 [1.16.4](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.52 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 效果示例

![|600x338](https://cdn.nlark.com/yuque/0/2021/png/179989/1624617388445-56a25e52-e70c-4899-bd62-dea1a8cc24fe.png#align=left&display=inline&height=338&margin=%5Bobject%20Object%5D&name=f663e0473f32d0a8514999ced6d8e65d.png&originHeight=720&originWidth=1280&size=52052&status=done&style=none&width=600)

# 接口调用

## 示例代码

### .js 示例代码

```javascript
//.js
Page({
  onReady() {
    if (my.canIUse('hideBackHome')) {
      my.hideBackHome();
    }
  },
});
```

```javascript
//.js
Page({
  onLoad() {
    my.reLaunch({
      url: '../swiper/swiper', // 在页面中添加的非首页
    });

    setTimeout(() => {
      //5秒后隐藏返回首页按钮
      my.hideBackHome();
    }, 5000);
  },
});
```

# 常见问题 FAQ

## Q：如何隐藏页面的回退按钮？

A：暂无 API 可以直接隐藏页面的回退按钮。可以先通过 my.reLaunch 进行页面跳转，在被跳转的页面里调用 my.hideBackHome 隐藏返回首页按钮。

## Q：怎么显示小程序标题栏中的返回首页按钮？
A：当页面栈深度为 1 时，标题栏左上角默认展示返回首页按钮；当页面栈深度大于 1 时，默认展示返回上一页按钮。**页面栈** 是小程序框架管理界面的方式，可以使用 getCurrentPages().length 查看当前页面栈页面深度。详情可查看 [getCurrentPages](https://opendocs.alipay.com/mini/framework/getcurrentpages) 方法。当只展示首页时，页面栈深度为 1，默认首页和 tabBar 页面不展示返回首页或者返回上一页按钮。当使用 my.navigateTo 跳转页面时，因为 my.navigateTo 是保留当前页面，跳转到新页面，所以此时页面栈深度加 1，展示的是返回上一页按钮；当使用 my.redirectTo 跳转页面时，因为 my.redirectTo 是关闭当前页面，跳转到新页面，所以此时页面栈深度不增加，此时是分两种情况的，若之前页面栈深度大于 1，则显示返回上一页按钮，若等于1，则显示返回首页按钮；当使用 my.reLaunch 跳转页面时，因为 my.reLaunch 是关闭所有页面，跳转到新页面，所以此时页面栈深度置为 1，显示的是返回首页按钮。
