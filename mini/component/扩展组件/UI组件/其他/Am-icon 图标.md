# 简介

图标。

## 扫码体验

![|154x191](https://mdn.alipayobjects.com/afts/img/A*FIgnQYG0eU4Cu2dKuSefyABkAa8wAA/original?bz=openpt_doc&t=P5eibJNtHlEwlULPUKeZ8QAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-am-icon?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### .json 示例代码

```json
{
  "defaultTitle": "am-icon icon 图标",
  "usingComponents": {
    "am-icon": "mini-ali-ui/es/am-icon/index"
  }
}
```

### .axml 示例代码

```html
<view class="icon-list">
  <block a:for="{{iconTypes}}">
    <view class="icon-item">
      <am-icon type="{{item}}" size="30" />
      <text class="icon-desc">{{item}}</text>
    </view>
  </block>
</view>
```

### .js 示例代码

```javascript
Page({
  data: {
    iconTypes: [
      'qr',
      'share',
      'picture',
      'add-square',
      'file',
      'text',
      'minus-square',
      'barcode',
      'wallet',
      'scan-code',
      'receipt',
      'down-circle',
      'bill-note',
      'trash',
      'bill',
      'scan',
      'content',
      'circle',
      'play',
      'limit',
      'money',
      'link',
      'zoom-in',
      'koubei',
      'location',
      'capslock',
      'time-5',
      'warn',
      'help',
      'close-circle',
      'selected',
      'search',
      'net',
      'chat',
      'contacts',
      'appx',
      'question',
      'person-setting',
      'setting',
      'like',
      'ant',
      'add',
      'more',
      'more-1',
      'zoom-out',
      'money-circle',
      'collect',
      'voice',
      'good',
      'voice-limit',
      'people',
      'person-add',
      'download',
      'sad',
      'left',
      'right',
      'eye-close',
      'eye',
      'koubei_',
      'star_',
      'check',
      'chat_',
      'help_',
      'key_',
      'lock_',
      'people_',
      'voice-limit_',
      'location_',
      'phone_',
      'logo-alipay_',
      'person-delete_',
      'wait_',
      'apps_',
      'microphone_',
      'pen_',
      'close_',
      'question_',
      'down_',
      'certified-check_',
      'certified-warn_',
      'sad_',
      'ant_',
      'time-5_',
      'warn_',
      'person-circle_',
      'time-3_',
      'check_',
      'logo-alipays',
      'like_',
      'home',
      'eye_',
      'edit_',
      'mail_',
      'forbid_',
      'eye-limit_',
      'delete-person_',
      'close',
      'address-book_',
      'person',
      'gift',
      'add-message',
      'alipay',
      'phone-book_',
      'delete_',
      'down',
      'up',
    ],
  },
  onLoad() {},
});
```

## 属性说明

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| className | String | false | 自定义 class。 |
| type | String | true | icon 类型，具体效果扫上面二维码预览（有效值请见下方表格）。 |
| size | String | false | icon 大小，单位 px。<br />**默认值：** 17 |
| color | String | false | icon 颜色，同 css 的 color。 |

### type 有效值

| **图标风格** | **type 有效值** |
| --- | --- |
| 线条型 | `add`、 `add-message`、 `add-square`、 `alipay`、 `ant`、 `appx`、 `barcode`、 `bill`、 `bill-note`、 `capslock`、 `chat`、 `check`、 `circle`、 `close`、 `close-circle`、 `collect`、 `contacts`、 `content`、 `down`、 `down-circle`、 `download`、 `eye`、 `eye-close`、`file`、 `gift`、 `good`、 `help`、 `home`、 `koubei`、 `left`、 `like`、 `limit`、 `link`、`location`、`logo-alipays`、 `minus-square`、 `money`、 `money-circle`、 `more`、 `more-1`、 `net`、 `people`、 `person`、 `person-add`、 `person-setting`、 `picture`、 `play`、 `qr`、 `question`、 `receipt`、 `right`、 `sad`、 `scan`、 `scan-code`、 `search`、 `selected`、 `setting`、 `share`、 `text`、 `time-5`、 `trash`、 `up`、 `voice`、 `voice-limit`、 `wallet`、 `warn`、 `zoom-in`、 `zoom-out` |
| 实心型 | `address-book_`、`ant_`、 `apps_`、 `certified-check_`、 `certified-warn_`、 `chat_`、 `check_`、 `close_`、 `delete_`、`delete-person_`、 `down_`、 `edit_`、 `eye_`、 `eye-limit_`、 `forbid_`、 `help_`、 `key_`、 `koubei_`、 `like_`、 `location_`、 `lock_`、 `logo-alipay_`、 `mail_`、 `microphone_`、 `pen_`、 `people_`、 `person-circle_`、 `person-delete_`、 `phone_`、 `phone-book_`、`question_`、 `sad_`、`star_`、 `time-3_`、 `time-5_`、 `voice-limit_`、`wait_`、 `warn_` |

## Bug & Tip

- `size`只需要填写纯数字，默认增加 `px` 单位，当安装 **mini-ali-ui-rpx npm** 包后，默认增加`rpx` 单位，仅仅只是默认增加的单位，具体的 `size` 将根据所填写的值而显示。比如 `size="30"`，最终得到的可能就是 `30px` 或者 `30rpx` 的结果。
- `color` 默认为空，可继承父级元素的颜色值。
- **am-icon** 使用的是 iconfont 方式，如通过 `className` 方式控制大小，需要通过设置 `font-size` 来改变。
- 如果设置 `size` 和 `color` 属性后无效，那么很大可能就是当前设备 不支持 CSS 自定义属性（CSS 变量），只能通过 className 方式来修改 `font-size` 和 `color` 的属性值。
