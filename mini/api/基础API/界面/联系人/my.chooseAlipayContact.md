# 简介

**my.chooseAlipayContact** 是用于唤起支付宝通讯录，选择一个或者多个支付宝联系人的 API。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/b4c0871505fd79b356ee24711e25e718.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 在线示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/contact?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light)

### .js 示例代码

```javascript
// API-DEMO page/API/contact/contact.js
Page({
  data: {
    photoFilePath: '/sdcard/DCIM/Camera/a.jpg',
    nickName: '七月流火',
    lastName: 'Last',
    middleName: 'Middle',
    firstName: 'First',
    remark: '这里是备注',
    mobilePhoneNumber: '13800000000',
    homePhoneNumber: '11111115',
    workPhoneNumber: '11111112',
    homeFaxNumber: '11111114',
    workFaxNumber: '11111111',
    hostNumber: '11111113',
    weChatNumber: 'liuhuo',
    alipayAccount: 'alipay@alipay.com',
    addressCountry: 'US',
    addressState: 'California',
    addressCity: 'San Francisco',
    addressStreet: 'Mountain View',
    addressPostalCode: '94016',
    workAddressCountry: 'China',
    workAddressState: 'Zhejiang',
    workAddressCity: 'Hangzhou',
    workAddressStreet: 'Tianmushan Road',
    workAddressPostalCode: '361005',
    homeAddressCountry: 'Canada',
    homeAddressState: 'Ontairo',
    homeAddressCity: 'Toronto',
    homeAddressStreet: 'No.234 Road',
    homeAddressPostalCode: '123456',
    organization: 'AntFin',
    title: 'Developer',
    email: 'liuhuo01@sina.com',
    url: 'www.alipay.com',
    success: res => {
      my.alert({
        content: 'addPhoneContact response: ' + JSON.stringify(res),
      });
    },
    fail: res => {
      my.alert({
        content: 'addPhoneContact response: ' + JSON.stringify(res),
      });
    },
  },
  choosePhoneContact() {
    my.choosePhoneContact({
      success: res => {
        my.alert({
          content: 'choosePhoneContact response: ' + JSON.stringify(res),
        });
      },
      fail: res => {
        my.alert({
          content: 'choosePhoneContact response: ' + JSON.stringify(res),
        });
      },
    });
  },
  chooseAlipayContact() {
    my.chooseAlipayContact({
      count: 2,
      success: res => {
        my.alert({
          content: 'chooseAlipayContact response: ' + JSON.stringify(res),
        });
      },
      fail: res => {
        my.alert({
          content: 'chooseAlipayContact response: ' + JSON.stringify(res),
        });
      },
    });
  },
  chooseContact() {
    my.chooseContact({
      chooseType: 'multi', // 多选模式
      includeMe: true, // 包含自己
      includeMobileContactMode: 'known', //仅包含双向手机通讯录联系人，也即双方手机通讯录都存有对方号码的联系人
      multiChooseMax: 3, // 最多能选择三个联系人
      multiChooseMaxTips: '超过选择的最大人数了',
      success: res => {
        my.alert({
          content: 'chooseContact : ' + JSON.stringify(res),
        });
      },
      fail: res => {
        my.alert({
          content: 'chooseContact : ' + JSON.stringify(res),
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
        content: 'my.addPhoneContact() 需要 10.1.32 及以上版本',
      });
    }
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| count | Number | 否 | 单次最多选择联系人个数，默认值为 1，最大值为 10。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### success 回调函数

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型**     | **描述**                                         |
| -------- | ------------ | ------------------------------------------------ |
| contacts | Object/Array | 选中的支付宝联系人数组，数组内部对象字段见下表。 |

#### Object/Array contacts

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| realName | String | 账号的真实姓名。 |
| mobile | String | 账号对应的手机号码。<br />**注意**：<br /><ul><li>请在手机端开启支付宝客户端的通讯录权限，否则可能出现获取不到手机号码的情况。</li><li>手机本地系统通讯录号码需要与支付宝好友手机号码一致，否则可能出现获取不到手机号码的情况。</li></ul> |
| email | String | 账号的邮箱。 |
| avatar | String | 账号的头像链接。 |
| userId | String | 支付宝账号唯一标识符。 |

**注意**：返回的 `mobile` 和 `email`  字段不一定全部有值，取决于所选取联系人的支付宝账号类型是手机号还是邮箱。

## 错误码

| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 10 | 没有权限。 | 检查权限设置。 |
| 11 | 用户取消操作（或设备未授权使用通讯录）。 | 建议设备授权使用通讯录。 |
