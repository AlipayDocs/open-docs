
# 简介
**my.getFileInfo** 是获取文件信息的 API。

## 使用限制

- 基础库 [1.4.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
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
  apFilePath:'https://resource/apml953bb093ebd2834530196f50a4413a87.video',
  digestAlgorithm:'sha1',
  success:(res)=>{
    console.log(JSON.stringify(res))
  }
})
```

## 入参
入参为Object类型，属性如下

| **属性** | **类型** | **是否必填** | **描述** |
| --- | --- | --- | --- |
| apFilePath | String | 必须 | 文件路径（本地路径）。 |
| digestAlgorithm | String | 可选 | 摘要算法，支持 md5 和 sha1，默认为 md5。 |
| success | Function | 可选 | 调用成功的回调函数。 |
| fail | Function | 可选 | 调用失败的回调函数。 |
| complete | Function | 可选 | 调用结束的回调函数（调用成功、失败都会执行）。 |


## success 回调函数
入参为Object类型，属性如下

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| size | Number | 文件大小。单位：字节（B）。 |
| digest | String | 摘要结果。 |



