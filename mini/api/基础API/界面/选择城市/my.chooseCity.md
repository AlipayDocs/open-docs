# 简介

**my.chooseCity** 是打开城市选择列表的 API。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/f90e5ac0b3afa41eb2555c1df44812df.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 在线示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/choose-city?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light)

## 示例代码

一般使用：
```javascript
my.chooseCity({
  showLocatedCity: true, // 显示当前定位城市
  showHotCities: true, // 显示热门城市
  success: res => {
    my.alert({
      title: 'chooseCity success',
      content: JSON.stringify(res),
    });
  },
  fail: err => {
    my.alert({
      title: 'chooseCity fail',
      content: JSON.stringify(err),
    });
  },
});
```

修改当前定位城市名：
```
const chooseCityTask = my.chooseCity({
  showLocatedCity: true, // 显示当前定位城市
  setLocatedCity: true, // 修改当前定位城市
  success: res => {
    my.alert({
      title: 'chooseCity success',
      content: JSON.stringify(res),
    });
  },
  fail: err => {
    my.alert({
      title: 'chooseCity fail',
      content: JSON.stringify(err),
    });
  },
});
// 监听定位完成事件
chooseCityTask.onLocatedComplete(res => {
  // 获取定位位置
  const { longitude, latitude } = res;
  // 修改默认定位城市名
  chooseCityTask.setLocatedCity({ locatedCityName: 'New CityName' });
});
```

使用自定义城市列表：
```javascript
my.chooseCity({
  cities: [
    {
      city: '朝阳区',
      adCode: '110105',
      spell: 'chaoyang',
    },
    {
      city: '海淀区',
      adCode: '110108',
      spell: 'haidian',
    },
    {
      city: '丰台区',
      adCode: '110106',
      spell: 'fengtai',
    },
    {
      city: '东城区',
      adCode: '110101',
      spell: 'dongcheng',
    },
    {
      city: '西城区',
      adCode: '110102',
      spell: 'xicheng',
    },
    {
      city: '房山区',
      adCode: '110111',
      spell: 'fangshan',
    },
  ],
  hotCities: [
    {
      city: '朝阳区',
      adCode: '110105',
      spell: 'chaoyang',
    },
    {
      city: '海淀区',
      adCode: '110108',
      spell: 'haidian',
    },
    {
      city: '丰台区',
      adCode: '110106',
      spell: 'fengtai',
    },
  ],
  success: res => {
    my.alert({
      title: 'chooseCity success',
      content: JSON.stringify(res),
    });
  },
  fail: err => {
    my.alert({
      title: 'chooseCity fail',
      content: JSON.stringify(err),
    });
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| showLocatedCity | Boolean | 否 | 是否显示当前定位城市，默认 false。 |
| showHotCities | Boolean | 否 | 是否显示热门城市，默认 true。 |
| setLocatedCity | Boolean | 否 | 是否修改当前定位城市，默认 false，如果 showLocatedCity 为 false，此设置无效。 |
| cities | Array<Object> | 否 | 自定义城市列表，列表内对象字段见下方 **Array<Object> cities**。 |
| hotCities | Array<Object> | 否 | 自定义热门城市列表，列表内对象字段同 cities。 |
| customHistoryCities | Array<Object> | 否 | 自定义历史访问城市列表，列表内对象字段同 cities。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Array<Object> cities

cities 内对象字段如下所示：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| city | String | 是 | 城市名。 |
| adCode | String | 是 | 行政区划代码。不同行政区域对应的代码可查看 [中华人民共和国县以上行政区划代码](http://www.mca.gov.cn///article/sj/xzqh/2020/2020/202007170301.html)。 |
| spell | String | 是 | 城市名对应拼音拼写，方便用户搜索。 |

### success 回调函数

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| city | String | 城市名。 |
| adCode | String | 行政区划代码。 |
| longitude | Number | 经度（**注意**：仅用户选择当前定位城市才会返回）。<br />支付宝客户端 10.1.32 及以上版本开始支持。 |
| latitude | Number | 纬度（**注意**：仅用户选择当前定位城市才会返回）。<br />支付宝客户端 10.1.32 及以上版本开始支持。 |

## 错误码

| **错误码** | **说明**       |
| ---------- | -------------- |
| 11         | 用户取消操作。 |

## 返回值

[ChooseCityTask](https://opendocs.alipay.com/mini/04naqz)，可用于监听定位完成事件，以及修改默认定位城市的名称。
  
基础库 [2.8.0](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2)、客户端 10.2.70 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。

## Bug & Tip

- 支付宝 10.2.70 以下版本，如果用户没有选择任何城市而直接点击了返回，将不会触发回调函数。
