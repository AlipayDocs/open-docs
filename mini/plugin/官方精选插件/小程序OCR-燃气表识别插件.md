# 产品介绍
小程序 OCR-燃气表识别插件可实时识别并返回燃气表信息和相关图片数据。该插件是纯前端能力，无需依赖后端，也不会传输任何数据到后端。

支付宝最低支持版本 10.1.92。

# 产品特色
商家/服务商（ISV）价值：生活缴费场景，减少人工抄表成本，可以让用户自己完成燃气数据上传。

# 使用流程
小程序场景下，以自助抄表为例，用户操作流程：

1. 小程序上选择燃气表识别；
1. 识别插件唤起相机和识别功能，对准燃气表区域扫一扫识别；
1. 识别成功后返回识别结果和图像到小程序；
1. 用户可自行修改识别结果，并提交结果。<br/>
![|258x462](https://cdn.nlark.com/yuque/0/2022/png/179989/1648624730038-e9248fb5-d571-4e55-93bf-91ca6b78a561.png) 

# 接入指引

## 第一步：创建小程序
要在小程序内使用小程序 OCR-燃气表识别插件，首先请完成 [平台入驻](https://opendocs.alipay.com/common/02asmu) 并 [创建小程序](https://opendocs.alipay.com/mini/introduce/create)。

## 第二步：订购插件
完成创建小程序后，使用小程序所属的主体支付宝账号，在 PC 端 [小程序 OCR-燃气表识别插件](https://open.alipay.com/plugin/order-page?serviceCode=MP2020121900100066) 能力详情页点击 **立即订购**，完成插件订购。 

## 第三步：修改小程序参数
示例插件 APPID：2021001153627163

### app.json 插件配置

```json
{
  "pages": [
    "pages/index/index",
    "pages/ocr/ocr"  ],
  "plugins": {
    "myPlugin": {
      "version": "*",
      "provider": "2021001153627163"        // 插件 appId    }
  }
}
```

### OCR 插件页面

#### .json 示例代码

```javascript
// pages/ocr/ocr.json
{
  "usingComponents": {
     "ocr-gas": "plugin://myPlugin/ocr-gas"  }
}
```

#### .axml 示例代码

```html
<!-- pages/ocr/ocr.axml -->
<ocr-gas onComplete="onCompleteOcr" 
         title="{{ocrTitle}}"
         imageOutput="{{imageOutput}}" />
```

#### .js 示例代码

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

### 属性
| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| onComplete | (data) => {} | 是 | 识别结果回调。 |
| title | String | 否 | 提示语。 |
| imageOutput | String | 否 | 返回 ROI 图或全图。<br />**默认值**：roi<br />**可选值**：global |


### 识别结果 data

```javascript
{
  "success": true,
  "result": [
    {
      "name":"ocr_gasMeters",
      "type": "cv_common",
      "body": [
        { "label": "35.58", "conf": 0.6, "pos": [[0.11, 0.22], [0.33, 0.44], [0.11, 0.22], [0.33, 0.44]] }
      ]
    }
  ],
  "image":"base64string"
}
```

## 预览
![|258x462](https://cdn.nlark.com/yuque/0/2022/png/179989/1648624724529-1dfd1bbd-08f6-4504-8841-9941d1c171c0.png)
