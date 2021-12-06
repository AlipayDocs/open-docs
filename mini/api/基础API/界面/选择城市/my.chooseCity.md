
# 简介
**my.chooseCity** 是打开城市选择列表的 API。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/f90e5ac0b3afa41eb2555c1df44812df.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-choose-city?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .axml 示例代码
```html
<!-- API-DEMO page/API/choose-city/choose-city.axml-->
<view class="page">
  <view class="page-description">选择城市 API</view>
  <view class="page-section">
    <view class="page-section-title">my.chooseCity</view>
    <view class="page-section-demo">
      <button type="primary" onTap="chooseCity">选择城市</button>
    </view>
  </view>
  <view class="page-description">修改当前定位城市的名称 API</view>
  <view class="page-section">
    <view class="page-section-title">my.setLocatedCity</view>
    <view class="page-section-demo">
      <button type="primary" onTap="setLocatedCity">修改当前定位城市的名称</button>
    </view>
  </view>
</view>
```

### .js 示例代码
```javascript
// API-DEMO page/choose-city/choose-city.js
Page({
  chooseCity() {
    my.chooseCity({
      showLocatedCity: true,
      showHotCities: true,
      success: (res) => {
        my.alert({
          title: 'chooseCity response: ' + JSON.stringify(res),
        });
      },
    });
  },
  setLocatedCity() {
    my.onLocatedComplete({
      success: (res) => {
        my.setLocatedCity({
          locatedCityId:res.locatedCityId,//res.locatedCityId
          locatedCityName:'修改后的城市名', 
          success: (res) => {
            my.alert({ content: '修改当前定位城市成功' + JSON.stringify(res), });
          },
          fail: (error) => {
            my.alert({ content: '修改当前定位城市失败' + JSON.stringify(error), });
          },
        });
      },
      fail: (error) => {
        my.alert({ content: 'onLocatedComplete失败' + JSON.stringify(error), });
      }
    });
    my.chooseCity({
      showLocatedCity: true,
      showHotCities: true,
      setLocatedCity: true,
      success: (res) => {
        my.alert({
          title: 'chooseCity response: ' + JSON.stringify(res),
        });
      },
    });
  },
});
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| showLocatedCity | Boolean | 否 | 是否显示当前定位城市，默认 false。 |
| showHotCities | Boolean | 否 | 是否显示热门城市，默认 true。 |
| setLocatedCity | Boolean | 否 | 是否修改当前定位城市，默认 false，如果 showLocatedCity 为 false，此设置无效。 |
| cities | Object Array | 否 | 自定义城市列表，列表内对象字段见下方 **自定义城市列表 cities** 表。 |
| hotCities | Object Array | 否 | 自定义热门城市列表，列表内对象字段同 cities。 |
| customHistoryCities | Object Array | 否 | 自定义历史访问城市列表，列表内对象字段同 cities。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


### 自定义城市列表 cities
cities 内对象字段如下所示：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| city | String | 是 | 城市名。 |
| adCode | String | 是 | 行政区划代码。不同行政区域对应的代码可参见 [中华人民共和国县以上行政区划代码](http://www.mca.gov.cn///article/sj/xzqh/2020/2020/202007170301.html)。 |
| spell | String | 是 | 城市名对应拼音拼写，方便用户搜索。 |


#### 示例代码
.js 示例代码
```javascript
//.js
my.chooseCity({
  cities: [
    {
      city: '朝阳区',
      adCode: '110105',
      spell: 'chaoyang'
    },
    {
      city: '海淀区',
      adCode: '110108',
      spell: 'haidian'
    },
    {
      city: '丰台区',
      adCode: '110106',
      spell: 'fengtai'
    },
    {
      city: '东城区',
      adCode: '110101',
      spell: 'dongcheng'
    },
    {
      city: '西城区',
      adCode: '110102',
      spell: 'xicheng'
    },
    {
      city: '房山区',
      adCode: '110111',
      spell: 'fangshan'
    }
  ],
  hotCities: [
    {
      city: '朝阳区',
      adCode: '110105'
    },
    {
      city: '海淀区',
      adCode: '110108'
    },
    {
      city: '丰台区',
      adCode: '110106'
    }
  ],
  success: (res) => {
    my.alert({
      content: res.city + ':' + res.adCode
    });
  },
});
```

### success 回调函数
**说明**：如果用户没有选择任何城市，直接点击了返回，将不会触发回调函数。

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| city | String | 城市名。 |
| adCode | String | 行政区划代码。 |
| longitude | Number | 经度（**注意**：仅用户选择当前定位城市才会返回）。<br />支付宝客户端 10.1.32 及以上版本开始支持。 |
| latitude | Number | 纬度（**注意**：仅用户选择当前定位城市才会返回）。<br />支付宝客户端 10.1.32 及以上版本开始支持。 |

