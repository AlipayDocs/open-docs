# 简介

**my.chooseContact** 是唤起选择联系人的 API，默认只包含支付宝联系人，可通过修改参数选择手机通讯录联系人或者双向通讯录联系人。

## 使用限制

- 基础库 [1.4.0](https://opendocs.alipay.com/mini/framework/lib)   或更高版本；支付宝客户端 10.1.8 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/cdaf692bb22982c98f0104dc69587c17.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

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
| chooseType | String | 是 | 选择类型，值为 single（单选）或者 multi（多选）。 |
| includeMobileContactMode | String | 否 | 选择手机通讯录联系人的模式。<br /><ul><li>none：默认为只包含支付宝联系人，不包含手机通讯录联系人；</li><li>known：仅包含双向通讯录联系人，即双方手机通讯录都存有对方号码的联系人；</li><li>all：包含所有通讯录联系人。</li></ul> |
| includeMe | Boolean | 否 | 是否包含自己。 |
| multiChooseMax | Number | 否 | 最大选择人数，仅 chooseType 为 multi 时才有效。 |
| multiChooseMaxTips | String | 否 | 多选达到上限时提示的文案，仅 chooseType 为 multi 时才有效。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### success 回调函数

**说明**：当用户没有选择任何联系人时，返回也是 success，但是返回值为空。

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性**         | **类型**    | **描述**             |
| ---------------- | ----------- | -------------------- |
| contactsDicArray | StringArray | 选择返回的用户信息。 |

#### StringArray contactsDicArray

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| userId | String | 支付宝账号唯一标识符。 |
| avatar | String | 账号的头像链接。 |
| mobile | String | 账号对应的手机号码。<br />**注意**：<br /><ul><li>请在手机端开启支付宝客户端的通讯录权限，否则可能出现获取不到手机号码的情况。</li><li>手机本地系统通讯录号码需要与支付宝好友手机号码一致，否则可能出现获取不到手机号码的情况。</li></ul> |
| realName | String | 账号的真实姓名。 |
| displayName | String | 账号的显示名称，即支付宝设置的备注名称，默认为朋友圈里面的昵称。 |

# 常见问题

## Q：如果系统权限未开启，接口调用报错，如何引导开启系统权限？

A：可以调用 [my.showAuthGuide](https://opendocs.alipay.com/mini/api/show-auth-guide) 引导用户开启相关系统权限。
