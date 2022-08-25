# 简介

**my.getSavedFileList** 是获取保存的所有文件信息的 API。

## 使用限制

- 基础库 [1.13.0](https://opendocs.alipay.com/mini/framework/lib)   或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取  [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/b94e35a681410e53a98ad6798530878e.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例

![|300x540](https://gw.alipayobjects.com/zos/skylark-tools/public/files/9c924664a311d3bd246299d29b25a112.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&originHeight=540&originWidth=300&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
my.getSavedFileList({
  success: res => {
    console.log(JSON.stringify(res));
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
| size       | Number   | 文件大小。 |
| createTime | Number   | 创建时间。 |
| apFilePath | String   | 文件路径。 |
