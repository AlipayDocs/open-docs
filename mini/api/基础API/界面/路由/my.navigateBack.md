
# 简介
**my.navigateBack** 是关闭当前页面，返回上一级或多级页面的 API。可通过 [Page.getCurrentPages](https://opendocs.alipay.com/mini/framework/getcurrentpages) 获取当前的页面栈信息，决定需要返回几层。

相关问题请参见 [路由FAQ](https://opendocs.alipay.com/mini/api/fu8l65) 。


## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![image.png](https://cdn.nlark.com/yuque/0/2021/png/179989/1637056770503-813c17f4-e76c-4870-a0c7-5aae8768a06c.png#align=left&display=inline&height=127&margin=%5Bobject%20Object%5D&name=image.png&originHeight=157&originWidth=127&size=16714&status=done&style=none&width=103)

## 示例代码

### .json 示例代码
```json
{
  "defaultTitle": "Navigator"
}
```

### .axml 示例代码
```html
<!-- navigateTo.axml-->
<view class="page">
  <view class="page-section">
    <button type="primary" onTap="navigateTo">跳转新页面</button>
    <button type="primary" onTap="redirectTo">在当前页面打开新页面</button>
    <button type="primary" onTap="switchTab">跳转到“我的”</button>
    <button type="primary" onTap="reLaunch">重新打开</button>
  </view>
</view>
```

### .js 示例代码

```javascript
// navigateTo.js
Page({
  navigateTo() {
    my.navigateTo({ url: './back' })
  },
  redirectTo() {
    my.redirectTo({ url: './back' })
  },
  reLaunch() {
    my.reLaunch({
      url: '/demo/my',
    })
  },
  switchTab() {
    my.switchTab({
        url: '/demo/my',
        success: () => {
          my.showToast({
            content: '成功',
            type: 'success',
            duration: 4000
          });
        }
      }
    );
  },
})
```

### .axml 示例代码

```html
<!-- navigateBack.axml-->
<view class="page">
  <view class="page-section">
    <button type="primary" onTap="navigateBack">返回上一页</button>
  </view>
</view>
```

### .js 示例代码
```javascript
// navigateBack.js
Page({
  navigateBack() {
    my.navigateBack()
  },
})
```

### .json 示例代码
```json
{
  "defaultTitle": "Navigator"
}
```


## 入参
| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| delta | Number | 否 | 返回的页面数，如果 delta 大于现有打开的页面数，则返回到首页。默认值为 1。 |

