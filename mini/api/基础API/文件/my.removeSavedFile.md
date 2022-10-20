**此 API 已停止维护，推荐使用 [FileSystemManager.removeSavedFile](https://opendocs.alipay.com/mini/api/0229pv)，历史接入此 API 的小程序不受影响。**

# 简介

**my.removeSavedFile** 是删除某个[本地缓存文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%BC%93%E5%AD%98%E6%96%87%E4%BB%B6)的 API。

## 使用限制

- 基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本，支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/8a63c0ed49503d906e08dd04b2d2b6b0.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例

![|368x662](https://gw.alipayobjects.com/zos/skylark-tools/public/files/79576f79a6de2825d1bc0f199bf5d6e4.gif#align=left&display=inline&height=662&margin=%5Bobject%20Object%5D&originHeight=662&originWidth=368&status=done&style=stroke&width=368)

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// 从已保存的本地缓存文件中删除一个。
my.getSavedFileList({
  success: res => {
    my.removeSavedFile({
      apFilePath: res.fileList[0].apFilePath,
      success: res => {
        console.log('remove success');
      },
    });
  },
});
```

## 入参

Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| apFilePath | String | 是 | [本地缓存文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%BC%93%E5%AD%98%E6%96%87%E4%BB%B6)路径，不支持删除其它类型文件的文件路径。注：[本地临时文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6)，当小程序关闭后会自动清理，不需要主动删除。|
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |
