# 简介
my.getServerTime 是获取当前服务器时间（从 1970 年 1 月 1 日 0 时 0 分 0 秒（UTC）距离当前时间的毫秒数）的 API。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/a3b3b0843841d6a92ad0275006cc89ab.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/examples/a0582ce9-e2e1-40de-b2dd-cd810d433afe) 

### .axml 示例代码

```html
<!-- API-DEMO page/API/get-server-time/get-server-time.axml-->
<view class="page">
  <view class="page-section">
    <view class="page-section-btns">
      <view onTap="getServerTime">获取服务器时间</view>
    </view>
  </view>
</view>
```

### .js 示例代码

```javascript
// API-DEMO page/API/get-server-time/get-server-time.js
Page({
  getServerTime(){
    my.getServerTime({
      success: (res) => {
        my.alert({
          content: res.time,
        });
      },
    });
  }
})
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| time | Number | 获取当前服务器时间，返回一个数值，代表从 1970 年 1 月 1 日 0 时 0 分 0 秒（UTC）距离当前时间的毫秒数。 |

