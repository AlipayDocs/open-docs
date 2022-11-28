# 简介

**my.regionPicker** 是唤起多级省市区选择器的 API，自带省市区数据源。

## 使用限制

- 基础库 [1.23.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.90 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
Page({
  regionPicker() {
    my.regionPicker({
      mergeOptions: {
        // 新增
        add: [
          {
            pid: '340000',
            id: 'x1',
            name: '新市',
            nextId: '340800',
            subList: [
              {
                name: '新区',
                id: 'x11',
              },
            ],
          },
        ],
        // 删除
        remove: [
          {
            id: '330000',
          },
        ],
        // 更新
        update: [
          {
            id: '110000',
            name: '北京',
            subList: [
              {
                name: '北京市',
                id: '110100',
                subList: [
                  {
                    name: '东城区',
                    id: '110101',
                  },
                ],
              },
            ],
          },
        ],
      },
      selectedItem: ['广东', '深圳', '福田区'],
      success: res => {
        my.alert({
          title: 'regionPicker response: ' + JSON.stringify(res),
        });
      },
    });
  },
});
```

## 返回示例

### success 回调返回示例

执行成功时，触发 success 回调，回调参数示例如下（已转换为 JSON 字符串）：

```json
{
  "data": ["重庆", "重庆", "璧山区"],
  "code": ["500000", "500100", "500120"]
}
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| title | String | 否 | 标题。 |
| mergeOptions | Object | 否 | 自定义修改城市数据，支持删除、添加和更新城市信息。 |
| selectedItem | Array | 否 | 初始选中的省市区名称。不传则默认选中第一个 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |

### Object mergeOptions

**说明**：mergeOptions 对城市信息的删除、添加、更新操作不会全局生效，仅单次生效。

| **参数** | **类型** | **描述**       |
| -------- | -------- | -------------- |
| remove   | Array    | 删除城市信息。 |
| add      | Array    | 添加城市信息。 |
| update   | Array    | 更新城市信息。 |

#### Array remove

| **参数** | **类型** | **描述** |
| --- | --- | --- |
| id | String | 需要移除的对象 ID。可通过 my.regionPicker 回调参数里 code 字段获得 |

#### Array add

| **参数** | **类型** | **描述** |
| --- | --- | --- |
| pid | String | 增加对象的父对象的 ID，新增省份对象时无需此参数。可通过 my.regionPicker 回调参数里 code 字段获得。<br> **注意** ：支付宝 iOS 客户端 10.2.60 之前的版本不支持此参数。 |
| id | String | 增加对象的 ID。 |
| name | String | 增加对象的名称。 |
| nextId | String | 增加对象之后的对象 ID。可通过 my.regionPicker 回调参数里 code 字段获得 |
| subList | Array | 对象下辖的完整的市和区信息。<br />示例：<br />"subList": [{<br />&nbsp;&nbsp;"name": "北京市",<br />&nbsp;&nbsp;"id": "110100",<br />&nbsp;&nbsp;"subList": [{<br />&nbsp;&nbsp;&nbsp;&nbsp;"name": "东城区",<br />&nbsp;&nbsp;&nbsp;&nbsp;"id": "110101"<br />&nbsp;&nbsp;}],······<br/>}] |

#### Array update

| **参数** | **类型** | **描述** |
| --- | --- | --- |
| id | String | 更新对象的 ID。可通过 my.regionPicker 回调参数里 code 字段获得 |
| name | String | 更新对象的名称。 |
| subList | Array | 对象下辖的完整的市和区信息。<br />示例：<br />"subList": [{<br />&nbsp;&nbsp;"name": "北京市",<br />&nbsp;&nbsp;"id": "110100",<br />&nbsp;&nbsp;"subList": [{<br />&nbsp;&nbsp;&nbsp;&nbsp;"name": "东城区",<br />&nbsp;&nbsp;&nbsp;&nbsp;"id": "110101"<br />&nbsp;&nbsp;}]<br />}] |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述**               |
| -------- | -------- | ---------------------- |
| data     | Array    | 选择的省市区名称数组。 |
| code     | Array    | 选择的省市区 ID 数组。 |

### Function fail

fail 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性**     | **类型** | **描述**   |
| ------------ | -------- | ---------- |
| error        | String   | 错误码。   |
| errorMessage | String   | 错误描述。 |

## 错误码

| **错误码** | **描述**         | **解决方案**       |
| ---------- | ---------------- | ------------------ |
| 11         | 用户取消选择     | 重新选择即可。     |
| 10001      | 用户没有选择数据 | 重新选中数据即可。 |

# 常见问题 FAQ

## Q：可以获取 my.regionPicker 中的省市区数据吗？

A：不能直接通过 my.regionPicker 获取省市区数据，只能作为选择器使用。可以通过 [高德 Web API](https://lbs.amap.com/api/webservice/guide/api/district/) 获取最新行政区信息。

## Q：my.regionPicker 不包含最新的行政区信息怎么办？

A：可以通过 mergeOptions 参数自定义修改城市数据，支持删除、添加和更新城市信息。
