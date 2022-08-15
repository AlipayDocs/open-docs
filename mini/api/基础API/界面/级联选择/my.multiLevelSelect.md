# 简介

**my.multiLevelSelect** 是级联选择功能 API。主要用于选择多级关联数据，例如省市区的信息选择。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/multi-level-select?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light) 

### js 示例代码
```javascript
my.multiLevelSelect({
  title: '多级联选择器',
  list: [{
    name: "杭州市",
    subList: [{
      name: "西湖区",
      subList: [
        { name: "古翠街道" },
        { name: "文新街道" }
      ]
    },{
      name: "上城区",
      subList: [
        { name: "延安街道" },
        { name: "龙翔桥街道" }
      ]
    }]
  },{
    name: "北京市",
    subList: [
      { name: "东城区" },
      { name: "西城区" }
    ]
  }],
  success: (res) => {
    my.alert({
      title: 'multiLevelSelect success',
      content: res.success ? '已选择: ' + JSON.stringify(res.result) : '未选择'
    });
  },
  fail: (res) => {
    my.alert({
      title: 'multiLevelSelect fail',
      content: JSON.stringify(res)
    });
  }
});
```

## 入参

入参为 Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| title | String | 否 | 标题。 |
| list | Object[] | 是 | 选择数据列表。具体格式可查看下方 **Object[] list**。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Object[] list

list 中的每个 Object 支持的属性如下表

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| name | String | 是 | 条目名称。 |
| subList | JsonArray | 否 | 子条目列表。subList 的结构与 list 相同，即支持多级嵌套 |

注意：除了 name 和 subList 以外的属性实际会被忽略，但也会增大 list 数据量，Android 版本上可能导致功能异常。参见后文 **Bug & Tip**

### Function success

success 回调函数会收到一个 Object 类型的参数，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| success | Boolean | 用户是否完成选择 |
| result | Object[] | 选择的结果，如 [{"name":"杭州市"},{"name":"上城区"},{"name":"古翠街道"}] |

## 错误码

| **错误码** | **描述** | **解决方案** |
| --- | --- | --- |
| 2 | 参数无效 | 检查入参 list |


# Bug & Tip

- `bug` Android 版本对于过大的入参 list 支持有缺陷，数据超过 100K 时在部分机型上选择器不能弹出。建议通过删除额外字段等方式控制 list 数据大小
- `bug` 如果传入的 list 为 null，会触发 success 回调（res.success 为 false）而非 fail 回调
- `tip` 若希望选择结果里包含除了 name 以外的更多字段（如 id 等），可参考以下代码自行实现：
```javascript
// 封装 my.multiLevelSelect
// - 对于传入的数据，只向底层接口传递 name 和 subList
// - 对于选中的结果，替换成对应的完整数据条目再回调
function multiLevelSelect({ title, list, success, fail, complete }) {
  const clean = ({ name, subList }) => {
    return { name, subList: subList && subList.map(clean) };
  };
  const lookup = (array, index, pool) => {
    if (array && index < array.length) {
      array[index] = pool.filter(x => x.name === array[index].name)[0];
      lookup(array, index + 1, array[index].subList);
      delete array[index].subList; // 方便回调中的 my.alert 演示。真实代码请删除此行，避免副作用
    }
  };
  const wrap = func => func && (res => {
    res.success && lookup(res.result, 0, list);
    func(res);
  });
  return my.multiLevelSelect({
    title, list: list.map(clean),
    success: wrap(success), fail, complete: wrap(complete)
  });
}

// 调用示例
multiLevelSelect({
  title: '多级联选择器',
  list: [{
    id: 300, name: "杭州市",
    subList: [{
      id: 310, name: "西湖区",
      subList: [
        { id: 311, name: "古翠街道" },
        { id: 312, name: "文新街道" }
      ]
    },{
      id: 320, name: "上城区",
      subList: [
        { id: 321, name: "延安街道" },
        { id: 322, name: "龙翔桥街道" }
      ]
    }]
  }],
  success: (res) => {
    my.alert({
      title: 'multiLevelSelect success',
      content: res.success ? '已选择: ' + JSON.stringify(res.result) : '未选择'
    });
  },
  fail: (res) => {
    my.alert({
      title: 'multiLevelSelect fail',
      content: JSON.stringify(res)
    });
  }
});
```
