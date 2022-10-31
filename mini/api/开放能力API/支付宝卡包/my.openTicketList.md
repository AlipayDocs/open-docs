# 简介

**my.openTicketList** 是打开支付宝票列表的 API。

有关支付宝卡包详细功能，可查看 [支付宝卡包产品介绍](https://opendocs.alipay.com/open/199/105225)。


## 使用限制

此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
my.openTicketList({
  success: (res) => {
    console.log('调用成功',res)
  },
  fail: (error) => {
    console.log('调用失败',error)
  },
  complete: () => {
    console.log('调用完成，无论成功或者失败都会调用')
  }
});
```
### 示例效果图
![avatar](https://img.alicdn.com/imgextra/i2/O1CN01SylD5p1sW5H4WFzhl_!!6000000005773-0-tps-592-1280.jpg)
