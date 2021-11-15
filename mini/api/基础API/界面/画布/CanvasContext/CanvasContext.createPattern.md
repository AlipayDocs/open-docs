> 从基础库 [2.7.9](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始，CanvasContext 相关接口已停止维护，请使用 [Canvas](https://opendocs.alipay.com/mini/01vzqv) 代替。


# 简介
**CanvasContext.createPattern** 是对指定的图像创建模式的方法，可在指定的方向上重复元图像。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|128x158](https://cdn.nlark.com/yuque/0/2021/png/179989/1624962146631-2d9e47e9-40e8-4f38-a51e-a01d9bf60f46.png#align=left&display=inline&height=158&margin=%5Bobject%20Object%5D&originHeight=158&originWidth=128&status=done&style=stroke&width=128)

# 接口调用

## 示例代码

### .js 示例代码
```javascript
const context = my.createCanvasContext('canvas');
const parttern = context.createPattern('https://gw.alipayobjects.com/zos/rmsportal/CuyuyNQuuJvOYOsYvPYd.png', 'repeat');
context.setFillStyle(parttern);
context.fillRect(20, 20, 250, 180);
context.draw();
```

## 入参
**string image**

重复的图像源

**string repetition**

如何重复图像

### repetition 的合法值
| **值** | **说明** |
| --- | --- |
| repeat | 水平竖直方向都重复 |
| repeat-x | 水平方向重复 |
| repeat-y | 竖直方向重复 |
| no-repeat | 不重复 |
