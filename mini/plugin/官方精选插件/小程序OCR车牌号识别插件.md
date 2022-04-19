# 产品介绍
以小程序插件形式输出，OCR-车牌号识别插件可帮助开发者快速实时识别并返回车牌号信息和相关图片数据。该插件是纯前端能力，无需依赖后端，也不会传输任何数据到后端。

## 产品特色
商家/服务商（ISV） 价值：生活缴费场景，减少人工成本，可以让用户自己完成车牌号数据上传。

## 准入条件

- 仅支持支付宝企业账号使用。
- 具备一定的技术能力，能够独立或由 ISV 协助完成技术对接。
- 支持合作后的服务联动处理，数据反馈和异议处理。

## 场景说明
以本地生活 App 为例，选择小程序后，展示的识别流程。

1. 用户在小程序上开启车牌识别功能；
1. 识别插件唤起相机和识别功能，对准车牌号区域扫一扫识别；
1. 识别成功后返回车牌号和图片到小程序；
1. 用户可自行修改识别结果，并提交结果。 <br/>
![|320x572](https://mdn.alipayobjects.com/afts/img/A*3RwfS5qPlEoAAAAAAAAAAAAAAa8wAA/original?bz=openpt_doc&t=DaNBPk5RaQFLfjtWb7qnKwAAAABkMK8AAAAA#align=left&display=inline&height=572&margin=%5Bobject%20Object%5D&originHeight=572&originWidth=320&status=done&style=none&width=320) 
![|320x572](https://mdn.alipayobjects.com/afts/img/A*c3nyTbZcmz0AAAAAAAAAAAAAAa8wAA/original?bz=openpt_doc&t=HFUIlhjKxlM9FZVQTpnj0QAAAABkMK8AAAAA#align=left&display=inline&height=572&margin=%5Bobject%20Object%5D&originHeight=572&originWidth=320&status=done&style=none&width=320)

# 接入指引
支付宝 App 10.1.92 或更高版本支持 OCR-车牌号识别插件。

## 第一步：创建小程序
要在小程序内使用小程序 OCR-车牌号识别插件，首先请完成 [平台入驻](https://opendocs.alipay.com/common/02asmu) 并 [创建小程序](https://opendocs.alipay.com/mini/introduce/create)。 

## 第二步：订购插件
完成创建小程序后，使用小程序所属的主体支付宝账号，在插件中心订购并获取 [小程序OCR车牌号识别插件](https://open.alipay.com/plugin/order-page?serviceCode=MP2020121900100072)，详情可查看 [插件获取](https://opendocs.alipay.com/mini/plugin/plugin-order)。

## 第三步：修改小程序参数
示例插件 APPID：2021001130699293

### app.json 插件配置

```json
{
  "pages": [
    "pages/index/index",
    "pages/ocr/ocr"  ],
  "plugins": {
    "myPlugin": {
      "version": "*",
      "provider": "2021001130699293"        // 插件 appId    }
  }
}
```

### OCR 插件页面

```javascript
// pages/ocr/ocr.json
{
  "usingComponents": {
     "ocr-plate": "plugin://myPlugin/ocr-plate"  }
}
```

```html
<!-- pages/ocr/ocr.axml -->
<ocr-plate onComplete="onCompleteOcr" 
  title="{{ocrTitle}}"
  imageOutput="{{imageOutput}}" />
```

```javascript
// pages/ocr/ocr.js
var app = getApp();
Page({
  data: {
    imageOutput: 'roi'  // 'global' || 'roi'  },
  onLoad(query) {
    console.info(`Page onLoad with query: ${JSON.stringify(query)}`);
  },
  onCompleteOcr(data) {
    console.log(data, 'onCompleteOcr callback');
    if (data.image) {
      const img = "data:image/jpeg;base64," + data.image.replace(/\s/g, '');
      app.imageData = img;
    }
  },
});
```

### 插件属性
| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| onComplete | (data) => {} | 是 | 识别结果回调。 |
| title | String | 否 | 提示语。 |
| imageOutput | String | 否 | 返回 ROI 图或全图。<br />**默认值**：roi<br />**可选值**：global |


### 识别结果 data 

#### 车牌号

```javascript
{
  "success": true,
  "result": [
   {
      "name":"ocr_vehicle_plate",
      "type": "cv_common",
      "body": [
        { "label": "1234567890123456", "conf": 0.6, "pos": [[0.11, 0.22], [0.33, 0.44], [0.11, 0.22], [0.33, 0.44]] }
      ]
   }
  ],
  "image":"base64string"}
```

## 第四步：展示效果
![|320x572](https://mdn.alipayobjects.com/afts/img/A*3RwfS5qPlEoBpgxNkRmF5QAAAa8wAA/original?bz=openpt_doc&t=MLHTnt93Aj0z5HbkDRT82gAAAABkMK8AAAAA#align=left&display=inline&height=572&margin=%5Bobject%20Object%5D&originHeight=572&originWidth=320&status=done&style=none&width=320)
