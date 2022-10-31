此 API 已停止维护，推荐使用 [FileSystemManager.getSavedFileList](https://opendocs.alipay.com/mini/api/0228qj)，历史接入此 API 的开发者不受影响。

# 简介

**my.getSavedFileList** 是获取 [my.saveFile](https://opendocs.alipay.com/mini/api/xbll1q) 保存的 [本地缓存文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E7%BC%93%E5%AD%98%E6%96%87%E4%BB%B6) 列表的 API。

## 使用限制

- 基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/b94e35a681410e53a98ad6798530878e.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例

![|300x540](https://gw.alipayobjects.com/zos/skylark-tools/public/files/9c924664a311d3bd246299d29b25a112.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&originHeight=540&originWidth=300&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码

```javascript
my.getSavedFileList({
  success: res => {
    console.log(res);
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型**     | **描述**   |
| -------- | ------------ | ---------- |
| fileList | List\<File\> | 文件列表。 |

#### List\<File\> fileList

| **属性**   | **类型** | **描述**   |
| ---------- | -------- | ---------- |
| size       | Number   | 文件大小。单位为 Byte。 |
| createTime | Number   | 创建时间。 |
| apFilePath | String   | 文件路径。 |
