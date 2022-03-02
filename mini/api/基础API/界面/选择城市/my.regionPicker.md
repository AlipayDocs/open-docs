
# 简介
**my.regionPicker** 是多级省市区选择器 API，自带省市区数据源。

## 使用限制

- 基础库 [1.23.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.90 或更高版本，若版本较低，建议采取 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。<br />
- IDE 模拟器暂不支持调试，请以真机调试结果为准。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .axml 示例代码
```html
<!-- .axml -->
<view class="page">
  <view class="page-description">多级省市区选择器</view>
  <view class="page-section">
    <view class="page-section-title">regionPicker</view>
    <view class="page-section-demo">
      <button type="primary" onTap="regionPicker">选择城市</button>
    </view>
  </view>
</view>
```

### .js 示例代码
```javascript
// .js
Page({
  regionPicker() {
    my.regionPicker({
      mergeOptions: {
        // 新增
        add: [{
          "id": "x100",
          "name": "新省",
          "nextId": "340000",
          "subList": [{
            "name": "新市",
            "id": "x110",
            "subList": [{
              "name": "新区",
              "id": "x111"
            }]
          }]
        }],
        // 删除
        remove: [{
          "id": "330000"
        }],
        // 更新
        update: [{
          "id": "110000",
          "name": "北京",
          "subList": [{
            "name": "北京市",
            "id": "110100",
            "subList": [{
              "name": "东城区",
              "id": "110101"
            }]
          }]
        }],
        selectedItem: ["广东", "深圳", "福田区"],
      },
      success: (res) => {
        my.alert({
          title: 'regionPicker response: ' + JSON.stringify(res),
        })
      },
    });
  }
})
```

## ﻿入参
| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| title | String | 否 | 标题。 |
| mergeOptions | Object | 否 | 自定义修改城市数据，支持删除、添加和更新城市信息。 |
| selectedItem | Array | 否 | 初始选中的省市区名称。不传则默认选中第一个 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |


### ﻿
**说明**： mergeOptions 对城市信息的删除、添加、更新操作不会全局生效，仅单次生效。

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| remove | Array | 删除城市信息。 |
| add | Array | 添加城市信息。 |
| update | Array | 更新城市信息。 |


#### remove 对象
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| id | String | 需要移除的对象 ID。可通过 my.regionPicker 回调参数里 code 字段获得 |


#### ﻿add 对象
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| id | String | 增加对象的 ID。 |
| name | String | 增加对象的名称。 |
| nextId | String | 插入点之后的对象 ID。可通过 my.regionPicker 回调参数里 code 字段获得 |
| subList | Array | 对象下辖的完整的市和区信息。<br />示例：<br />"subList": [{<br />                "name": "北京市",<br />                "id": "110100",<br />                "subList": [{<br />                    "name": "东城区",<br />                    "id": "110101"<br />                }] ```|


#### ﻿update 对象
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| id | String | 更新对象的 ID。可通过 my.regionPicker 回调参数里 code 字段获得 |
| name | String | 更新对象的名称。 |
| subList | Array | 对象下辖的完整的市和区信息。<br />示例：<br />"subList": [{<br />                "name": "北京市",<br />                "id": "110100",<br />                "subList": [{<br />                    "name": "东城区",<br />                    "id": "110101"<br />                }]<br />﻿ |


### ﻿success 返回值
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| data | Array | 选择的省市区名称数组。 |
| code | Array | 选择的省市区ID数组。 |


### success 返回值示例
以下示例值作为参考，为 JSON 格式。
```json
{
  "data": [
    "重庆",
    "重庆",
    "璧山区"
  ],
  "code": [
    "500000",
    "500100",
    "500120"
  ]
}
```

### ﻿fail 返回值
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| error | String | 错误码。 |
| errorMessage | String | 错误描述。 |


## ﻿错误码
| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 11 | 用户取消选择 | 重新选择即可。 |
| 10001 | 用户没有选择数据 | 重新选中数据即可。 |
