
## Marker 样式优先级说明
- **customcallout、callout** 与 label 互斥 优先级： label > customcallout > callout
- **style 与 icon** 互斥 优先级：style > iconAppendStr、style > icon

## style

### 图鉴列表
| 结构 | 图鉴 | 支持版本 |
| --- | --- | --- |
| {    type:1,    text1:"Style1",    icon1:'xxx',    icon2:'xxx'} | ![](https://cdn.nlark.com/lark/0/2018/png/36245/1537428922033-7f44ea7c-6f28-43cc-a5d0-80cc4cf0213b.png) | 10.1.35 |
| {    type:2,    text1:"Style2",    icon1:'xxx',    icon2:'xxx'} | ![](https://cdn.nlark.com/lark/0/2018/png/36245/1537428730637-bd21f41b-3352-4c42-a2ba-0dca4012b0e3.png)<br /> | 10.1.38 |
| {    type:3,    icon:xxx,  //选填    text:xxx,  //必填    color:xxx,  //默认#33B276    bgColor:xxx,  //默认#FFFFFF     gravity:"left/center/right", //默认 center    fontType:"small/standard/large"  //默认 standard} | ![](https://cdn.nlark.com/lark/0/2018/png/36245/1539856153541-8cecb299-4d29-4661-847b-8abe912081fc.png)<br /> | 10.1.50 |


## customcallout

### 图鉴列表
| 结构 | 图鉴 | 支持版本 |
| --- | --- | --- |
| {    "type": 0,    "time": "3",    "descList": [{        "desc": "点击立即打车",        "descColor": "#ffffff"    }],    "isShow": 1} | ![](https://cdn.nlark.com/lark/0/2018/png/36245/1537429397117-959401db-99f0-48b1-a15d-9817d441d978.png)<br /> | 10.1.32 |
| {    "type": 1,    "time": "3",    "descList": [{        "desc": "点击立即打车",        "descColor": "#333333"    }],    "isShow": 1} | ![](https://cdn.nlark.com/lark/0/2018/png/36245/1537429638548-7a7dd421-7bc7-4849-8498-e8a9a3381618.png)<br /> | 10.1.32 |
| {  "type": 2,  "descList": [{    "desc": "预计",    "descColor": "#333333"  }, {    "desc": "5 分钟",    "descColor": "#108EE9"  }, {    "desc": "到达",    "descColor": "#333333"  }],  "isShow": 1} | ![](https://cdn.nlark.com/lark/0/2018/png/36245/1537429958605-eff755af-bc25-40bd-b697-1d4c2e1be712.png)<br /> | 10.1.32 |


## label

### 参数列表
| 名称 | 描述 | 必填 | 默认值 |
| --- | --- | --- | --- |
| content | 内容 | 是 | - |
| color | 颜色 | 否 | #000000 |
| fontsize | 字号 | 否 | 14 |
| borderRadius | 绘图边角的弧度设置 | 否 | 20 |
| bgColor | 背景颜色 | 否 | #FFFFFF |
| padding | 填充 | 否 | 10 |


### 图鉴列表
| 结构 | 图鉴 | 支持支付宝客户端版本 |
| --- | --- | --- |
| {  content:"Hello Label",  color:"#000000",  fontSize:16,  borderRadius:5,  bgColor:"#ffffff",  padding:12,} | ![](https://cdn.nlark.com/lark/0/2018/png/36245/1537430323991-11bf3fb8-58e7-4416-be4c-2700cdc8f3ec.png) <br /> | 10.1.38 |

