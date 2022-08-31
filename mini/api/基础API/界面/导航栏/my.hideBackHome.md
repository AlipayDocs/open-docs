# 简介

**my.hideBackHome** 是隐藏标题栏上的 **返回首页** 按钮和右上角通用菜单中的返回首页功能的 API。

当用户打开的小程序最底层页面是非首页且非 tabbar 页面时，默认展示 **返回首页** 按钮，可以通过调用 my.hideBackHome 进行隐藏。

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
