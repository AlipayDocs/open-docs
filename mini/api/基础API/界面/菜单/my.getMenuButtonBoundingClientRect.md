
# 简介
获取菜单按钮（右上角胶囊按钮）的布局位置信息，坐标信息以屏幕左上角为原点。

![菜单.png](https://cdn.nlark.com/yuque/0/2021/png/179989/1638855990915-c1522a27-33e7-45d0-9df6-187266b10ed5.png#align=left&display=inline&height=1082&margin=%5Bobject%20Object%5D&name=%E8%8F%9C%E5%8D%95.png&originHeight=2164&originWidth=1088&size=603496&status=done&style=none&width=544)

## 使用限制

- 支付宝客户端版本 10.1.90，**基础库** [1.25.4](https://opendocs.alipay.com/mini/framework/lib) 开始支持，低版本需要做 [兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 由于历史原因，需要使用IDE [2.7.0](https://opendocs.alipay.com/mini/ide/download) 以上版本才可正常调用。

# 接口调用

## 示例代码

### .js 示例代码
```html
// 由于历史原因，请使用『版本号检测』的方式来判断可用性
// compareVersion的参考自 https://opendocs.alipay.com/mini/framework/compatibility
function compareVersion(v1, v2) {
  var s1 = v1.split(".");
  var s2 = v2.split(".");
  var len = Math.max(s1.length, s2.length);
  for (let i = 0; i < len; i++) {
    var num1 = parseInt(s1[i] || "0");
    var num2 = parseInt(s2[i] || "0");
    if (num1 > num2) {
      return 1;
    } else if (num1 < num2) {
      return -1;
    }
  }
  return 0;
}
const clientVersion = my.env.clientVersion || my.getSystemInfo().clientVersion;
const sdkVersion = my.SDKVersion;
if (compareVersion(sdkVersion, '1.25.4') >= 0 && compareVersion(clientVersion, '10.1.90') >= 0) {
 const res = my.getMenuButtonBoundingClientRect();
} else {
 console.log('当前环境不支持调用my.getMenuButtonBoundingClientRect');
}
```

## 返回值
**Object**<br />菜单按钮的布局位置信息

| **属性** | **类型** | **说明** |
| --- | --- | --- |
| width | Number | 胶囊按钮宽度，单位 px。 |
| height | Number | 胶囊按钮高度，单位 px。 |
| top | Number | 胶囊按钮上边界坐标，单位 px。 |
| bottom | Number | 胶囊按钮下边界坐标，单位 px。 |
| left | Number | 胶囊按钮左边界坐标，单位 px。 |
| right | Number | 胶囊按钮右边界坐标，单位 px。 |
| optionMenuWidth | Number | 自定义按钮宽度，单位 px。<br />若无自定义按钮，则无相关字段。 |
| optionMenuHeight | Number | 自定义按钮高度，单位 px。 |
| optionMenuTop | Number | 自定义按钮上边界坐标，单位 px。 |
| optionMenuButtom | Number | 自定义按钮下边界坐标，单位 px。 |
| optionMenuLeft | Number | 自定义按钮左边界坐标，单位 px。 |
| optionMenuRight | Number | 自定义按钮右边界坐标，单位 px。 |
| optionMenuStatus | OptionMenuStatus | iOS 10.2.15、Android 10.2.30 以上支持。 |


### OptionMenuStatus 有效值
| **值** | **说明** |
| --- | --- |
| Favorite | 已收藏 |
| UnFavorite | 未收藏 |
