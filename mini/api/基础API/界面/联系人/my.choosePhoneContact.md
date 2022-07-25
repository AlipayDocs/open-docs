# 简介
**my.choosePhoneContact** 是选择本地系统通信录中某个联系人的电话的 API。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/2af29e82e83aa4eeeac56c006dd2f79f.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 在线示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/contact?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light) 

### .js 示例代码
```javascript
// API-DEMO page/API/contact/contact.js
Page({
  data:{
    "photoFilePath": "/sdcard/DCIM/Camera/a.jpg",
    "nickName": "七月流火",
    "lastName": "Last",
    "middleName": "Middle",
    "firstName": "First",
    "remark": "这里是备注",
    "mobilePhoneNumber": "13800000000",
    "homePhoneNumber": "11111115",
    "workPhoneNumber": "11111112",
    "homeFaxNumber": "11111114",
    "workFaxNumber": "11111111",
    "hostNumber": "11111113",
    "weChatNumber": "liuhuo",
    "alipayAccount": "alipay@alipay.com",
    "addressCountry": "US",
    "addressState": "California",
    "addressCity": "San Francisco",
    "addressStreet": "Mountain View",
    "addressPostalCode": "94016",
    "workAddressCountry": "China",
    "workAddressState": "Zhejiang",
    "workAddressCity": "Hangzhou",
    "workAddressStreet": "Tianmushan Road",
    "workAddressPostalCode": "361005",
    "homeAddressCountry": "Canada",
    "homeAddressState": "Ontairo",
    "homeAddressCity": "Toronto",
    "homeAddressStreet": "No.234 Road",
    "homeAddressPostalCode": "123456",
    "organization": "AntFin",
    "title": "Developer",
    "email": "liuhuo01@sina.com",
    "url": "www.alipay.com",
    success: (res) => {
      my.alert({
        content: 'addPhoneContact response: ' + JSON.stringify(res)
      });
    },
    fail: (res) => {
      my.alert({
        content: 'addPhoneContact response: ' + JSON.stringify(res)
      });
    }
  },
  choosePhoneContact() {
    my.choosePhoneContact({
      success: (res) => {
        my.alert({
          content: 'choosePhoneContact response: ' + JSON.stringify(res)
        });
      },
      fail: (res) => {
        my.alert({
          content: 'choosePhoneContact response: ' + JSON.stringify(res)
        });
      },
    });
  },
  chooseAlipayContact() {
    my.chooseAlipayContact({
      count: 2,
      success: (res) => {
        my.alert({
          content: 'chooseAlipayContact response: ' + JSON.stringify(res)
        });
      },
      fail: (res) => {
        my.alert({
          content: 'chooseAlipayContact response: ' + JSON.stringify(res)
        });
      },
    });
  },
  chooseContact() {
    my.chooseContact({
      chooseType: 'multi', // 多选模式
      includeMe: true,     // 包含自己
      includeMobileContactMode: 'known',//仅包含双向手机通讯录联系人，也即双方手机通讯录都存有对方号码的联系人
      multiChooseMax: 3,  // 最多能选择三个联系人
      multiChooseMaxTips: '超过选择的最大人数了',
      success: (res) => {
        my.alert({
          content: 'chooseContact : ' + JSON.stringify(res)
        });
      },
      fail: (res) => {
        my.alert({
          content: 'chooseContact : ' + JSON.stringify(res)
        });
      },
    });
  },
  onInput(e) {
    this.data[e.currentTarget.id] = e.detail.value;
  },
  addPhoneContact() {
    if (my.canIUse('addPhoneContact')) {
      my.addPhoneContact(this.data);
    } else {
      my.alert({ 
        title: '客户端版本过低',
        content: 'my.addPhoneContact() 需要 10.1.32 及以上版本'
      });
    }
  }
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


### success 回调函数

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| name | String | 选中的联系人姓名。 |
| mobile | String | 选中的联系人手机号。 |


## 错误码

| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 10 | 没有权限。 | 检查权限限制。 |
| 11 | 用户取消操作（或设备未授权使用通讯录）。 | 建议设备授权使用通讯录。 |
