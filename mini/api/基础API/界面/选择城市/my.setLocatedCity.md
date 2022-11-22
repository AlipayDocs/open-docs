# 简介

**my.setLocatedCity** 是用于修改 [my.chooseCity](https://opendocs.alipay.com/mini/api/ui-city) 中的默认定位城市的名称的 API。

推荐使用接口 [ChooseCityTask](https://opendocs.alipay.com/mini/04naqz) 替代 my.setLocatedCity。

## 使用限制

- IDE 模拟器暂不支持调试，请以真机调试结果为准。
- 此 API 暂仅支持企业支付宝小程序使用。

## 扫码体验

![|127x157](https://mdn.alipayobjects.com/afts/img/A*uGCmRImDNksAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=4XIxqvsosH7EjPo-LvzPMgAAAABkMK8AAAAA#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/choose-city?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light)

### .js 示例代码

```javascript
// .js
Page({
  data: {
    localcity: '天津',
  },
  chooseCity() {
    my.chooseCity({
      showLocatedCity: true,
      showHotCities: true,
      success: res => {
        my.alert({
          title: `chooseAlipayContact response: ${JSON.stringify(res)}`,
        });
      },
      fail: error => {
        my.alert({ content: `选择失败${JSON.stringify(error)}` });
      },
      complete: () => {
        my.showToast({ content: 'complete回调' });
      },
    });
  },
  noChooseCity() {
    my.chooseCity({
      showLocatedCity: false,
      showHotCities: false,
      success: res => {
        my.alert({ title: `操作成功: ${JSON.stringify(res)}` });
      },
      fail: error => {
        my.alert({ content: `选择失败${JSON.stringify(error)}` });
      },
    });
  },
  selfChooseCity() {
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
        },
        {
          city: '海淀区',
          adCode: '110108',
        },
        {
          city: '丰台区',
          adCode: '110106',
        },
      ],
      success: res => {
        my.alert({ title: `操作成功: ${JSON.stringify(res)}` });
      },
      fail: error => {
        my.alert({ content: `选择失败${JSON.stringify(error)}` });
      },
    });
  },
  self_chooseCity() {
    my.chooseCity({
      showLocatedCity: true,
      showHotCities: true,
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
      ],
      hotCities: [
        {
          city: '朝阳区',
          adCode: '110105',
        },
        {
          city: '海淀区',
          adCode: '110108',
        },
        {
          city: '丰台区',
          adCode: '110106',
        },
      ],
      success: res => {
        my.alert({ title: `操作成功: ${JSON.stringify(res)}` });
      },
      fail: error => {
        my.alert({ content: `选择失败${JSON.stringify(error)}` });
      },
    });
  },
  multiLevelSelect() {
    my.multiLevelSelect({
      title: '请选择城市', // 级联选择标题
      list: [
        {
          name: '杭州市', // 条目名称
          subList: [
            {
              name: '西湖区',
              subList: [
                {
                  name: '文一路',
                },
                {
                  name: '文二路',
                },
                {
                  name: '文三路',
                },
              ],
            },
            {
              name: '滨江区',
              subList: [
                {
                  name: '滨河路',
                },
                {
                  name: '滨兴路',
                },
                {
                  name: '白马湖动漫广场',
                },
              ],
            },
          ], // 级联子数据列表
        },
      ],
      success: result => {
        console.log(result);
        my.alert({ content: `级联${JSON.stringify(result)}` });
      },
      fail: error => {
        my.alert({ content: `调用失败${JSON.stringify(error)}` });
      },
    });
  },
  setLocatedCity() {
    my.chooseCity({
      showLocatedCity: true,
      showHotCities: true,
      setLocatedCity: true,
      success: res => {
        this.setData({
          localcity: res.city,
        });
        my.alert({
          title: `chooseAlipayContact response: ${JSON.stringify(res)}`,
        });
      },
      fail: error => {
        my.alert({ content: `选择失败${JSON.stringify(error)}` });
      },
      complete: () => {
        my.showToast({ content: 'complete回调' });
      },
    });
    my.onLocatedComplete(res => {
      my.setLocatedCity({
        locatedCityId: res.locatedCityId,
        locatedCityName: this.data.localcity,
        success: result => {
          console.log(result);
        },
        fail: error => {
          my.alert({
            content: `修改当前定位城市失败${JSON.stringify(error)}`,
          });
        },
      });
    });
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| locatedCityId | String | 是 | 当前定位城市 ID，my.chooseCity 接口的 onLocatedComplete 返回。 |
| locatedCityName | String | 是 | 当前定位城市的名称。 |
| locatedCityAdCode | String | 否 | 当前定位城市的行政区划代码，不传值时以控件默认拿到的为准。 |
| locatedCityPinyin | String | 否 | 当前定位城市的拼音，不传值时以控件默认拿到的为准。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性**        | **类型** | **描述**             |
| --------------- | -------- | -------------------- |
| locatedCityName | String   | 当前定位城市的名称。 |

### Function fail

fail 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性**     | **类型** | **描述**   |
| ------------ | -------- | ---------- |
| error        | Number   | 错误码。   |
| errorMessage | String   | 错误描述。 |

## 错误码

| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 11 | 参数类型错误。 | 检查参数类型是否正确。 |
| 12 | 必填参数为空。 | 请确认参数 locatedCityId、locatedCityName 是否已填写。 |
| 13 | locatedCityId 不匹配。 | 请确保与 **my.chooseCity** 的 onLocatedComplete 的 locatedCityId 保持一致。 |
