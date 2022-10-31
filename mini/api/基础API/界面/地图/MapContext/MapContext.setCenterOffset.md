# 简介

**MapContext.setCenterOffset** 用于设置地图中心偏移。屏幕比例范围为 (0~1)，默认偏移为 [0.5, 0.5]（ 屏幕显示范围的中心位置 ）。默认情况下，中心点在地图中央位置，地图的旋转缩放都将围绕这个点进行。

例如：
offset:[ 0,0 ]时，中心点位于屏幕左上角, offset:[ 1,0 ]时，中心点位于屏幕右上角。
offset:[ 0,1 ]时，中心点位于屏幕左下角, offset:[ 1,1 ]时，中心点位于屏幕右下角。

![|399x225](https://img.alicdn.com/imgextra/i1/O1CN01pZ2gyy1qw4VzgCPEn_!!6000000005559-0-tps-588-780.jpg)

## 使用限制

- 基础库 [2.6.2](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 或更高版本；支付宝客户端 10.2.0 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
this.mapCtx = my.createMapContext('map');
this.mapCtx.setCenterOffset({
  offset: [0.5, 0.6],// 使地图移动，中心点距屏幕顶部的距离是总长的 60%，距离屏幕左侧的距离是总宽的 50%
});
```

## 入参

| **参数** | **类型**        | **必填** | **描述**             |
| -------- | --------------- | -------- | -------------------- |
| offset   | `Array<Number>` | 是       | 偏移量。为两位数组。第一项控制地图中心在屏幕横向 X 轴的位置，第二项控制地图中心在屏幕纵向 Y 轴的位置 |


## 错误码

<table>
  <tr>
      <th><b>错误码</b></th>
      <th><b>说明</b></th>
      <th><b>解决方案</b></th>
  </tr>
  <tr>
      <td >2</td>
      <td>接口参数无效</td>
      <td>
          offset 数组数值目前只支持 0~1
      </td>
  </tr>
  
</table>
