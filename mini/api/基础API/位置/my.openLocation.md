
# 简介
**my.openLocation** 是使用支付宝内置地图显示指定经纬度位置的 API。

地图相关接口使用的经纬度坐标格式为 GCJ-02（俗称“火星坐标系”）。

## 使用限制
- 暂无境外地图数据，在中国内地（不含港澳台）以外地区可能无法正常调用此 API。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/d24dde5bf8bd8b7c34f38dd33b8c589b.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例
![|300x540](https://gw.alipayobjects.com/zos/skylark-tools/public/files/5468fba94664d5e279a2acc5ed365ac6.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&originHeight=540&originWidth=300&status=done&style=stroke&width=300)

**说明**：点击 **导航** 后，会引导用户打开高德地图；若未安装高德地图，会引导用户下载高德地图。

# 接口调用

## 示例代码
```javascript
my.openLocation({
  longitude: 120.126293,
  latitude: 30.274653,
  name: '黄龙万科中心',
  address: '学院路77号',
});
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| longitude | String | 是 | 经度，范围为 -180~180，负数表示西经。|
| latitude | String | 是 | 纬度，范围为 -90~90，负数表示南纬。 |
| name | String | 是 | 位置名称。 |
| address | String | 是 | 地址的详细说明。 |
| scale | Number | 否 | 地图缩放比例，范围 3 ~ 19，默认为 15。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |
