# 简介

**my.showActionSheet** 是显示操作菜单的 API。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/8b18ebd5beaee3db9120b720546b0aea.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 在线示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/action-sheet?view=preview&defaultPage=pages%2Findex%2Findex&defaultOpenedFiles=pages%2Findex%2Findex&theme=light) 

### .json 示例代码

```json
{
    "defaultTitle": "Action Sheet"
}
```

### .axml 示例代码

```html
<!-- API-DEMO page/API/action-sheet/action-sheet.axml-->
<view class="page">
  <view class="page-description">操作菜单 API</view>
  <view class="page-section">
    <view class="page-section-title">my.showActionSheet</view>
    <view class="page-section-demo">
      <button type="primary" onTap="showActionSheet">显示操作菜单</button>
    </view>
  </view>
</view>
```

### .js 示例代码

```javascript
// API-DEMO page/API/action-sheet/action-sheet.js
Page({
  showActionSheet() {
    my.showActionSheet({
      title: '支付宝-ActionSheet',
      items: ['菜单一', '菜单二', '菜单三'],
      cancelButtonText: '取消好了',
      success: (res) => {
        const btn = res.index === -1 ? '取消' : '第' + res.index + '个';
        my.alert({
          title: `你点了${btn}按钮`
        });
      },
    });
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| title | String | 否 | 菜单标题。 |
| items | String Array | 是 | 菜单按钮文字数组。 |
| cancelButtonText | String | 否 | 取消按钮文案。默认为 **取消**。<br />**注意**：Android 平台此字段无效，不会显示取消按钮。 |
| destructiveBtnIndex | Number | 否 | （iOS 特殊处理）指定按钮的索引号，从 0 开始。<br />使用场景：需要删除或清除数据等类似场景，默认为红色。 |
| badges | ObjectArray | 否 | 需飘红选项的数组，数组内部对象字段见下方 **ObjectArray badges**。<br />**注意**：基础库 [1.9.0](https://opendocs.alipay.com/mini/framework/lib) 及以上版本开始支持。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### ObjectArray badges

| **参数** | **类型** | **描述** |
| --- | --- | --- |
| index | Number | 需要飘红的选项的索引，从 0 开始。 |
| type | String | 飘红类型。<br />可选值：<ul><li>none：无红点。</li><li>point：纯红点。</li><li>num：数字红点。</li><li>text：文案红点。</li><li>more：显示 `...`。</li></ul> |
| text | String | 自定义飘红文案。<ul><li>type 为 `none`、`point`、`more` 时，`text` 可不填。</li><li>type 为 num 时，`text` 为小数或 ≤ 0 均不显示, ≥ 100 显示"..."。</li></ul> |
