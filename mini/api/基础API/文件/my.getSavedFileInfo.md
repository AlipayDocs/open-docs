此 API 已停止维护，推荐使用 [FileSystemManager.getFileInfo](https://opendocs.alipay.com/mini/api/0226og)，历史接入此 API 的开发者不受影响。

# 简介

**my.getSavedFileInfo** 是获取保存的文件信息的 API。

## 使用限制

- 基础库 [1.3.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/5b1c31f689c9407c3d43ba17a18f34f5.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例

![|300x536](https://gw.alipayobjects.com/zos/skylark-tools/public/files/3fd64a0c32311e0d9014e9a095473aae.gif#align=left&display=inline&height=536&margin=%5Bobject%20Object%5D&originHeight=536&originWidth=300&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

使用 [my.saveFile](https://opendocs.alipay.com/mini/api/xbll1q) 保存的地址才能够使用 my.getSavedFileInfo。

### .js 示例代码
```javascript
// .js
var that = this;
    my.chooseImage({
    success: (res) => {
      console.log(res.apFilePaths[0], 1212)
      my.saveFile({
        apFilePath: res.apFilePaths[0],
        success: (result) => {
          console.log(result, 1212)
          my.getSavedFileInfo({
            apFilePath: result.apFilePath,
            success: (resu) => {
              console.log(JSON.stringify(resu))
              that.filePath = resu
            }
          })
        },
      });
    },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| apFilePath | String | 是 | 文件路径。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| size | Number | 文件大小。 |
| createTime | Number | 创建时间的时间戳。 |

