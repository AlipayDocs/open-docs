
# 简介
**my.multiLevelSelect** 是级联选择功能 API。主要用于选择多级关联数据，比如省市区的信息选择。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-multi-level-select?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .json 示例代码
```json
{
     "defaultTitle": "多级联选择器"
}
```

### .axml 示例代码
```html
<!-- API-DEMO page/API/multi-level-select/multi-level-select.axml-->
<view class="page">
  <view class="page-description">多级联选择器 API</view>
  <view class="page-section">
    <view class="page-section-title">my.multiLevelSelect</view>
    <view class="page-section-demo">
      <button type="primary" onTap="openMultiLevelSelect">多级联选择器</button>
    </view>
  </view>
</view>
```

### .js 示例代码
```javascript
// API-DEMO page/API/multi-level-select/multi-level-select.js
Page({
  openMultiLevelSelect() {
    my.multiLevelSelect({
        title: '多级联选择器',//级联选择标题
        list: [
        {
            name: "杭州市",//条目名称
            subList: [
                {
                    name: "西湖区",
                    subList: [
                        {
                            name: "古翠街道"
                        },
                        {
                            name: "文新街道"
                        }
                    ]
                },
                {
                    name: "上城区",
                    subList: [
                        {
                            name: "延安街道"
                        },
                        {
                            name: "龙翔桥街道"
                        }
                    ]
                }
            ]//级联子数据列表
        }],//级联数据列表
        success:(res)=>{
            my.alert({title:JSON.stringify(res)})
        }
    });
  }
})
```

## 入参
入参为 Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| title | String | 否 | 标题。 |
| list | JsonArray | 是 | 选择数据列表。具体对象值参见下方 list 对象表。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


### list 对象
| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| name | String | 是 | 条目名称。 |
| subList | JsonArray | 否 | 子条目列表。 |


### success 回调函数
入参为 Object 类型，属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| success | Boolean | 是否选择完成，取消返回 false。 |
| result | JsonArray | 选择的结果，如 [{“name”:”杭州市”},{“name”:”上城区”},{“name”:”古翠街道”}]。 |

