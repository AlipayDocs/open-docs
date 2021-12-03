
# 产品介绍
小程序OCR-燃气表识别插件可实时识别并返回燃气表信息和相关图片数据。该插件是纯前端能力，无需依赖后端，也不会传输任何数据到后端。

支付宝最低支持版本 10.1.92。

# 产品特色
商家/ISV价值：生活缴费场景，减少人工抄表成本，可以让用户自己完成燃气数据上传。

# 使用流程
小程序场景下，以自助抄表为例，用户操作流程：

1. 小程序上选择燃气表识别；
1. 识别插件唤起相机和识别功能，对准燃气表区域扫一扫识别；
1. 识别成功后返回识别结果和图像到小程序；
1. 用户可自行修改识别结果，并提交结果。<br/>
![|224x468](https://intranetproxy.alipay.com/skylark/lark/0/2020/png/5503/1592899834502-5eb6ce8b-4af8-43c8-b404-16374737ff35.png#align=left&display=inline&height=468&margin=%5Bobject%20Object%5D&originHeight=468&originWidth=224&status=done&style=none&width=224) 
![|224x468](https://intranetproxy.alipay.com/skylark/lark/0/2020/png/5503/1592899850224-f8d861e5-9de4-46b5-9920-74c3e2ca3618.png#align=left&display=inline&height=468&margin=%5Bobject%20Object%5D&originHeight=468&originWidth=224&status=done&style=none&width=224) 
![|224x466](https://intranetproxy.alipay.com/skylark/lark/0/2020/png/5503/1592899864902-1c119cdb-f705-4a54-a3ae-dd19b72d2b59.png#align=left&display=inline&height=466&margin=%5Bobject%20Object%5D&originHeight=466&originWidth=224&status=done&style=none&width=224)

# 接入指引

## 第一步：创建小程序
要在小程序内使用小程序OCR-燃气表识别插件，首先请完成 [开发者入驻](https://opendocs.alipay.com/mini/introduce/register) 并 [创建小程序](https://opendocs.alipay.com/mini/introduce/create)。

## 第二步：订购插件
完成创建小程序应用后，使用小程序所属的主体支付宝账号，在 PC 端 [小程序 OCR-燃气表识别插件](https://appstore.alipay.com/abilityprod/detail?abilityCode=PL002020061800011447) 能力详情页点击 **立即订购**，完成插件订购。 

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
![|258x462](https://intranetproxy.alipay.com/skylark/lark/0/2020/png/122911/1590659136944-5ab1b5cb-4970-4e38-8542-9971ecce9aa4.png#align=left&display=inline&height=462&margin=%5Bobject%20Object%5D&originHeight=1010&originWidth=564&status=done&style=none&width=258)
