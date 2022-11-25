# 简介

**my.chooseDistrict** 打开地区选择器。

地区选择器内置数据境内外及港澳台城市数据，可进行差量自定义，也可全量自定义，并可通过在数据中指定 subList 支持级联选择。

## 使用限制

- 基础库 [2.6.2](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本；支付宝客户端 10.2.0 或更高版本，若版本较低，建议采取 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|100x124](https://cdn.nlark.com/yuque/0/2021/png/179989/1624869024841-78a3bc1b-7ff9-458d-bd7d-6978759f3979.png#align=left&display=inline&height=124&margin=%5Bobject%20Object%5D&name=my.chooseDistrict_1.png&originHeight=124&originWidth=100&size=11494&status=done&style=stroke&width=100)

# 接口调用

## 示例代码

### 普通模式

```javascript
my.chooseDistrict({
  mode: 2,
  mainTitle: '境内',
  mainHeadList: [
    {
      title: '定位模块',
      type: 1,
    },
    {
      title: '热门城市',
      list: [
        { name:"杭州", adCode:"330100" },
        { name:"北京", adCode:"110100" },
        { name:"上海", adCode:"310100" },
        { name:"广州", adCode:"440100" },
        { name:"深圳", adCode:"440300" }
      ],
    },
  ],
  mainNormalList: [
    {
      name: '北京市',
      adCode: '110100',
      appendName: '北京',
      subList: [
        { name:"昌平区", adCode:"110114" },
        { name:"朝阳区", adCode:"110105" },
        { name:"大兴区", adCode:"110115" },
        { name:"东城区", adCode:"110101" },
        { name:"房山区", adCode:"110111" },
        { name:"丰台区", adCode:"110106" },
        { name:"海淀区", adCode:"110108" },
        { name:"怀柔区", adCode:"110116" },
        { name:"门头沟区", adCode:"110109" },
        { name:"密云区", adCode:"110118" },
        { name:"平谷区", adCode:"110117" },
        { name:"石景山区", adCode:"110107" },
        { name:"顺义区", adCode:"110113" },
        { name:"通州区", adCode:"110112" },
        { name:"西城区", adCode:"110102" },
        { name:"延庆区", adCode:"110119" }
      ],
    },
  ],
  // 境外
  seniorTitle: '境外/港澳台',
  seniorPageList: [
    {
      title: '亚洲',
      headList: [
        {
          title: '热门城市列表',
          list: [
            { name: '东京', adCode: '39200037000000000000' },
          ],
        },
      ],
      normalList: [
        { name: '喀布尔', adCode: '00400003000100000000' },
        { name: '迪拜', adCode: '78400003000300000000' },
      ],
    },
    {
      title: '大洋洲',
      normalList: [
        { name: '堪培拉', adCode: '03600001000100000000' },
        { name: '斐济', adCode: '24200001000100000000' },
      ],
    },
  ],
  success: (res) => {
    my.alert({
      content: res.name + ':' + res.adCode,
    });
  },
  fail: (res) => {
    my.alert({ title: '调用失败', content: JSON.stringify(res) });
  }
});
```

### src 模式

对于入参数据量较大的场景，可将 my.chooseDistrict 的入参作为 json 文件添加到小程序项目中：

```json
// 文件路径：${app.json 所在目录}/data/chooseDistrict.json
{
  "mode": 2,
  "mainHeadList": [
    {
      "title": "定位模块",
      "type": 1
    }
  ],
  "mainMergeOptions": {
    "371200": "",
    "542400": "",
    "540600": "那曲",
    "659010": "胡杨河市",
    "123456": "测试"
  }
}
```

需要在 mini.project.json 中配置文件路径，否则无法使用：

```json
{
  "include": ["/data/*.json"]
}
```

调用时 my.chooseDistrict 时，将包文件路径作为 src 参数传入：

```javascript
my.chooseDistrict({   
  // src 模式优先级最高，指定 src，只读取 src 内的数据
  src: "/data/chooseDistrict.json",
  success: res => {
    my.alert({
      content: res.name + ':' + res.adCode,
    });
  },
  fail: (res) => {
    my.alert({ title: '调用失败', content: JSON.stringify(res) });
  }
})
```


## 入参

<table>
  <tr>
    <th><b>参数</b></th>
    <th><b>类型</b></th>
    <th><b>必填</b></th>
    <th><b>描述</b></th>
  </tr>
  <tr>
    <td colspan="4"><b>通用场景</b></td>
  </tr>
  <tr>
    <td>mode</td>
    <td>int</td>
    <td>是</td>
    <td>指定场景。枚举如下：</br><ul><li>0：展示境内。</li><li>1：展示境外。</li><li>2：展示境内+境外。</li></ul></td>
  </tr>
  <tr>
    <td>src</td>
    <td>String</td>
    <td>否</td>
  <td>自定义数据文件地址。自定义数据量大时，建议将数据文件内置在小程序内。文件内参数格式同接口定义。<br /><b>注意：</b> src模式优先级最高，指定src，只读取src内的数据</td>
  </tr>
  <tr>
    <td>success</td>
    <td>Function</td>
    <td>否</td>
    <td>成功回调。</td>
  </tr>
  <tr>
    <td>fail</td>
    <td>Function</td>
    <td>否</td>
    <td>失败回调。</td>
  </tr>
  <tr>
    <td colspan="4"><b>境内场景</b></td>
  </tr>
  <tr>
    <td>mainTitle</td>
    <td>String</td>
    <td>否</td>
    <td>境内 Tab 自定义标题。</td>
  </tr>
  <tr>
    <td>mainHeadList</td>
    <td>Array</td>
    <td>否</td>
    <td>头部自定义对象数组。如定位区块、热门城市区块。对象值可查看下方 <b>HeadModel</b>。</td>
  </tr>
  <tr>
    <td>mainNormalList</td>
    <td>Array</td>
    <td>否</td>
    <td>底部城市列表。</br>当对象为空时，默认使用内置的境内城市列表填充。对象值可查看 <b>ItemModel</b>。</td>
  </tr>
  <tr>
    <td>mainMergeOptions</td>
    <td>Object</td>
    <td>否</td>
  <td>修改内置数据的参数接口。传值方式为 <code>{“key”,"value"}</code>。其中 key 是需要修改的城市的 adCode， value 是展示的城市名。</br>仅在 mainNormalList 为空时生效，支持对默认境内数据差量更新:<code>{"371200":"","542400":"","540600":"那曲","659010":"胡杨河市"}</code>。</br>value 为空代表删除对应 adCode 的城市；value 不为空代表更新对应 adCode 的城市。</td>
  </tr>
  <tr>
    <td colspan="4"><b>境外 / 港澳台场景</b></td>
  </tr>
  <tr>
    <td>seniorTitle</td>
    <td>String</td>
    <td>否</td>
    <td>境外 Tab 自定义标题。</td>
  </tr>
  <tr>
    <td>seniorPageList</td>
    <td>Array</td>
    <td>否</td>
    <td>境外多 tab 数据集合, 对象值可查看 <b>PageModel</b>。</br>如果对象为空时，默认使用内置的境外城市列表填充。</td>
  </tr>
</table>

### HeadModel

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| title | String | 是 | 区块名，如“热门城市”。 |
| type | Int | 否 | 模块类型。枚举如下：<br /><ul><li>0：常规城市；</li><li>1：定位模块；</li><li>2：展示支付宝提供的热门城市模块。</li></ul> |
| list | Array | 否 | 区块城市列表。不支持嵌套，对象值可查看 **ItemModel**。 |

### ItemModel

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| name | String | 是 | 城市名。 |
| adCode | String | 是 | 行政区划代码。不同行政区域对应的代码可查看 [中华人民共和国县以上行政区划代码](http://www.mca.gov.cn/article/sj/xzqh/1980/201803/201803131454.html)。 |
| spell | String | 否 | 城市名对应拼音拼写，方便用户检索。 |
| appendName | String | 否 | 子标题。 |
| ext | String | 否 | 额外信息。 |
| subList | Array | 否 | 支持级联，自定义次级城市列表，列表内对象字段可查看 **ItemModel**。 |

### PageModel (境外样式下需要)

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| title | String | 是 | 境外左侧 tab 名称，不带左侧 tab 时可不填。 |
| headList | Array | 否 | 头部对象集合，不支持嵌套，对象值可查看 **HeadModel**。 |
| normalList | Array | 否 | 城市列表，对象值可查看 **ItemModel**。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述**             |
| -------- | -------- | -------------------- |
| name     | String   | 城市名称。           |
| adCode   | String   | 城市编码。           |
| ext      | String   | 自定义扩展字段透传。 |
