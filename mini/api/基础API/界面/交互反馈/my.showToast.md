
# 简介
**my.showToast** 是显示一个弱提示，在到达设定的显示时间后自动消失弱提示的 API。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/e9f3b3c8c7c3cd7d169955c9facf59fa.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/examples/863c53fd-fd81-4ca0-baed-45cc8f8190e8)


### .axml 示例代码
```html
<!-- toast.axml-->
<view class="page">
 <view type="primary" onTap="showToastSuccess">显示 success 提示</view>
</view>
```

### .js 示例代码
```javascript
// toast.js
Page({
  showToastSuccess() {
    my.showToast({
      type: 'success',
      content: '操作成功',
      duration: 3000,
      success: () => {
        my.alert({
          title: 'toast 消失了',
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
| content | String | 否 | 文字内容。 |
| type | String | 否 | toast 类型，展示相应图标，默认 none，支持 success / fail / exception / none。其中 exception 类型必须传文字信息。 |
| duration | Number | 否 | 显示时长，单位为 ms，默认值为 3000。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |
