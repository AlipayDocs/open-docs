
# 简介
**my.textRiskIdentification** 是对用户在使用小程序过程产生用户原创内容（UGC）进行风险识别的 API。

详细接入方法，见 [文本风险识别](/mini/introduce/text-identification)。

## 使用限制

- 支付宝客户端 10.1.10 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

## 扫码体验
![|128x158](https://gw.alipayobjects.com/zos/skylark-tools/public/files/81bb273449f36ab0374d0cfaf1e2d405.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例
![|738x415](https://gw.alipayobjects.com/zos/skylark-tools/public/files/ecf86f8540170474bf4cf17d9af34992.png#align=left&display=inline&height=420&margin=%5Bobject%20Object%5D&originHeight=720&originWidth=1280&status=done&style=stroke&width=746)

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// .js
my.textRiskIdentification({
      content: '加我支付宝',
      type: ['keyword', '0', '1', '2', '3'],
      success: (res) => {
        my.alert({
          title: 'ok', // alert 框的标题
          content: JSON.stringify(res),
        });
      },
      fail: (res) => {
        my.alert({
          title: 'fail', // alert 框的标题
          content: JSON.stringify(res),
        });
      },
    });
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| content | String | 是 | 需要进行风险识别的文本内容。 |
| type | StringArray | 是 | 识别类型：<br /><ul><li>keyword：自定义敏感词。</li><li>0：广告。</li><li>1：涉政。</li><li>2：涉黄。</li><li>3：低俗辱骂。</li> |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


### success 回调函数
入参为 Object 类型，属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| result | Object | 文本风险识别的返回结果。 |


#### result 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| type | String | 目标内容文本识别到的类型。<br /><ul><li>keyword：自定义敏感词。</li><li>0：广告。</li><li>1：涉政。</li><li>2：涉黄。</li><li>3：低俗辱骂。</li> |
| hitKeywords | StringArray | 仅当识别命中了 type 为 keyword 时，才会返回该字段。 |
| score | String | 识别命中得分，最高分为 100 分。仅当识别没有命中 keyword ，但入参中包含了广告或涉政或涉黄时，才会返回该字段。 |


### fail 回调函数
入参为 Object 类型，属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| error | String | 识别错误码。 |
| errorMessage | String | 识别错误消息。 |

