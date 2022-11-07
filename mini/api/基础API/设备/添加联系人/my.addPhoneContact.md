# 简介

**my.addPhoneContact** 是用户可以选择将表单以“创建新联系人”或“添加到现有联系人”的方式，写入联系人资料到手机系统的通讯录的 API。

## 使用限制

- 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/923c02f9255e2892e76c94feea5c4df1.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例

![|300x540](https://gw.alipayobjects.com/zos/skylark-tools/public/files/9f9bf631614f647b544bdd8ebdbce69f.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&originHeight=540&originWidth=300&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .json 示例代码

```json
// API-DEMO page/API/contact/contact.json
{
  "defaultTitle": "Contact"
}
```

### .axml 示例代码

```html
<!-- API-DEMO page/API/contact/contact.axml-->
<view class="page">
  <view class="page-description">联系人 API</view>
  <view class="page-section">
    <view class="page-section-title">my.choosePhoneContact</view>
    <view class="page-section-demo">
      <button type="primary" onTap="choosePhoneContact">唤起本地通讯录</button>
    </view>
  </view>
  <view class="page-section">
    <view class="page-section-title">my.chooseAlipayContact</view>
    <view class="page-section-demo">
      <button type="primary" onTap="chooseAlipayContact">
        唤起支付宝通讯录
      </button>
    </view>
  </view>
  <view class="page-section">
    <view class="page-section-title">my.chooseContact</view>
    <view class="page-section-demo">
      <button type="primary" onTap="chooseContact">选择联系人</button>
    </view>
  </view>
  <view class="page-section">
    <view class="page-section-title">my.addPhoneContact</view>
    <view class="page-section-demo">
      <view style="font-size:18px;margin-top:18px;margin-bottom:18px">
        <text style="font-size:18px;margin-top:18px;margin-bottom:18px"
          >基本信息</text
        >
      </view>
      <view class="form-row">
        <view class="form-row-label">昵称</view>
        <view class="form-row-content">
          <input
            id="nickName"
            onInput="onInput"
            class="input"
            value="七月流火"
          />
        </view>
      </view>
      <view class="form-row">
        <view class="form-row-label">姓氏</view>
        <view class="form-row-content">
          <input id="lastName" onInput="onInput" class="input" value="Last" />
        </view>
      </view>
      <view class="form-row">
        <view class="form-row-label">中间名</view>
        <view class="form-row-content">
          <input
            id="middleName"
            onInput="onInput"
            class="input"
            value="Middle"
          />
        </view>
      </view>
      <view class="form-row">
        <view class="form-row-label">名字</view>
        <view class="form-row-content">
          <input id="firstName" onInput="onInput" class="input" value="First" />
        </view>
      </view>
      <view class="form-row">
        <view class="form-row-label">备注</view>
        <view class="form-row-content">
          <input
            id="remark"
            onInput="onInput"
            class="input"
            value="这里是备注"
          />
        </view>
      </view>
      <view class="form-row">
        <view class="form-row-label">手机号</view>
        <view class="form-row-content">
          <input
            id="mobilePhoneNumber"
            onInput="onInput"
            class="input"
            value="13800000000"
          />
        </view>
      </view>
      <view class="form-row">
        <view class="form-row-label">支付宝账号</view>
        <view class="form-row-content">
          <input
            id="alipayAccount"
            onInput="onInput"
            class="input"
            value="alipay@alipay.com"
          />
        </view>
      </view>
      <view class="form-row">
        <view class="form-row-label">微信号</view>
        <view class="form-row-content">
          <input
            id="weChatNumber"
            onInput="onInput"
            class="input"
            value="liuhuo"
          />
        </view>
      </view>
      <view style="font-size:18px;margin-top:18px;margin-bottom:18px">
        <text style="font-size:18px;margin-top:18px;margin-bottom:18px"
          >联系地址</text
        >
      </view>
      <view class="form-row">
        <view class="form-row-label">国家</view>
        <view class="form-row-content">
          <input
            id="addressCountry"
            onInput="onInput"
            class="input"
            value="US"
          />
        </view>
      </view>
      <view class="form-row">
        <view class="form-row-label">省份</view>
        <view class="form-row-content">
          <input
            id="addressState"
            onInput="onInput"
            class="input"
            value="California"
          />
        </view>
      </view>
      <view class="form-row">
        <view class="form-row-label">城市</view>
        <view class="form-row-content">
          <input
            id="addressCity"
            onInput="onInput"
            class="input"
            value="San Francisco"
          />
        </view>
      </view>
      <view class="form-row">
        <view class="form-row-label">街道</view>
        <view class="form-row-content">
          <input
            id="addressStreet"
            onInput="onInput"
            class="input"
            value="Mountain View"
          />
        </view>
      </view>
      <view class="form-row">
        <view class="form-row-label">邮政编码</view>
        <view class="form-row-content">
          <input
            id="addressPostalCode"
            onInput="onInput"
            class="input"
            value="94016"
          />
        </view>
      </view>
      <view style="font-size:18px;margin-top:18px;margin-bottom:18px">
        <text style="font-size:18px;margin-top:18px;margin-bottom:18px"
          >工作</text
        >
      </view>
      <view class="form-row">
        <view class="form-row-label">公司</view>
        <view class="form-row-content">
          <input
            id="organization"
            onInput="onInput"
            class="input"
            value="AntFin"
          />
        </view>
      </view>
      <view class="form-row">
        <view class="form-row-label">职位</view>
        <view class="form-row-content">
          <input id="title" onInput="onInput" class="input" value="Developer" />
        </view>
      </view>
      <view class="form-row">
        <view class="form-row-label">工作传真</view>
        <view class="form-row-content">
          <input
            id="workFaxNumber"
            onInput="onInput"
            class="input"
            value="11111111"
          />
        </view>
      </view>
      <view class="form-row">
        <view class="form-row-label">工作电话</view>
        <view class="form-row-content">
          <input
            id="workPhoneNumber"
            onInput="onInput"
            class="input"
            value="11111112"
          />
        </view>
      </view>
      <view class="form-row">
        <view class="form-row-label">公司电话</view>
        <view class="form-row-content">
          <input
            id="hostNumber"
            onInput="onInput"
            class="input"
            value="11111113"
          />
        </view>
      </view>
      <view class="form-row">
        <view class="form-row-label">电子邮件</view>
        <view class="form-row-content">
          <input
            id="email"
            onInput="onInput"
            class="input"
            value="liuhuo01@sina.com"
          />
        </view>
      </view>
      <view class="form-row">
        <view class="form-row-label">网站</view>
        <view class="form-row-content">
          <input
            id="url"
            onInput="onInput"
            class="input"
            value="www.alipay.com"
          />
        </view>
      </view>
      <view style="font-size:18px;margin-top:18px;margin-bottom:18px">
        <text style="font-size:18px;margin-top:18px;margin-bottom:18px"
          >工作地址</text
        >
      </view>
      <view class="form-row">
        <view class="form-row-label">国家</view>
        <view class="form-row-content">
          <input
            id="workAddressCountry"
            onInput="onInput"
            class="input"
            value="China"
          />
        </view>
      </view>
      <view class="form-row">
        <view class="form-row-label">省份</view>
        <view class="form-row-content">
          <input
            id="workAddressState"
            onInput="onInput"
            class="input"
            value="Zhejiang"
          />
        </view>
      </view>
      <view class="form-row">
        <view class="form-row-label">城市</view>
        <view class="form-row-content">
          <input
            id="workAddressCity"
            onInput="onInput"
            class="input"
            value="Hangzhou"
          />
        </view>
      </view>
      <view class="form-row">
        <view class="form-row-label">街道</view>
        <view class="form-row-content">
          <input
            id="workAddressStreet"
            onInput="onInput"
            class="input"
            value="Tianmushan Road"
          />
        </view>
      </view>
      <view class="form-row">
        <view class="form-row-label">邮政编码</view>
        <view class="form-row-content">
          <input
            id="workAddressPostalCode"
            onInput="onInput"
            class="input"
            value="361005"
          />
        </view>
      </view>
      <view style="font-size:18px;margin-top:18px;margin-bottom:18px">
        <text style="font-size:18px;margin-top:18px;margin-bottom:18px"
          >住宅</text
        >
      </view>
      <view class="form-row">
        <view class="form-row-label">传真</view>
        <view class="form-row-content">
          <input
            id="homeFaxNumber"
            onInput="onInput"
            class="input"
            value="11111114"
          />
        </view>
      </view>
      <view class="form-row">
        <view class="form-row-label">电话</view>
        <view class="form-row-content">
          <input
            id="homePhoneNumber"
            onInput="onInput"
            class="input"
            value="11111115"
          />
        </view>
      </view>
      <view class="form-row">
        <view class="form-row-label">国家</view>
        <view class="form-row-content">
          <input
            id="homeAddressCountry"
            onInput="onInput"
            class="input"
            value="Canada"
          />
        </view>
      </view>
      <view class="form-row">
        <view class="form-row-label">省份</view>
        <view class="form-row-content">
          <input
            id="homeAddressState"
            onInput="onInput"
            class="input"
            value="Ontario"
          />
        </view>
      </view>
      <view class="form-row">
        <view class="form-row-label">城市</view>
        <view class="form-row-content">
          <input
            id="homeAddressCity"
            onInput="onInput"
            class="input"
            value="Toronto"
          />
        </view>
      </view>
      <view class="form-row">
        <view class="form-row-label">街道</view>
        <view class="form-row-content">
          <input
            id="homeAddressStreet"
            onInput="onInput"
            class="input"
            value="No.234 Road"
          />
        </view>
      </view>
      <view class="form-row">
        <view class="form-row-label">邮政编码</view>
        <view class="form-row-content">
          <input
            id="homeAddressPostalCode"
            onInput="onInput"
            class="input"
            value="123456"
          />
        </view>
      </view>
      <button type="primary" onTap="addPhoneContact">添加到手机联系人</button>
    </view>
  </view>
</view>
```

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
| photoFilePath | String | 否 | 头像本地文件路径。 |
| nickName | String | 否 | 昵称。 |
| lastName | String | 否 | 姓氏。 |
| middleName | String | 否 | 中间名。 |
| firstName | String | 否 | 名字。 |
| remark | String | 否 | 备注。 |
| mobilePhoneNumber | String | 否 | 手机号。 |
| alipayAccount | String | 否 | 支付宝账号。 |
| addressCountry | String | 否 | 联系地址国家。 |
| addressState | String | 否 | 联系地址省份。 |
| addressCity | String | 否 | 联系地址城市。 |
| addressStreet | String | 否 | 联系地址街道。 |
| addressPostalCode | String | 否 | 联系地址邮政编码。 |
| organization | String | 否 | 公司。 |
| title | String | 否 | 职位。 |
| workFaxNumber | String | 否 | 工作传真。 |
| workPhoneNumber | String | 否 | 工作电话。 |
| hostNumber | String | 否 | 公司电话。 |
| email | String | 否 | 电子邮件。 |
| url | String | 否 | 网站。 |
| workAddressCountry | String | 否 | 工作地址国家。 |
| workAddressState | String | 否 | 工作地址省份。 |
| workAddressCity | String | 否 | 工作地址城市。 |
| workAddressStreet | String | 否 | 工作地址街道。 |
| workAddressPostalCode | String | 否 | 工作地址邮政编码。 |
| homeFaxNumber | String | 否 | 住宅传真。 |
| homePhoneNumber | String | 否 | 住宅电话。 |
| homeAddressCountry | String | 否 | 住宅地址国家。 |
| homeAddressState | String | 否 | 住宅地址省份。 |
| homeAddressCity | String | 否 | 住宅地址城市。 |
| homeAddressStreet | String | 否 | 住宅地址街道。 |
| homeAddressPostalCode | String | 否 | 住宅地址邮政编码。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

以上字段视不同 ROM 中内置的联系人 App 的支持程度不同，可能不支持 Emoji 表情和颜文字。当不支持时，此项会被忽略。

## 返回值

成功则返回：addPhoneContact response:{"success":true}

## 错误码

| **错误码** | **错误信息** | **描述** | **解决方案** |
| --- | --- | --- | --- |
| 3 | fail ${detail} | 调用失败，detail 中是详细信息。 | - |
