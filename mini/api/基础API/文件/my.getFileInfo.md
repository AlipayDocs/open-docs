此 API 已停止维护，推荐使用 [FileSystemManager.getFileInfo](https://opendocs.alipay.com/mini/api/0226og)，历史接入此 API 的开发者不受影响。

# 简介

**my.getFileInfo** 是获取 [本地文件](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E6%96%87%E4%BB%B6) 信息的 API。

## 使用限制

- 基础库 [1.4.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/6b701ceeda8e89e8a76065f67b4f4946.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例

![|300x540](https://gw.alipayobjects.com/zos/skylark-tools/public/files/b5510bb7efd866b5a5368099d62156c8.gif#align=left&display=inline&height=540&margin=%5Bobject%20Object%5D&originHeight=540&originWidth=300&status=done&style=stroke&width=300)

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
my.getFileInfo({
  apFilePath: `${my.env.USER_DATA_PATH}/test.txt`,
  digestAlgorithm: 'sha1',
  success: res => {
    console.log(JSON.stringify(res));
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| apFilePath | String | 是 | 文件路径（[本地路径](https://opendocs.alipay.com/mini/03dt4s#%E6%9C%AC%E5%9C%B0%E6%96%87%E4%BB%B6)）。 |
| digestAlgorithm | String | 否 | 摘要算法，支持 md5 和 sha1，默认为 md5。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述**                    |
| -------- | -------- | --------------------------- |
| size     | Number   | 文件大小。单位：字节（B）。 |
| digest   | String   | 摘要结果。                  |
