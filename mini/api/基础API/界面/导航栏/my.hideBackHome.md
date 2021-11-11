
# 简介
**my.hideBackHome** 是隐藏标题栏上的返回首页图标（如下图所示）和右上角通用菜单中的返回首页功能的 API。

## 使用限制

- 基础库 [1.16.4](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.52 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- 用户启动小程序时，若进入的页面不是小程序首页，则会在左上角出现返回首页图标。
- 如果 app.json 中配置了 tabbar 跳转 pages/index/index 时，则左上角不会出现 返回首页 icon 图标。
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

### .js 示例代码
```javascript
//.js
onLoad(){
    my.reLaunch({
    url:'../swiper/swiper'// 在页面中添加的非首页
  })
  
  setTimeout(() => {
    //5秒后隐藏返回首页按钮
    my.hideBackHome()
  }, 5000)
}
```
